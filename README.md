<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Book API Interaction</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      margin: 0;
      padding: 0;
    }
    header {
      background: #333;
      color: white;
      padding: 1rem;
      text-align: center;
    }
    .container {
      width: 90%;
      max-width: 1200px;
      margin: 2rem auto;
    }
    .book-form {
      background: white;
      padding: 1.5rem;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      margin-bottom: 2rem;
    }
    .book-form input, .book-form button {
      padding: 0.5rem;
      margin: 0.5rem 0;
      width: 100%;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    .book-form button {
      background: #333;
      color: white;
      cursor: pointer;
    }
    .book-list {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.5rem;
    }
    .book-card {
      background: white;
      padding: 1rem;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      text-align: center;
    }
    .book-card img {
      max-width: 100%;
      border-radius: 6px;
      height: 160px;
      object-fit: cover;
    }
    .book-card h3 {
      margin: 0.8rem 0 0.4rem;
      font-size: 1.1rem;
    }
    .book-card p {
      font-size: 0.9rem;
      color: #555;
    }
    .book-card button {
      margin-top: 0.5rem;
      padding: 0.4rem 0.8rem;
      border: none;
      background: #c0392b;
      color: white;
      border-radius: 4px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <header>
    <h1>📚 Book API Interaction</h1>
  </header>

  <div class="container">
    <!-- Add Book Form -->
    <div class="book-form">
      <h2>Add a New Book</h2>
      <input type="text" id="title" placeholder="Book Title" />
      <input type="text" id="author" placeholder="Author" />
      <input type="text" id="image" placeholder="Image URL (leave empty for default)" />
      <button onclick="addBook()">Add Book</button>
    </div>

    <!-- Book List -->
    <div class="book-list" id="bookList"></div>
  </div>

  <script>
    let books = [
      { id: 1, title: "The Great Gatsby", author: "F. Scott Fitzgerald", image: "https://images.unsplash.com/photo-1544936207-3b1b76c9a7c3?auto=format&fit=crop&w=400&q=80" },
      { id: 2, title: "1984", author: "George Orwell", image: "https://images.unsplash.com/photo-1512820790803-83ca734da794?auto=format&fit=crop&w=400&q=80" },
      { id: 3, title: "To Kill a Mockingbird", author: "Harper Lee", image: "https://images.unsplash.com/photo-1495446815901-a7297e633e8d?auto=format&fit=crop&w=400&q=80" }
    ];

    function renderBooks() {
      const bookList = document.getElementById("bookList");
      bookList.innerHTML = "";
      books.forEach(book => {
        bookList.innerHTML += `
          <div class="book-card">
            <img src="${book.image}" alt="${book.title}" />
            <h3>${book.title}</h3>
            <p>${book.author}</p>
            <button onclick="deleteBook(${book.id})">Delete</button>
          </div>
        `;
      });
    }

    function addBook() {
      const title = document.getElementById("title").value;
      const author = document.getElementById("author").value;
      const image = document.getElementById("image").value || "https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?auto=format&fit=crop&w=400&q=80";
      
      if (title && author) {
        const newBook = {
          id: Date.now(),
          title,
          author,
          image
        };
        books.push(newBook);
        renderBooks();
      }
    }

    function deleteBook(id) {
      books = books.filter(book => book.id !== id);
      renderBooks();
    }

    renderBooks();
  </script>
</body>
</html>
