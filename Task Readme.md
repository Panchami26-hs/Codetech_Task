How It Works

User enters name and email in the frontend form

Frontend sends data to backend using Fetch API

Backend receives and stores data

Success message is returned to frontend

Result

Successful data transfer from frontend to backend

REST API communication verified

Multi-cloud interoperability demonstrated
 
  Explanation in Short

This project demonstrates a multi-cloud setup where the frontend is hosted on Google Cloud and the backend API is hosted on AWS.
Both components communicate using REST APIs, showcasing seamless cross-cloud integration.
 Conclusion

This project highlights the flexibility and scalability of multi-cloud architectures and demonstrates real-world cloud interoperability using simple and effective tools.


Backend Code:
from flask import Flask, request, jsonify
from flask_cors import CORS

print(">>> FILE EXECUTED <<<")

app = Flask(__name__)
CORS(app)

data_store = []

@app.route("/")
def home():
    return "Flask is running"

@app.route('/add', methods=['POST'])
def add_data():
    data = request.json
    data_store.append(data)
    return jsonify({"message": "Data stored in AWS backend", "data": data})

@app.route('/get', methods=['GET'])
def get_data():
    return jsonify(data_store)

if __name__ == "__main__":
    print(">>> SERVER STARTING <<<")
    app.run(host="0.0.0.0", port=5000, debug=True)

Frontend Code:

<!DOCTYPE html>
<html>
<head>
  <title>Multi-Cloud Demo</title>
</head>
<body>
  <h2>GCP Frontend</h2>

  <input id="name" placeholder="Name"><br><br>
  <input id="email" placeholder="Email"><br><br>

  <button onclick="sendData()">Submit</button>

  <p id="result"></p>

  <script>
    function sendData() {
      fetch("http://localhost:5000/add", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          name: document.getElementById("name").value,
          email: document.getElementById("email").value
        })
      })
      .then(res => res.json())
      .then(data => {
        document.getElementById("result").innerText = data.message;
      })
      .catch(err => {
        console.error(err);
        document.getElementById("result").innerText = "Error connecting to backend";
      });
    }
  </script>
</body>
</html>


Screenshots:
<img width="890" height="573" alt="Screenshot 2025-12-30 162111" src="https://github.com/user-attachments/assets/d255b24d-d949-41b5-9c85-dd6221d21553" />

