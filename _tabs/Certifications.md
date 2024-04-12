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
  width: 250px;
  height: 250px;
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

.card-image.blue { background-color: #fff8e4; }
.card-image.red { background-color: #d8eaf5; }
.card-image.green { background-color: #d1ffdc; }

.card-title {
  font-size: 18px;
  color: #333;
  margin-bottom: 20px;
}

.card-button {
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 9px;
  padding: 7px 8px;
  font-size: 16px;
  cursor: pointer;
  outline: none;
  margin-bottom: 20px;
  align-self: center;
}

.card-button:hover {
  background-color: #d32f2f;
}
img-style {
    max-width: 100%;
    height: 150px;
    transition: all .35s ease-in-out;
}
</style>
<div class="certification-container">
  <div class="card">
    <div class="card-image blue">
      <img class="img-style" src="../images/comptia_security.png" alt="Comptia Security+">
    </div>
   <button class="card-button" onclick="window.open('https://www.credly.com/badges/3b4e1349-6760-4a3e-8635-b5aa177fb2ba','_blank');">Verify here</button>
  </div>
  <div class="card">
    <div class="card-image red">
      <img class="img-style" src="../images/aws_cloud.png" alt="AWS Cloud Practitioner">
    </div>
   
    <button class="card-button" onclick="window.open('https://www.credly.com/badges/f0f11634-5abb-405c-8588-40b361ee4d81/linked_in_profile','_blank');">Verify here</button>
  </div>
  <div class="card">
    <div class="card-image green">
      <img class="img-style" src="../images/CEH.png" alt="Certified Ethical Hacker">
    </div>
   
    <button class="card-button">In Progress</button>
  </div>
</div>

