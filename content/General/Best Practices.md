Unlike [guidelines](Guidelines), these are not enforcements. They are suggestions and advice for writing performant, maintainable and scalable code. You should follow these to have a great degree of control over the code you write, avoid unnecessary abstraction and [technical debt](Glossary/Non-technical/Technical-Debt) in the code base.

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

It would be easier to ask you to use AI judiciously but I will (try to) list everything you should choose to do (and not do) with all the amazing LLMs out there.

A general fact - to learn and write great code you must go through frustrating, anxious, confusing, self-doubting, blood-boiling, hair-pulling, banging-head-on-your-keyboard and about-to-cry hours in front of your computer. That's the best way to do it. That's the best way to learn.

It's easy to find 'quick' solutions to complex problems using AI but that comes with it's side effects. When we brute force our way out of problems using AI, it general looks like this: 
- GPT a solution
- use the subpar solution
- face bottlenecks, roadblocks and errors in the subpar solution
- GPT the solution again

We keep doing this until the code becomes a mix of generated code that looks fancy, code we have some vague idea of and code that operates on very low confidence levels. This not only makes you more dependent on AI for the next steps but introduces abstraction that was never needed.

How you should use them so they support you:
- Don't copy-pasta generated code unless it's **test data, complex database queries/aggregations/regular-expressions, repetition of code you fully understand or a refactor of code you originally wrote.** 
- Use it to understand errors, not bypass them. 
- Read documentation to understand usage of a technology before asking an LLM.
### 3. Approach To Roadblocks

You will inevitably hit roadblocks. 

Try to:
- Read official documentation of the technology
- Find solutions in blogs/articles/forums
- Ask a peer or senior
- Ask an LLM
- Go through the source code

In order, from the top.
### 4. Blueprint Before Writing

'Figuring out as you write' is the surest way to write code that could have been written better. You should have a mental or physical (scribble on a page as much as you can) blueprint of the system/sub-system you are going to write. 

Know what you are writing before you write. 

