## Review of MYSQL - ADVANCED

### Syntax

* AS  

* LIMIT, OFFSET, FETCH  

* DECLARE, SET  

* FUNCTION <BEGIN, RETURN, END>   

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




