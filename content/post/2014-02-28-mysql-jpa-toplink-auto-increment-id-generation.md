+++
title = "MySql JPA toplink Auto increment id generation."
slug = "2014-02-28-mysql-jpa-toplink-auto-increment-id-generation"
published = 2014-02-28T02:30:00.002000-08:00
author = "Pandurang Patil"
tags = [ "jpa", "mysql", "ORM", "Java"]
+++
To configure `JPA` entity to make use of `auto increment` feature of `MySql` for primary key generation you can make use of `IDENTITY` strategy ref below code.

```
    @Entity 
    public class Customer { 

        @Id 
        @GeneratedValue(strategy=GenerationType.IDENTITY) 
        private long id;
            .
            .
            .
        public long getId() {
            return id;
        }
    }
```

But problem with this way of generating ids with `MySql` and `JPA` combination is when you persist new entity and try to retrieve `id` assigned to newly persisted entity using `getId()` method. You get `0` value, because newly generated `id` for the record is not set with managed entity for that you need to flush after persisting the entity.

If you don't specify strategy with `GeneratedValue` annotation, default value will be `GenerationType.AUTO`. `AUTO` strategy means your are asking `JPA` to select appropriate strategy. In most of the cases it is `TABLE` strategy.

```
    @Entity 
    public class Customer { 

        @Id 
        @GeneratedValue
        private long id;
            .
            .
            .
        public long getId() {
            return id;
        }
    }
```

One can make use of `TABLE` strategy directly, this way you have more control over configurations.

```
    @Entity 
    public class Customer { 

        @Id
        @GeneratedValue(generator = "idgen")
        @TableGenerator(name = "idgen", table = "ID_GEN", pkColumnName = "ID_NAME", valueColumnName = "ID_VAL", pkColumnValue = "CUST_SEQ", allocationSize = 1, initialValue = 0)
        private long id;
            .
            .
            .
        public long getId() {
            return id;
        }
    }
```
  
