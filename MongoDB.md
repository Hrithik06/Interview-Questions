# 1. Field Required to Enable Sharding on a Collection in MongoDB

To enable sharding on a MongoDB collection, you **must specify a shard key**. The shard key is a field (or a combination of fields) in your documents that MongoDB uses to distribute data across shards.

- The **shard key** is mandatory when running the sharding command (e.g., `sh.shardCollection()`).
- The collection must have an index whose prefix is the shard key.
- The shard key determines how documents are partitioned and distributed among the shards.

**Example:**
```js
sh.shardCollection("myDatabase.myCollection", { "myShardKey": 1 })
```
Here, `"myShardKey"` is the required field specified as the shard key.

---

### **Summary Table**

| Requirement                | Description                                                   |
|----------------------------|--------------------------------------------------------------|
| Shard Key Field            | Field(s) used to distribute documents across shards          |
| Shard Key Index            | Collection must have an index on the shard key field(s)      |

---

**In summary:**  
The required field to enable sharding on a MongoDB collection is the **shard key**—a field or fields that determine how data is distributed across shards.

# 2. Use of `$lookup` Aggregation in MongoDB

The `$lookup` aggregation stage in MongoDB is used to **perform a left outer join between documents from two collections** within the same database. This allows you to combine related data from different collections in a single query, similar to SQL joins.

---

### **Key Purposes and Benefits**

- **Join Data Across Collections:** Fetch related documents from another collection and merge them into the results of your aggregation pipeline.
- **Reduce Redundant Queries:** Retrieve all necessary related data in a single operation, eliminating the need for multiple queries.
- **Enable Relational-like Queries:** Perform SQL-like joins in a NoSQL environment, which is useful for reporting, analytics, and complex data retrieval.

---

### **How `$lookup` Works**

- It matches documents from the input (primary) collection with documents from the foreign (secondary) collection based on specified fields.
- The matched documents are included in an array field in the output documents.
- If there are no matches, the array field will be empty, but the input document still appears in the results (left outer join behavior).

---

### **Basic Syntax**

```js
{
  $lookup: {
    from: "",
    localField: "",
    foreignField: "",
    as: ""
  }
}
```
- `from`: Name of the collection to join with.
- `localField`: Field from the input documents.
- `foreignField`: Field from the foreign collection.
- `as`: Output array field name for joined documents.

---

### **Example**

Suppose you have `orders` and `customers` collections, and you want to get each order with its customer details:

```js
db.orders.aggregate([
  {
    $lookup: {
      from: "customers",
      localField: "customer_id",
      foreignField: "_id",
      as: "customer_details"
    }
  }
])
```
- This will add a `customer_details` array to each order, containing the matching customer document(s).

---

### **Summary Table**

| Feature                | Description                                              |
|------------------------|---------------------------------------------------------|
| Join Type              | Left outer join between collections                     |
| Use Case               | Combine related data from multiple collections          |
| Output                 | Input docs with an array of matched foreign docs        |
| SQL Equivalent         | `LEFT OUTER JOIN`                                       |

---

**In summary:**  
The `$lookup` aggregation stage in MongoDB is used to join documents from two collections, enabling you to combine and query related data in a single aggregation pipeline, similar to performing a left outer join in SQL.


# 3. What is a Capped Collection in MongoDB?

A **capped collection** in MongoDB is a **fixed-size collection** that automatically overwrites its oldest documents when it reaches its size limit, functioning similarly to a circular buffer.

---

### **Key Characteristics**

- **Fixed Size:** You specify the maximum size (in bytes) and optionally the maximum number of documents when creating the collection.
- **Insertion Order:** Documents are stored and retrieved in the order they were inserted; no additional index is needed for this.
- **Automatic Overwrite:** When the collection’s size limit is reached, the oldest documents are automatically removed to make room for new ones.
- **High Throughput:** Supports high-performance insert and read operations, making it suitable for logging, caching, or queue-like scenarios.
- **Restrictions:** Documents cannot be deleted manually (except by dropping the collection), and updates must not increase the document size. Capped collections cannot be sharded.

---

### **How to Create a Capped Collection**

```js
db.createCollection("log", { capped: true, size: 100000 })
```
- This creates a capped collection named `log` with a maximum size of 100,000 bytes.

---

### **Common Use Cases**

- **Log storage:** Retain only the most recent logs, automatically discarding the oldest.
- **Cache:** Store temporary data where only the latest entries are important.
- **FIFO Queues:** Maintain a fixed-length queue of data.

---

### **Summary Table**

| Feature                | Description                                               |
|------------------------|----------------------------------------------------------|
| Fixed size             | Yes (set at creation)                                    |
| Overwrites oldest data | Yes, when size limit is reached                          |
| Maintains order        | Yes, insertion order                                     |
| High throughput        | Yes, for insert and read                                 |
| Manual delete          | No (except by dropping collection)                       |
| Use cases              | Logging, caching, FIFO queues                            |

---

**In summary:**  
A capped collection in MongoDB is a fixed-size, high-performance collection that automatically overwrites the oldest documents as new ones are inserted, making it ideal for logs, caches, and similar use cases.


# 4. Transactions in MongoDB

### **What Are Transactions?**

Transactions in MongoDB allow you to group multiple read and write operations into a single, atomic unit of work. This means that either **all operations within the transaction succeed and are committed together, or none of them are applied**—ensuring data consistency and integrity.

---

### **ACID Properties in MongoDB Transactions**

MongoDB transactions are **ACID-compliant**, which means they guarantee:
- **Atomicity:** All operations in the transaction are executed as a single unit; if any operation fails, the entire transaction is rolled back.
- **Consistency:** The database moves from one valid state to another, never leaving it in an invalid state.
- **Isolation:** Transactions are isolated from each other; intermediate states are not visible to other transactions.
- **Durability:** Once a transaction is committed, its changes are permanent, even in the event of a system failure.

---

### **Key Features**

- **Multi-document Transactions:** Introduced in MongoDB 4.0, allowing atomic operations across multiple documents, collections, and databases.
- **Distributed Transactions:** Supported from MongoDB 4.2, enabling transactions across sharded clusters.
- **Session-based:** Transactions are started and managed within a session object.

---

### **Typical Use Cases**

- **Banking and Financial Applications:** Where money must be debited from one account and credited to another atomically.
- **Order Management:** Ensuring inventory is updated and an order is created together.
- **Any scenario requiring data integrity across multiple documents or collections**.

---

### **How to Use Transactions**

1. **Start a Session:** Create a session object.
2. **Start a Transaction:** Use the session to start a transaction.
3. **Perform Operations:** Execute your read/write operations within the transaction.
4. **Commit or Abort:** Commit the transaction to apply changes, or abort to roll back if an error occurs.

**Example (Pseudocode):**
```js
const session = client.startSession();
session.startTransaction();
try {
  // Perform multiple operations
  db.collection1.insertOne(..., { session });
  db.collection2.updateOne(..., { session });
  // Commit if everything succeeds
  session.commitTransaction();
} catch (error) {
  // Abort on error
  session.abortTransaction();
}
session.endSession();
```

---

### **Benefits and Considerations**

- **Ensures data integrity** across complex operations.
- **Can introduce performance overhead,** so use only where necessary.
- **Not all applications need transactions:** For many use cases, MongoDB’s single-document atomicity is sufficient.

---

**In summary:**  
Transactions in MongoDB enable you to group multiple operations into a single atomic, consistent, isolated, and durable unit of work—ensuring data integrity across multiple documents, collections, and even shards, especially useful for critical business logic and financial operations.

# 5. Command to Show All Collections in MongoDB

To list all collections in the current database in MongoDB, use the following command in the MongoDB shell:

```js
show collections
```
- This will display the names of all collections in the currently selected database.

**Steps:**
1. Switch to your desired database:
   ```js
   use your_database_name
   ```
2. Then run:
   ```js
   show collections
   ```

**Alternative methods:**
- You can also use:
  ```js
  db.getCollectionNames()
  ```
  or
  ```js
  db.runCommand({ listCollections: 1, nameOnly: true })
  ```
  to get the list programmatically.

---

**In summary:**  
The standard command to show all collections in the current MongoDB database is:
```js
show collections
```
# 6. To get the current database name in MongoDB, use either of these commands in the MongoDB shell:

- Simply type:
  ```js
  db
  ```
  This will output the name of the current database.

- Or, for a method that returns the name as a string:
  ```js
  db.getName()
  ```
  This also returns the current database name.

Both commands are standard and widely used to check which database you are currently working in.


# 7. Command to Update Multiple Documents in MongoDB

To update multiple documents in a MongoDB collection, use the `updateMany()` method. This method applies the specified update to all documents that match the filter criteria.

---

### **Syntax**

```
db.collection.updateMany(
  ,
  ,
  
)
```

- ``: Criteria to select documents to update.
- ``: Update operations (e.g., `$set`, `$inc`).
- ``: (Optional) Additional options.

---

### **Example**

Suppose you want to set the `status` field to `"active"` for all documents where `age` is greater than 30:

```
db.users.updateMany(
  { age: { $gt: 30 } },
  { $set: { status: "active" } }
)
```
This command will update the `status` field to `"active"` for every document in the `users` collection where the `age` is greater than 30.

---

### **Summary Table**

| Method                    | Description                         |
|---------------------------|-------------------------------------|
| `updateMany()`            | Updates all documents matching filter|

---

**In summary:**  
Use `db.collection.updateMany(, )` to update multiple documents in MongoDB that match the given filter.
