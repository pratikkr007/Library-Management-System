#include <iostream>
#include <unordered_map>
#include <stack>
#include <queue>  // Include for priority queue
using namespace std;

class Book {
public:
    int id;
    string title, author;
    int year;

    Book(int i, string t, string a, int y) {
        id = i;
        title = t;
        author = a;
        year = y;
    }

    void display() {
        cout << "ID: " << id << ", Title: " << title
             << ", Author: " << author << ", Year: " << year << endl;
    }
};

// Node for Linked List
class Node {
public:
    Book* book;
    Node* next;

    Node(Book* b) {
        book = b;
        next = nullptr;
    }
};

// Comparator for Priority Queue (Min-Heap by Year)
class CompareYear {
public:
    bool operator()(Book* b1, Book* b2) {
        return b1->year > b2->year; // Min-Heap based on year (earliest year at top)
    }
};

class Library {
private:
    Node* head = nullptr;
    stack<Node*> undoStack;
    unordered_map<string, Book*> titleMap;
    priority_queue<Book*, vector<Book*>, CompareYear> yearQueue;  // Min-Heap

public:
    void addBook(int id, string title, string author, int year) {
        Book* newBook = new Book(id, title, author, year);
        Node* newNode = new Node(newBook);
        newNode->next = head;
        head = newNode;

        titleMap[title] = newBook;
        undoStack.push(newNode);
        yearQueue.push(newBook);  // Add the book to priority queue

        cout << "Book added.\n";
    }

    void displayBooks() {
        if (!head) {
            cout << "Library is empty.\n";
            return;
        }
        Node* curr = head;
        while (curr) {
            curr->book->display();
            curr = curr->next;
        }
    }

    void searchBookByTitle(string title) {
        if (titleMap.find(title) != titleMap.end()) {
            titleMap[title]->display();
        } else {
            cout << "Book not found.\n";
        }
    }

    void deleteBookById(int id) {
        Node* curr = head;
        Node* prev = nullptr;

        while (curr) {
            if (curr->book->id == id) {
                if (prev)
                    prev->next = curr->next;
                else
                    head = curr->next;

                titleMap.erase(curr->book->title);
                delete curr->book;
                delete curr;
                cout << "Book deleted.\n";
                return;
            }
            prev = curr;
            curr = curr->next;
        }
        cout << "Book with ID " << id << " not found.\n";
    }

    void undoLastAdd() {
        if (undoStack.empty()) {
            cout << "Nothing to undo.\n";
            return;
        }

        Node* toDelete = undoStack.top();
        undoStack.pop();

        // Remove from linked list
        if (toDelete == head) {
            head = head->next;
        } else {
            Node* curr = head;
            while (curr && curr->next != toDelete) {
                curr = curr->next;
            }
            if (curr)
                curr->next = toDelete->next;
        }

        // Remove from hash map
        titleMap.erase(toDelete->book->title);

        delete toDelete->book;
        delete toDelete;

        cout << "Last book addition undone.\n";
    }

    // New Feature: View the Oldest Book
    void viewOldestBook() {
        if (yearQueue.empty()) {
            cout << "No books in the library.\n";
            return;
        }
        Book* oldestBook = yearQueue.top();
        cout << "Oldest Book:\n";
        oldestBook->display();
    }

    // New Feature: View the Newest Book
    void viewNewestBook() {
        if (yearQueue.empty()) {
            cout << "No books in the library.\n";
            return;
        }

        // Extract all books, find the latest one
        Book* newestBook = nullptr;
        priority_queue<Book*, vector<Book*>, CompareYear> tempQueue = yearQueue;

        while (!tempQueue.empty()) {
            newestBook = tempQueue.top();
            tempQueue.pop();
        }

        cout << "Newest Book:\n";
        newestBook->display();
    }
};

int main() {
    Library lib;
    int choice;

    while (true) {
        cout << "\nLibrary Menu:\n";
        cout << "1. Add Book\n2. Display Books\n3. Search Book by Title\n4. Delete Book by ID\n5. Undo Last Add\n6. View Oldest Book\n7. View Newest Book\n8. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        if (choice == 1) {
            int id, year;
            string title, author;
            cout << "Enter Book ID: ";
            cin >> id;
            cin.ignore();
            cout << "Enter Title: ";
            getline(cin, title);
            cout << "Enter Author: ";
            getline(cin, author);
            cout << "Enter Year: ";
            cin >> year;
            lib.addBook(id, title, author, year);
        } else if (choice == 2) {
            lib.displayBooks();
        } else if (choice == 3) {
            string title;
            cin.ignore();
            cout << "Enter title to search: ";
            getline(cin, title);
            lib.searchBookByTitle(title);
        } else if (choice == 4) {
            int id;
            cout << "Enter Book ID to delete: ";
            cin >> id;
            lib.deleteBookById(id);
        } else if (choice == 5) {
            lib.undoLastAdd();
        } else if (choice == 6) {
            lib.viewOldestBook();
        } else if (choice == 7) {
            lib.viewNewestBook();
        } else if (choice == 8) {
            break;
        } else {
            cout << "Invalid choice.\n";
        }
    }

    return 0;
}
