
# Question
1.Problem Statement: Create a simple Library Management System where you manage a collection of books and allow users to search for a book based on various attributes.

Class Structure:
Book (Base Class):

Attributes: title (String), author (String), genre (String), and available (boolean).
Methods:
Constructor to initialize all attributes.
getDetails(): Returns a formatted string with book details in the format: "Title: [title], Author: [author], Genre: [genre], Available: [Yes/No]".
isAvailable(): Returns a boolean indicating if the book is available.
EBook (Derived Class):

Inherits Book and adds an fileSize attribute (in MB).
Override getDetails() to include fileSize in the details, in the format: "File Size: [fileSize] MB".
Encapsulate fileSize with getter and setter methods.
Library (Encapsulating Class):

Attributes: books (ArrayList<Book>), which holds a collection of Book and EBook objects.
Methods:
addBook(Book book): Adds a book to the library collection.
searchByTitle(String title): Searches for books by title using a case-insensitive comparison and returns the getDetails() of the matching book(s).
displayAllBooks(): Displays details of all books in the library.
Task Requirements:
Implement all classes with proper inheritance, encapsulation, and polymorphism.
Ensure encapsulation by using private access for all attributes and appropriate getter/setter methods.
Utilize polymorphism to handle getDetails() for both Book and EBook in a unified way when calling from the Library class.

```Java

// Base class: Book
class Book {
    private String title;
    private String author;
    private String genre;
    private boolean available;

    // Constructor
    public Book(String title, String author, String genre, boolean available) {
        this.title = title;
        this.author = author;
        this.genre = genre;
        this.available = available;
    }

    // Getter for title
    public String getTitle() {
        return title;
    }

    // Method to get book details
    public String getDetails() {
        return "Title: " + title + ", Author: " + author + ", Genre: " + genre + ", Available: " + (available ? "Yes" : "No");
    }

    // Method to check availability
    public boolean isAvailable() {
        return available;
    }
}

// Derived class: EBook
class EBook extends Book {
    private double fileSize; // in MB

    // Constructor
    public EBook(String title, String author, String genre, boolean available, double fileSize) {
        super(title, author, genre, available);
        this.fileSize = fileSize;
    }

    // Overridden method to include file size in details
    @Override
    public String getDetails() {
        return super.getDetails() + ", File Size: " + fileSize + " MB";
    }
}

// Encapsulating class: Library (Array-based implementation)
class Library {
    private Book[] books;
    private int bookCount;

    // Constructor to initialize the library with a fixed size
    public Library(int size) {
        books = new Book[size];
        bookCount = 0;
    }

    // Method to add a book to the library
    public void addBook(Book book) {
        if (bookCount < books.length) {
            books[bookCount] = book;
            bookCount++;
        } else {
            System.out.println("Library is full. Cannot add more books.");
        }
    }

    // Method to search for books by title
    public String searchByTitle(String title) {
        StringBuilder result = new StringBuilder();
        for (int i = 0; i < bookCount; i++) {
            if (books[i].getTitle().toLowerCase().contains(title.toLowerCase())) {
                result.append(books[i].getDetails()).append("\n");
            }
        }
        return result.length() > 0 ? result.toString() : "No books found with the title: " + title;
    }

    // Method to display all books in the library
    public void displayAllBooks() {
        for (int i = 0; i < bookCount; i++) {
            System.out.println(books[i].getDetails());
        }
    }
}

// Main class to run the program
public class LibraryManagementSystem {
    public static void main(String[] args) {
        Library library = new Library(10); // Create a library with capacity for 10 books

        Book book1 = new Book("Java Fundamentals", "John Doe", "Programming", true);
        EBook ebook1 = new EBook("Advanced Java", "Jane Smith", "Programming", true, 5.4);
        Book book2 = new Book("Data Structures", "Jim Beam", "Education", false);

        library.addBook(book1);
        library.addBook(ebook1);
        library.addBook(book2);

        // Search for books by title
        System.out.println("Search Result:");
        System.out.println(library.searchByTitle("java"));

        // Display all books
        System.out.println("\nAll Books:");
        library.displayAllBooks();
    }
}
