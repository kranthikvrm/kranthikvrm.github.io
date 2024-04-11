---
title: Certifications
layout: page 
icon: fas fa-window-maximize
order: 6
---
<style>

.certification-container {
  display: flex;
  justify-content: space-around;
}

.card {
  width: 200px;
  border: 2px solid #ccc;
  border-radius: 10px;
  text-align: center;
  margin: 10px;
  background: #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.card-image {
  border-radius: 10px 10px 0 0;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  margin-bottom: 20px;
}

.card-image.blue { background-color: #007bff; }
.card-image.red { background-color: #dc3545; }
.card-image.green { background-color: #28a745; }

.card-title {
  font-size: 18px;
  color: #333;
  margin-bottom: 20px;
}

.card-button {
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  outline: none;
  margin-bottom: 20px;
}

.card-button:hover {
  background-color: #d32f2f;
}

</style>
<div class="certification-container">
  <div class="card">
    <div class="card-image blue">
      <!-- Image goes here -->
      <h2>CEH</h2>
    </div>
    <p class="card-title">Certified Ethical Hacker</p>
    <button class="card-button">Click me</button>
  </div>
  <div class="card">
    <div class="card-image red">
      <!-- Image goes here -->
      <h2>CEH MASTER</h2>
    </div>
    <p class="card-title">Certified Ethical Hacker Master</p>
    <button class="card-button">Click me</button>
  </div>
  <div class="card">
    <div class="card-image green">
      <!-- Image goes here -->
      <h2>WAHS</h2>
    </div>
    <p class="card-title">Web App Sec Professional</p>
    <button class="card-button">Click me</button>
  </div>
</div>

