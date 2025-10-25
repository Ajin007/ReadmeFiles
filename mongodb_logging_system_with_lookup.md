
# MongoDB Mini Project: Logging System with Capped Collection, Indexing, Validation, and Lookup

## 1. Show Databases
The `show dbs` command is used to list all available databases in MongoDB.

```bash
show dbs
```
This will return a list of all databases.

## 2. Use a Database
To switch to a specific database:

```bash
use app_logs
```
If the database doesn't exist, it will be created when you insert data.

## 3. Create a Collection
You can create a new collection explicitly with `db.createCollection()`:

```bash
db.createCollection("logs")
```

If you don't need any special options, MongoDB will create collections automatically when you insert the first document.

## 4. Capped Collection for Logs
A capped collection is used for storing logs or event data where the collection has a maximum size, and old records are automatically overwritten.

To create a capped collection:

```bash
db.createCollection("logs", { capped: true, size: 500000 })
```
Here, `size: 500000` specifies the size limit of the collection in bytes.

## 5. Schema Validation for Collection
MongoDB allows you to enforce validation rules when creating collections. You can define validation rules for documents to ensure they follow a specific schema.

Example:

```bash
db.createCollection("logs", {
    validator: {
        $jsonSchema: {
            bsonType: "object",
            required: ["timestamp", "level", "message"],
            properties: {
                timestamp: {
                    bsonType: "date",
                    description: "Timestamp must be a valid date"
                },
                level: {
                    bsonType: "string",
                    enum: ["info", "warning", "error"],
                    description: "Level must be one of 'info', 'warning', or 'error'"
                },
                message: {
                    bsonType: "string",
                    description: "Message must be a string"
                }
            }
        }
    }
})
```

## 6. Inserting Sample Data into the `logs` Collection
Now, insert documents into the capped collection.

```bash
db.logs.insertOne({ timestamp: new Date(), level: "info", message: "Application started successfully" })
db.logs.insertOne({ timestamp: new Date(), level: "warning", message: "Memory usage is high" })
db.logs.insertOne({ timestamp: new Date(), level: "error", message: "Database connection failed" })
```

## 7. Indexing
Indexes are important for query performance, especially on frequently queried fields.

Creating an index on the `level` field:

```bash
db.logs.createIndex({ level: 1 })
```

## 8. Querying Logs by Level
With the index in place, querying logs based on the `level` field will be faster.

```bash
db.logs.find({ level: "error" })
```

## 9. Getting the Database Name and Listing Collections
You can use `getName()` and `getCollectionNames()` to get the current database name and list all collections.

```bash
db.getName()  # Returns the current database name
db.getCollectionNames()  # Lists all collections in the current database
```

## 10. Lookup: Joining Collections
MongoDB's `$lookup` stage in the aggregation pipeline allows you to perform joins between collections, similar to SQL `JOIN`.

### Scenario: Join Logs with Users Collection
Imagine you have a `users` collection, and each log document includes a `userId` that references a user. You can use `$lookup` to join the logs with the users.

### Users Collection Example:
```bash
db.users.insertMany([
    { _id: 1, name: "John Doe", email: "john@example.com" },
    { _id: 2, name: "Jane Smith", email: "jane@example.com" }
])
```

### Lookup Example:
```bash
db.logs.aggregate([
    {
        $lookup: {
            from: "users",
            localField: "userId",  # Field in the logs collection
            foreignField: "_id",   # Field in the users collection
            as: "user_info"
        }
    }
])
```

In this example:
- The `userId` field from the `logs` collection is matched with the `_id` field from the `users` collection.
- The resulting documents will include an array field called `user_info` that contains the matched user data.

## 11. Performance Considerations
- **Indexes**: Indexing is crucial for fast querying. The `level` index in this example speeds up queries based on the log level.
- **Capped Collections**: Capped collections are useful for log data, where old logs are overwritten as the collection reaches its size limit.
- **Aggregation and `$lookup`**: The `$lookup` operator allows you to join data from multiple collections, enabling more complex queries in MongoDB.
- **Sharding**: For extremely large datasets, sharding allows MongoDB to distribute data across multiple servers.

---

## Final Thoughts
This mini project covers essential MongoDB features like capped collections, schema validation, indexing, and aggregation with `$lookup`. These are commonly used in production environments to manage data efficiently and maintain performance.

You can extend this project by adding more collections, additional queries, and more advanced aggregation pipelines based on your requirements.
