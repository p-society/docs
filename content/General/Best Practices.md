Unlike [guidelines](Guidelines), these are not enforcements. They are suggestions and advice for writing performant, maintainable and scalable code. You should follow these to have a great degree of control over the code you write, avoid unnecessary abstraction and [technical debt](Glossary/Non-technical/Technical Debt) in the code base.

### 1. Write Atomic Code

It is easy to keep bundling functionality into a single block of logic in our code. We must avoid this and write code that is decoupled, atomic and reusable.

Say, we have to implement a function `renderPDFAndUploadToS3` that has to:
-  render some template HTML into a PDF
-  upload it to AWS S3
-  patch the URL of the file into database and return it

It's not uncommon to see an implementation like this:

```javascript
async function renderPDFAndUploadToS3(templatePath, data) {

	try {
		const templateHtml = fs.readFileSync(templatePath, 'utf-8');
		const template = Handlebars.compile(templateHtml);
		const html = template(data);

		const browser = await puppeteer.launch();
		const page = await browser.newPage();
	    await page.setContent(html, { waitUntil: 'networkidle0' });
		const pdfBuffer = await page.pdf(this.defaultPDFOptions);
		await browser.close()

		const fileName = `${Date.now().toString()}`;
		const command = new PutObjectCommand({
			pdfBuffer,
		    fileName,
		    this.s3Client,
		    this.s3PDFOptions,
		});
		await this.s3Client.send(command);

		const response = this.userModel.findOneAndUpdate(
			{ data.userId }, 
			{ pdf: this.s3PDFOptions.Key}
		);

		return this.s3PDFOptions.Key;
	} catch (error) {
		throw new Error(
		"Something while rendering, uploading or patching went wrong. 🤷‍♂️"
		);
	}
	
}
```

Not only is the code difficult to read and understand it is also **hard to test, maintain, and reuse.** By bundling multiple responsibilities into a single function, we've violated the **Single Responsibility Principle (SRP)**. Each step in the function handles a distinct concern: rendering the PDF, uploading it to S3, and updating the database. This tight coupling makes debugging and extending the functionality unnecessarily complex.

Instead write all the separate logic as independent and self-contained functions.

```javascript

async function renderPDF(templatePath, data) {
  const templateHtml = fs.readFileSync(templatePath, "utf-8")
  const template = Handlebars.compile(templateHtml)
  const html = template(data)
  
  const browser = await puppeteer.launch()
  const page = await browser.newPage()
  await page.setContent(html, { waitUntil: "networkidle0" })
  
  const pdfBuffer = await page.pdf(this.defaultPDFOptions)
  await browser.close()
  
  return pdfBuffer
}

async function uploadToS3(pdfBuffer, fileName, s3Client, s3Options) {
  const options = { ...s3Options, Key: fileName, Body: pdfBuffer }
  const command = new PutObjectCommand(options)
  await s3Client.send(command)
  
  return options.Key
}

async function updateDatabase(userModel, userId, pdfKey) {
  return userModel.findOneAndUpdate(
    { _id: userId },
    { pdf: pdfKey },
    { new: true }
  )
}

async function renderPDFAndUploadToS3(templatePath, data) {
  try {
    const pdfBuffer = await renderPDF(templatePath, data)
    
    const fileName = `${Date.now().toString()}.pdf`
    const pdfKey = await uploadToS3(
      pdfBuffer,
      fileName,
      this.s3Client,
      this.s3PDFOptions
    )

    await updateDatabase(this.userModel, data.userId, pdfKey)

    return pdfKey
  } catch (error) {
    throw new Error("Something went wrong: " + error.message)
  }
}


```

Now each function can scale, change and handle errors in it's own scope. This implementation not only makes it easy to read and understand the code but delegates responsibility to separate functions making them independent to change in other functions, easy to debug and reusable.

### 2. Usage of AI
### 3. Approach to Roadblocks
### 4. Blueprint before writing

