## **POSTGRESQL, JDBC, & JAVA DATA TYPES**  
  
| PostgreSQL Data Type | SQL/JDBC Data Type | Java Type                  |
| -------------------- | ------------------ | -------------------------- |
| bool                 | BIT                | boolean                    |
| bit                  | BIT                | boolean                    |
| int8                 | BIGINT             | long                       |
| bigserial            | BIGINT             | long                       |
| oid                  | BIGINT             | long                       |
| bytea                | BINARY             | byte[]                     |
| char                 | CHAR               | String                     |
| bpchar               | CHAR               | String                     |
| numeric              | NUMERIC            | java.math.BigDecimal       |
| int4                 | INTEGER            | int                        |
| serial               | INTEGER            | int                        |
| int2                 | SMALLINT           | short                      |
| smallserial          | SMALLINT           | short                      |
| float4               | REAL               | float                      |
| float8               | DOUBLE             | double                     |
| money                | DOUBLE             | double                     |
| name                 | VARCHAR            | String                     |
| text                 | VARCHAR            | String                     |
| varchar              | VARCHAR            | String                     |
| date                 | DATE               | java.sql.Date              |
| time                 | TIME               | java.sql.Time              |
| timetz               | TIME               | java.sql.Time              |
| timestamp            | TIMESTAMP          | java.sql.Timestamp         |
| timestamptz          | TIMESTAMP          | java.sql.Timestamp         |
| cardinal_number      | DISTINCT           | Mapping of underlying type |
| character_data       | DISTINCT           | Mapping of underlying type |
| sql_identifier       | DISTINCT           | Mapping of underlying type |
| time_stamp           | DISTINCT           | Mapping of underlying type |
| yes_or_no            | DISTINCT           | Mapping of underlying type |
| xml                  | SQLXML             | java.sql.SQLXML            |
| refcursor            | REF_CURSOR         | Undefined                  |
| _abc                 | ARRAY              | java.sql.array             |