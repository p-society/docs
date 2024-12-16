We made a  `GlobalService`  provider class that hosts a set of robust methods to interact with the database in a clean and efficient manner, aligning with the philosophy of simplicity and flexibility, which is heavily inspired by the Feathers.js framework. The methods available — `_find`, `_create`, `_patch`, `_get`, and `_remove`—serve as the core tools for performing CRUD (Create, Read, Update, Delete) operations.

1. `_find`: This method allows for querying and retrieving data based on specific query options, such as filtering, sorting, and pagination. It is designed to work efficiently with large datasets, enabling developers to fetch only the data they need. This aligns with Feathers.js's philosophy of making data fetching and manipulation as flexible as possible.

2. `_create`: This method is used for creating new records, whether it's a single record or multiple records at once. It provides a simple, consistent way to handle record creation, reducing the complexity of having to write repetitive logic for inserting new data. Feathers.js’s philosophy of "convention over configuration" is evident here, as it abstracts much of the complexity.

3. `_patch`: This method updates existing records, allowing partial updates. This is particularly useful for making modifications to only certain fields of a record without needing to resend the entire data. This method promotes the Feathers approach of efficient updates, ensuring minimal data transfer and server load.

4. `_get`: This method retrieves a single record based on its unique identifier. It provides a quick and simple way to fetch specific records when needed. This simplicity and directness in accessing individual records follow Feathers’ focus on making common tasks like fetching data as straightforward as possible.

5. `_remove`: This method handles the deletion of records, either through soft deletes (marking records as deleted without actually removing them from the database) or hard deletes (completely removing the records). This method offers flexibility in managing data integrity, allowing developers to decide the best approach for data deletion.

The overall benefit of using these methods is that they provide a consistent, reusable interface for database interactions. They allow developers to focus more on business logic rather than on writing repetitive database code. Additionally, this approach promotes clean, maintainable code that can scale with the application's growth. 

The `GlobalService` ensures that operations are lightweight, flexible, and efficient, aligning with the principles of RESTful APIs and making it easier for developers to build, maintain, and scale applications, while helping the code-quality developers to improve the quality of existing services from a Single POC.

Learn more about this here: [Porting Feathers.js (v4) to NestJS: Global Service Provider and Presence Gateway Integration](https://github.com/p-society/gc-broadcast/pull/9 )

# Querying

The query options and filters provide a powerful and flexible way written by us to control how data is retrieved from the database. By utilizing these options, you can filter, sort, paginate, and populate related data efficiently. The available query options are:

- **$select**: This option allows you to specify which fields to include in the result, optimizing the query by limiting the data returned. It ensures that only the necessary fields are fetched, improving performance.

- **$sort**: This option determines the sorting order of the result set. A value of `1` indicates ascending order, while `-1` represents descending order. Sorting helps in organizing data according to your needs.

- **$limit: This  option restricts the number of records returned. This is especially useful when working with large datasets, ensuring that only a manageable number of records are retrieved at a time.

- **$skip**: This option allows you to skip a specific number of records, commonly used in pagination. It helps in retrieving data in chunks, improving user experience in applications where large amounts of data are displayed across multiple pages.

- **$populate**: This option is used to populate related documents or fields, reducing the need for additional queries. It is useful for retrieving associated data from other collections or tables, which is essential for handling relationships between entities.

In addition to these core query options, there are several **InternalQueryOptions** that provide more advanced filtering and querying capabilities:

Learn about all the currently supported options [here](https://github.com/p-society/gc-broadcast/blob/dev/src/types/QueryOptions.d.ts).

### Examples of Querying Data with Query Parameters

Let’s say you generated a `user`  module  using the `yarn generate users` command. Now, you can easily query the users' API using query parameters to retrieve the exact data you need, without writing custom routes!

#### Example Schema: User

Your `User` schema might look something like this:

```javascript
{
  _id: ObjectId,
  name: String,
  email: String,
  createdAt: Date,
  organization: { type: ObjectId, ref: 'Organization' }
}
```

### Fetching the Latest Users

Instead of writing a separate function like `findUsersLatest()`, you can query for the latest users using query parameters:

```
http://localhost:3000/users?$sort[createdAt]=-1
```

This sorts users by the `createdAt` field in descending order. It’s a quick and efficient way to fetch the most recently created users.

#### Sample Response:

```json
[
[
  {
    "_id": "user1_id",
    "name": "Soubhik Gon",
    "email": "b422056@iiit-bh.ac.in",
    "createdAt": "2024-12-16T10:00:00Z",
    "organization": "org1_id"
  },
  {
    "_id": "user2_id",
    "name": "Saswat PB",
    "email": "b122103@iiit-bh.ac.in",
    "createdAt": "2024-12-14T15:30:00Z",
    "organization": "org2_id"
  }
]
]
```

### Populating Related Fields

If your `User` schema contains a reference to another collection, such as an `organization` field, you can easily populate that field with the related data. Here’s how you do it:

```
http://localhost:3000/users?$populate=organization
```

This will automatically include the related `organization` data in the response for each user.

#### Sample Response with Populated Data:

```json
[
  {
    "_id": "60f7c9f3f8d5e8b28c7f1c4a",
    "name": "Soubhik Gon",
    "email": "b422056@iiit-bh.ac.in",
    "createdAt": "2024-12-15T12:00:00Z",
    "organization": {
      "_id": "org1_id",
      "name": "IIIT Bhubaneswar",
      "industry": "Education"
    }
  },
  {
    "_id": "60f7c9f3f8d5e8b28c7f1c4b",
    "name": "Saswat PB",
    "email": "b122103@iiit-bh.ac.in",
    "createdAt": "2024-12-14T09:30:00Z",
    "organization": {
      "_id": "org2_id",
      "name": "IIT Bhubaneswar",
      "industry": "Education"
    }
  }
]

```

Some more common query options you will be using is 
$paginate = true / false
$regex
$or


### Examples of Querying Data in Internal Services

when you are developing services, there will come cases where u want to access other services to get the data managed by them
eg: a userService might require 

