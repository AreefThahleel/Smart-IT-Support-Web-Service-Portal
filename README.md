<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Smart IT Support Web Service Portal</title>
  <style>
    * { box-sizing: border-box; font-family: Arial, sans-serif; }
    body { margin: 0; background: #f4f6f8; }
    header { background: #0f172a; color: #fff; padding: 16px; }
    header h1 { margin: 0; }
    nav { display: flex; gap: 15px; margin-top: 10px; }
    nav button { background: #1e293b; color: #fff; border: none; padding: 8px 14px; cursor: pointer; border-radius: 6px; }
    nav button:hover { background: #334155; }
    .container { padding: 20px; }
    .card { background: #fff; padding: 20px; border-radius: 10px; box-shadow: 0 4px 10px rgba(0,0,0,0.05); margin-bottom: 20px; }
    h2 { margin-top: 0; }
    input, select, textarea { width: 100%; padding: 10px; margin: 8px 0; border-radius: 6px; border: 1px solid #ccc; }
    button.primary { background: #2563eb; color: #fff; border: none; padding: 10px 16px; border-radius: 6px; cursor: pointer; }
    button.primary:hover { background: #1d4ed8; }
    table { width: 100%; border-collapse: collapse; }
    th, td { padding: 10px; border-bottom: 1px solid #ddd; text-align: left; }
    th { background: #f1f5f9; }
    .hidden { display: none; }
    footer { text-align: center; padding: 15px; font-size: 14px; color: #555; }
  </style>
</head>
<body>
  <header>
    <h1>Smart IT Support Web Service Portal</h1>
    <p>Simple IT ticketing & service management system</p>
    <nav>
      <button onclick="showSection('dashboard')">Dashboard</button>
      <button onclick="showSection('newTicket')">New Ticket</button>
      <button onclick="showSection('tickets')">All Tickets</button>
      <button onclick="showSection('about')">About</button>
    </nav>
  </header>

  <div class="container">
    <div id="dashboard" class="card">
      <h2>Dashboard</h2>
      <p>Welcome to the Smart IT Support Web Service Portal. This system allows users to submit IT issues, track status, and manage support requests efficiently.</p>
      <ul>
        <li>Create IT support tickets</li>
        <li>Track issue status</li>
        <li>View all submitted requests</li>
      </ul>
    </div>

    <div id="newTicket" class="card hidden">
      <h2>Create New Ticket</h2>
      <input type="text" id="name" placeholder="Your Name" />
      <input type="email" id="email" placeholder="Your Email" />
      <select id="category">
        <option value="">Select Issue Category</option>
        <option>Network Issue</option>
        <option>Hardware Issue</option>
        <option>Software Issue</option>
        <option>Account / Access Issue</option>
      </select>
      <textarea id="description" placeholder="Describe the issue"></textarea>
      <button class="primary" onclick="submitTicket()">Submit Ticket</button>
    </div>

    <div id="tickets" class="card hidden">
      <h2>All Tickets</h2>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Category</th>
            <th>Description</th>
            <th>Status</th>
          </tr>
        </thead>
        <tbody id="ticketTable"></tbody>
      </table>
    </div>

    <div id="about" class="card hidden">
      <h2>About This Project</h2>
      <p>This project is built as a portfolio-ready IT support system to demonstrate skills in:</p>
      <ul>
        <li>HTML, CSS, JavaScript</li>
        <li>Basic system design</li>
        <li>Problem-solving & UI design</li>
      </ul>
      <p>Designed for students, fresh graduates, and junior IT roles.</p>
    </div>
  </div>

  <footer>
    © 2026 Smart IT Support Web Service Portal | Built by Areef Thahleel
  </footer>

  <script>
    let tickets = [];
    let ticketId = 1;

    function showSection(sectionId) {
      document.querySelectorAll('.card').forEach(card => card.classList.add('hidden'));
      document.getElementById(sectionId).classList.remove('hidden');
    }

    function submitTicket() {
      const name = document.getElementById('name').value;
      const email = document.getElementById('email').value;
      const category = document.getElementById('category').value;
      const description = document.getElementById('description').value;

      if (!name || !email || !category || !description) {
        alert('Please fill all fields');
        return;
      }

      tickets.push({
        id: ticketId++,
        name,
        category,
        description,
        status: 'Open'
      });

      document.getElementById('name').value = '';
      document.getElementById('email').value = '';
      document.getElementById('category').value = '';
      document.getElementById('description').value = '';

      renderTickets();
      showSection('tickets');
    }

    function renderTickets() {
      const table = document.getElementById('ticketTable');
      table.innerHTML = '';
      tickets.forEach(t => {
        const row = `<tr>
          <td>${t.id}</td>
          <td>${t.name}</td>
          <td>${t.category}</td>
          <td>${t.description}</td>
          <td>${t.status}</td>
        </tr>`;
        table.innerHTML += row;
      });
    }
  </script>
</body>
</html>
