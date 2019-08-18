---


---

<blockquote>
<h2 id="mysql-basic">MySQL Basic</h2>
</blockquote>
<ul>
<li>
<p>mysql -u root -p --&gt; enter password 
<p>or <p>mysql -u root -p --&gt; enter password --&gt; in mac
<em>get access to the sql server</em> <br></p>
</li>
<li>
<p>exit / quit <em>exit the sql server</em> <br></p>
</li>
<li>
<p>create database my_database <em>create database</em> <br></p>
</li>
<li>
<p>drop database my_database <em>delete database</em> <br></p>
</li>
<li>
<p>CREATE TABLE Ages ( <br>
  name VARCHAR(128), <br>
  age INTEGER <br>
)EIGINE = InnoDB; <br> 
<em>creat new tables </em> <br></p>
</li>
<li>
<p>INSERT INTO Ages (name, age) VALUES ('Zahra', 34); <em>create new rows in the table</em> <br></p>
</li>
<li>
<p>DELETE FROM Album WHERE album_id = 2; <em>delete rows from table</em> <br></p>
</li>
<li>
<p>SELECT Track.title, Artist.name, Album.title, Genre.name FROM Track JOIN Genre JOIN Album JOIN Artist ON Track.genre_id = Genre.genre_id AND Track.album_id = Album.album_id AND Album.artist_id = Artist.artist_id; <em>how to join the relational tables</em> <br></p>
</li>

</ul>

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNTI1NDI4NjIsMTI4Nzc4NDU2NiwyMT
A0OTYyNDAzLC04NzEyODQzODQsMTg3NjY2MzcxOV19
-->