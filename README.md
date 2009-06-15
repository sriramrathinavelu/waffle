Waffle is a Python library for storing data in a schema-less, document oriented way using a relational database

Similar designs:
    
 * CouchDB: http://couchdb.apache.org/
 * FriendFeed: http://bret.appspot.com/entry/how-friendfeed-uses-mysql

Advantages:
 * Easy sharding
 * Indices can be created and populated online
 * Indices can be created on separate databases
 * Index values can be customizedon the client side (for example, MySQL only lets you customize the prefix)
 * Works with any database SQLAlchemy supports (SQLite, MySQL, PostgreSQL, Oracle)

Disadvantages:
 - Your records are stored in an opaque format the server cannot inspect.  This can jeopardize platform neutrality and maintainability.  For example if you choose to use encode your object data with Pickle (Python's main serialization format), you probably won't be able to access your data from other languages without first exporting it to another format.  
 - Along the same lines, your record data will no longer be directly queryable with your SQL client
 - Because the record data is opaque to the server, table-scan queries will executed on the client instead of the server.  This will likely be much slower than a table scan on the server side since there will be additional latency costs for marshalling the data over the network and filtering it on the client side
 - Indices are eventually consistent but not atomically consistent.

Requirements So Far
 * Python
 * SQLAlchemy (0.5.x but 0.4.x will probably work fine)
 * Kindred spirit