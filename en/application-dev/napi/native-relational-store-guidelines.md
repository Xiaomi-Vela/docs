# RelationalStore Development Guide


## When to Use

RelationalStore provides a complete mechanism for local database management. It offers a series of interfaces for adding, deleting, modifying, and querying data in an RDB store. To satisfy different needs in complicated scenarios, RelationalStore also supports direct execution of SQL statements.


## Basic concepts

- **OH_Predicates**: A representation of the property or feature of a data entity, or the relationship between data entities. It is used to define operation conditions.

- **OH_Cursor**: A set of query results, which allows access to the required data in flexible modes.


## Restrictions

- The default logging mode is Write Ahead Log (WAL), and the default flushing mode is **FULL** mode.

- RelationalStore supports a maximum of four connection pools to manage read and write operations.

- To ensure data accuracy, only one write operation is allowed at a time.

- Once an application is uninstalled, related database files and temporary files on the device are automatically deleted.


## Available APIs

For details about the APIs, see [RDB](../reference/native-apis/_r_d_b.md).

| API| Description|
| -------- | -------- |
| OH_Rdb_GetOrOpen(const OH_Rdb_Config *config, int *errCode) | Obtains an OH_Rdb_Store instance for RDB store operations.|
| OH_Rdb_Execute(OH_Rdb_Store *store, const char *sql) | Executes an SQL statement that contains specified arguments but returns no value.|
| OH_Rdb_Insert(OH_Rdb_Store *store, const char *table, OH_VBucket *valuesBucket) | Inserts a row of data into a table.|
| OH_Rdb_Update(OH_Rdb_Store *store, OH_VBucket *valuesBucket, OH_Predicates *predicates); | Updates data in the RDB store based on the specified OH_Predicates instance.|
| OH_Rdb_Delete(OH_Rdb_Store *store, OH_Predicates *predicates) | Deletes data from the RDB store based on the specified OH_Predicates instance.|
| OH_Rdb_Query(OH_Rdb_Store *store, OH_Predicates *predicates, const char *const *columnNames, int length) | Queries data in the RDB store based on specified conditions.|
| OH_Rdb_DeleteStore(const OH_Rdb_Config *config) | Deletes an RDB store.|


## How to Develop

1. Obtain the OH_Rdb_Store instance and create a database file.

   Example:

   ```c
   // Create an OH_Rdb_Config object.
   OH_Rdb_Config config;
   // The path is the application sandbox path.
   config.dataBaseDir = "xxx";
   // Database file name.
   config.storeName = "RdbTest.db";
   // Application bundle name.
   config.bundleName = "xxx";
   // Module name.
   config.moduleName = "xxx";
   // Security level of the database file.
   config.securityLevel = OH_Rdb_SecurityLevel::S1;
   // Whether the database is encrypted.
   config.isEncrypt = false;
   // Memory size occupied by config.
   config.selfSize = sizeof(OH_Rdb_Config);

   int errCode = 0;
   // Obtain the OH_Rdb_Store instance.
   OH_Rdb_Store *store_ = OH_Rdb_GetOrOpen(&config, &errCode);
   ```

2. After obtaining the OH_Rdb_Store instance, call **OH_Rdb_Execute** to create a table and call **OH_Rdb_Insert** to insert data to the table created.

   Example:

   ```c
   char createTableSql[] = "CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, "
                           "AGE INTEGER, SALARY REAL, CODES BLOB)";
   // Create a table.
   OH_Rdb_Execute(store_, createTableSql);

   // Create a key-value pair instance.
   OH_VBucket *valueBucket = OH_Rdb_CreateValuesBucket();
   valueBucket->putText(valueBucket, "NAME", "Lisa");
   valueBucket->putInt64(valueBucket, "AGE", 18);
   valueBucket->putReal(valueBucket, "SALARY", 100.5);
   uint8_t arr[] = {1, 2, 3, 4, 5};
   int len = sizeof(arr) / sizeof(arr[0]);
   valueBucket->putBlob(valueBucket, "CODES", arr, len);
   // Insert data.
   int rowId = OH_Rdb_Insert(store_, "EMPLOYEE", valueBucket);
   // Destroy the KV pair instance.
   valueBucket->destroy(valueBucket);
   ```

   > **NOTE**
   >
   > **RelationalStore** does not provide explicit flush operations for data persistence. **insert()** stores data in a file persistently.

3. Modify or delete data based on the specified **Predicates** instance.

   Call **OH_Rdb_Update** to modify data and call **OH_Rdb_Delete** to delete data.

   Example:

   ```c
   // Modify data.
   OH_VBucket *valueBucket = OH_Rdb_CreateValuesBucket();
   valueBucket->putText(valueBucket, "NAME", "Rose");
   valueBucket->putInt64(valueBucket, "AGE", 22);
   valueBucket->putReal(valueBucket, "SALARY", 200.5);
   uint8_t arr[] = {1, 2, 3, 4, 5};
   int len = sizeof(arr) / sizeof(arr[0]);
   valueBucket->putBlob(valueBucket, "CODES", arr, len);

   OH_Predicates *predicates = OH_Rdb_CreatePredicates("EMPLOYEE");
   OH_VObject *valueObject = OH_Rdb_CreateValueObject();
   const char *name = "Lisa";
   valueObject->putText(valueObject, name);
   predicates->equalTo(predicates, "NAME", valueObject)->andOperate(predicates);
   uint32_t count = 1;
   double salary = 100.5;
   valueObject->putDouble(valueObject, &salary, count);
   predicates->equalTo(predicates, "SALARY", valueObject);

   int changeRows = OH_Rdb_Update(store_, valueBucket, predicates);
   valueObject->destroy(valueObject);
   valueBucket->destroy(valueBucket);
   predicates->destroy(predicates);
   ```

   ```c
   // Delete data.
   OH_Predicates *predicates = OH_Rdb_CreatePredicates("EMPLOYEE");
   OH_VObject *valueObject = OH_Rdb_CreateValueObject();
   const char *name = "Lisa";
   valueObject->putText(valueObject, name);
   predicates->equalTo(predicates, "NAME", valueObject);
   int deleteRows = OH_Rdb_Delete(store_, predicates);
   valueObject->destroy(valueObject);
   predicates->destroy(predicates);
   ```

4. Query data based on the conditions specified by **Predicates**.

   Call **OH_Rdb_Query** to query data. The data obtained is returned in a **OH_Cursor** object.

   Example:

   ```c
   OH_Predicates *predicates = OH_Rdb_CreatePredicates("EMPLOYEE");

   const char *columnNames[] = {"NAME", "AGE"};
   int len = sizeof(columnNames) / sizeof(columnNames[0]);
   OH_Cursor *cursor = OH_Rdb_Query(store_, predicates, columnNames, len);

   int columnCount = 0;
   cursor->getColumnCount(cursor, &columnCount);

   // OH_Cursor is a cursor of a data set. By default, the cursor points to the -1st record. Valid data starts from 0.
   int64_t age;
   while (cursor->goToNextRow(cursor) == OH_Rdb_ErrCode::RDB_OK) {
       cursor->getInt64(cursor, 1, &age);
   }

   // Destroy the Predicates instance.
   predicates->destroy(predicates);
   // Destroy the result set.
   cursor->destroy(cursor);
   ```

5. Delete the database.

   Call **OH_Rdb_DeleteStore** to delete an RDB store and related database files.

   Example:

   ```c
   // Close the database instance.
   OH_Rdb_CloseStore(store_);
   // Delete the database file.
   OH_Rdb_DeleteStore(&config);
   ```
