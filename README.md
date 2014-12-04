#SQL Lab


##Getting Started

To get started we'll need to import the booktown.sql file.

1. open terminal
2. use the command `psql -f booktown.sql`
3. type `sql` to open your psql console
4. type \list to ensure the booktown database was successfully completed

##Instructions
Provide the follow sql statements below each question.

##Order
1. Find all subjects sorted by subject

	```
	SELECT subject FROM subjects;
	```
	
2. Find all subjects sorted by location

	```
	SELECT location FROM subjects;
	```

##Where
1. Find the book "Little Women"

	```
	SELECT * FROM books WHERE title = 'Little Women';
	```
	
2. Find all books containing the word "Python"

	```
	SELECT * FROM books WHERE title ILIKE '%python%';
	```

3. Find all subjects with the location "Main St" sort them by subject

	```	
	SELECT subject FROM subjects WHERE location ILIKE '%main st%';
	```

##Joins

1. Find all books about Computers list ONLY book title

	```
	
	solution 1:
	
	SELECT books.title FROM books INNER JOIN subjects ON books.subject_id = subjects.id WHERE subject = 'Computers';
	
	or 
	
	solution 2 (short version):
	
	SELECT b.title FROM books b INNER JOIN subjects s ON b.subject_id = s.id WHERE subject = 'Computers';
	```
	
* Find all books and display ONLY
	* Book title
	* Author's first name
	* Author's last name
	* Book subject
	
	```
	SELECT books.title, authors.first_name, authors.last_name, subjects.subject FROM books INNER JOIN authors ON books.author_id = authors.id INNER JOIN subjects ON books.subject_id = subjects.id;
	```

* Find all books that are listed in the stock table
	* Sort them by retail price (most expensive first)
	* Display ONLY: title and price

	```
	SELECT books.title, stock.retail FROM books INNER JOIN editions ON books.id = book_id INNER JOIN stock ON stock.isbn = editions.isbn ORDER BY retail DESC;
	```

* Find the book "Dune" and display ONLY
	* Book title
	* ISBN number
	* Publisher name
	* Retail price

	```
SELECT books.title, editions.isbn, publishers.name, stock.retail FROM books INNER JOIN editions ON books.id = editions.book_id INNER JOIN stock ON stock.isbn = editions.isbn INNER JOIN publishers ON publishers.id = editions.publisher_id WHERE books.title = 'Dune' ORDER BY retail DESC;
	```

* Find all shipments sorted by ship date display ONLY:
	* Customer first name
	* Customer last name
	* ship date
	* book title

	```
	SELECT books.title, shipments.ship_date, customers.first_name, customers.last_name FROM books INNER JOIN editions ON books.id = editions.book_id INNER JOIN shipments ON editions.isbn = shipments.isbn INNER JOIN customers ON shipments.customer_id = customers.id ORDER BY ship_date ASC;
	```
	
* Find all books that have either a 2nd or 3rd edition associated to it display ONLY:
	* Book title
	* Book Author
	* Edition Number
	
	```
	solution 1:
	
	SELECT books.title, authors.first_name, authors.last_name, editions.edition FROM books INNER JOIN authors ON books.author_id = authors.id INNER JOIN editions ON books.id = editions.book_id WHERE edition IN (2, 3);
	
	or 
	
	solution 2:
	
	SELECT books.title, authors.first_name, authors.last_name, editions.edition FROM books INNER JOIN authors ON books.author_id = authors.id INNER JOIN editions ON books.id = editions.book_id WHERE edition = 2 OR edition = 3;
	
	
	```
