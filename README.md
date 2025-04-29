# Library-Management-System
This is a simple library management system that allows you to add, delete, and manage books in a library using a variety of data structures, including a linked list, a hash map, a stack, and a priority queue.

Features
Add Book: Add a new book to the library with details like ID, title, author, and year of publication.

Display Books: Display all the books currently stored in the library.

Search Book by Title: Search for a book by its title. If found, it displays the book's details.

Delete Book by ID: Delete a book from the library by specifying its ID.

Undo Last Add: Undo the last book addition, effectively removing it from the library.

View Oldest Book: View the oldest book in the library based on its year of publication.

View Newest Book: View the newest book in the library based on its year of publication.

Data Structures Used
Linked List: Used to store books in a linear list.

Hash Map (unordered_map): Used for quick access to books by their title.

Stack: Used to store the books added to the library for undo functionality.

Priority Queue (Min-Heap): Used to keep track of the oldest and newest books based on their publication year.

Menu Options
The program presents the following options:

Add Book: Add a new book by providing the following details:

Book ID (integer)

Book Title (string)

Book Author (string)

Book Year of Publication (integer)

Display Books: Displays a list of all books in the library with their details.

Search Book by Title: Allows you to search for a book by its title. If the book is found, its details are displayed.

Delete Book by ID: Remove a book from the library by its unique ID.

Undo Last Add: Undo the last book added to the library (useful if you mistakenly add a book).

View Oldest Book: Displays the oldest book based on the year of publication.

View Newest Book: Displays the newest book based on the year of publication.

Exit: Exits the program.
