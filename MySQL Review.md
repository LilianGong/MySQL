## Review of MYSQL - ADVANCED

### Syntax

* AS  

* LIMIT, OFFSET, FETCH  

* DELETE  
the syntax for delete is exactly the same as SELECT.  
        
        DELETE p1.*
        FROM Person p1,
            Person p2
        WHERE
            p1.Email = p2.Email AND p1.Id > p2.Id

* DECLARE, UPDATE, SET 

        UPDATE [TABLE] SET [COLUMN] = [VALUE]  
        
* IF   

        IF(condition, value_if_true, value_if_false)
        
* CASE    
used to select specific case and give value   

        CASE WHEN condition THEN value_if_true ELSE value_if_false END   


* LIKE, REGEXP_LIKE  

    string pattern matching    

        SELECT mail 
        FROM Emails 
        WHERE 
        REGEXP_LIKE(mail, '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode.com$')  




* RANK, DENSE_RANK    

          DENSE_RANK() OVER (
            PARTITION BY <expression>[{,<expression>...}]
            ORDER BY <expression> [ASC|DESC], [{,<expression>...}]
        ) 
        
        e.g. 
            SELECT 
            DENSE_RANK() OVER(
            PARTITION BY DepartmentId 
            ORDER BY Salary DESC) as Dense
            FROM Employee
      
     
* LEFT JOIN, RIGHT JOIN, INNER JOIN, OUTER JOIN  
ON condition can represent a WHERE clause  

        SELECT w1.id FROM Weather AS w1 
        INNER JOIN 
        Weather AS w2
        ON
        DATEDIFF (w1.recordDate, w2.recordDate) = 1
        AND 
        w1.temperature > w2.temperature

* LEAD, LAG   
lead - look forward; lag - look backward  
lead & lag has the same expression.  

            LEAD(<expression>[,offset[, default_value]]) OVER (  
                PARTITION BY (expr)  
                ORDER BY (expr) )  

            e.g.  
            
            SELECT Num, 
                   LEAD(Num) OVER(ORDER BY Id)
                   From Numbers 



* COUNT 
can be used simply as 

        COUNT([])
        
      OR: 
      
        COUNT([]) OVER (
        PARTITION BY [] 
        ORDER BY []
        )


* COUNT(IF), COUNT(DISTINCT)

         SELECT class
         FROM courses c2
         GROUP BY class
         HAVING COUNT(DISTINCT(student))>=5

* ROW_NUMBER   
return the row number of specific partition and group  

        ROW_NUMBER () OVER(
        PARTITION BY []
        ORDER BY [])  

* DELETE  
can be combined with JOIN and achieve removing duplicates

        DELETE p1 FROM 
        Person p1
        INNER JOIN Person p2
        WHERE 
        p1.Id > p2.Id
        AND 
        p1.Email = p2.Email 

* ROUND, CAST, MOD, CEILING, FLOOR



* DATEDIFF 
            
            DATEDIFF ("2018-01-01","2018-01-02") = -1 
            DATEDIFF ("2018-01-02","2018-01-01") = 1


* FUNCTION <BEGIN, RETURN, END>   

### Techniques

* Multiple Database Instances  
This technique can be used by creating multiple parallel logs, thus create a way of indexing.      
            
            SELECT DISTINCT l1.Num
            FROM 
            LOGS l1,
            LOGS l2
            WHERE l1.Id = l2.Id -1 
            AND l1.Num = l2.Num

* Nested SELECT   
Sometimes we can select from a pre-selected table, but remember in MYSQL the pre-selected table should have an alias.  
Here is an example of selecting duplicated emails in the table:  

        SELECT Email 
        FROM 
        (SELECT Email, COUNT(Email) as ct
        FROM Person
        GROUP BY Email) AS grouped
        WHERE ct > 1


### Complecated cases
Calculate the cancellation rate by date from unbanned users   

        SELECT Request_at AS Day, 
        ROUND((COUNT(`Id`) - COUNT(IF(`Status` = 'completed', 1, NULL)))/COUNT(`Id`),2)
        AS "Cancellation Rate"
        FROM 
            (SELECT Id, `Status`, Request_at FROM 
                (SELECT *
                FROM 
                Trips as t1
                INNER JOIN 
                Users as u1
                ON 
                u1.Users_Id = t1.Client_Id
                AND 
                U1.Banned = "No") AS c1
            INNER JOIN 
            Users as u2
            ON 
            u2.Users_Id = c1.Driver_Id
            AND 
            u2.Banned = "No") AS merged
        GROUP BY  Request_at
        HAVING
        Request_at >="2013-10-01" 
        AND 
        Request_at <="2013-10-03" 

