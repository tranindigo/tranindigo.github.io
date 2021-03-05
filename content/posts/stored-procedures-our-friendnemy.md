---
title: "Stored Procedures: Our Friendnemy in SQL"
date: "2021-03-04"
categories: 
  - "sql"
tags: 
  - "sql-injection"
  - "stored-procedure"
---

A stored procedure is a SQL script that can be stored on the database server and called many times. Stored procedures have been falling out of favor for many years, in favor of Object-Relational-Mappers (ORM) like Hibernate, Entity Framework, and ActiveRecord. However, there are times when it makes sense to use them as part of your development process, such as working with legacy systems or with multiple systems that rely on the same database.

Stored procedures are great for calculations, data manipulation, and reporting data in the database. If your app has a feature to generate a report, it must query a database (preferably a mirror database). And it is often easier and faster to encapsulate that logic inside a stored procedure than it is to use an ORM to abstract that logic. Furthermore, it is often speedier to write a stored procedure to speed up data reporting because executing raw SQL is quicker than going through an ORM.

On the flip side, when you have business logic inside the database layer, it makes your code harder to maintain overall because it goes against the architectural pattern that you have inside of your application.

When working with stored procedures, the business layer may be relegated to the database due to the nature of stored procedures. This can make stored procedures harder to maintain since there are fewer tools to debug them. When you have hundreds of stored procedures spread across dozens of databases in a microservice architecture, this can make them a nightmare to debug and cost you and your team valuable time.

From a security perspective, stored procedures can be a powerful bulwark against SQL injection attacks. A parameterized query is the most secure against SQL injection attacks. However, care must be taken to prevent these attacks from happening in the stored procedure. Consider the following SQL script:

```sql
CREATE PROCEDURE spSearchToys
   @toyname VARCHAR(200)
AS
   EXEC('SELECT * FROM [dbo].[Toys] WHERE Name LIKE '%' + @toyname + '%'')
RETURN

```

In the above example, if @toyname contains a malicious string then a bad actor can potentially do lasting damage to your database system. For instance, if @toyname contains the string `*%'; DROP TABLE Toys; --`, then the user can potentially delete all of your data because the resulting query is:

```sql
SELECT * FROM Toys WHERE Name LIKE '%*'; DROP TABLE Toys; --;
```

The `--` makes the rest of your line comments, so the bad actor will likely be able to delete your table in this scenario!

The simple fix for this is to use parameterized queries within a stored procedure:

```sql
CREATE PROCEDURE spSearchToys
    @toyname varchar(200) = NULL AS
BEGIN
    SELECT * FROM [dbo].[Toys] WHERE Name LIKE @toyname;
END
```

So, stored procedures have upsides and downsides. They are useful in a variety of enterprise settings. Sometimes it's impossible to avoid working with them because they are essential to the business itself. I hope that this article provides some clarity so that you can learn to work with them, just as I have!
