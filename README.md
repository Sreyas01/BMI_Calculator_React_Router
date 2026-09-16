# Ex06 BMI Calculator

## NAME: M.SREYAS
## REG NO: 212224040323

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM

## app.jsx

```
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
import { useState } from "react";
import "./App.css";

function Home() {
  return (
    <div className="container">
      <h1>BMI Calculator</h1>
      <p>Calculate your Body Mass Index easily and quickly.</p>

      <Link to="/bmi">
        <button>Start Calculator</button>
      </Link>
    </div>
  );
}

function BMI() {
  const [height, setHeight] = useState("");
  const [weight, setWeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [category, setCategory] = useState("");
  const [error, setError] = useState("");

  const calculateBMI = (e) => {
    e.preventDefault();

    if (height <= 0 || weight <= 0 || height === "" || weight === "") {
      setError("Please enter valid height and weight.");
      return;
    }

    const heightInMeter = height / 100;
    const result = weight / (heightInMeter * heightInMeter);

    setBmi(result.toFixed(2));
    setError("");

    if (result < 18.5) {
      setCategory("Underweight");
    } else if (result < 25) {
      setCategory("Normal");
    } else if (result < 30) {
      setCategory("Overweight");
    } else {
      setCategory("Obese");
    }
  };

  return (
    <div className="container">
      <h1>BMI Calculator</h1>

      <form onSubmit={calculateBMI}>
        <label>Height (cm)</label>
        <input
          type="number"
          placeholder="Enter height"
          value={height}
          onChange={(e) => setHeight(e.target.value)}
        />

        <label>Weight (kg)</label>
        <input
          type="number"
          placeholder="Enter weight"
          value={weight}
          onChange={(e) => setWeight(e.target.value)}
        />

        {error && <p className="error">{error}</p>}

        <button type="submit">Calculate BMI</button>
      </form>

      {bmi && (
        <div className="result">
          <h2>Your BMI: {bmi}</h2>
          <h3>Category: {category}</h3>

          <Link to="/result">
            <button>View Result</button>
          </Link>
        </div>
      )}

      <Link to="/">← Back to Home</Link>
    </div>
  );
}

function Result() {
  return (
    <div className="container">
      <h1>BMI Result</h1>
      <p>Your BMI calculation has been completed successfully.</p>

      <div className="categories">
        <p>Underweight: Below 18.5</p>
        <p>Normal: 18.5 - 24.9</p>
        <p>Overweight: 25 - 29.9</p>
        <p>Obese: 30 and above</p>
      </div>

      <Link to="/bmi">
        <button>Calculate Again</button>
      </Link>
    </div>
  );
}

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/bmi" element={<BMI />} />
        <Route path="/result" element={<Result />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;

```

## app.css
```
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f2f5f9;
  color: #222;
}

.container {
  width: 90%;
  max-width: 500px;
  margin: 80px auto;
  padding: 40px;
  background: white;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

h1 {
  margin-bottom: 15px;
  color: #1f2937;
}

p {
  color: #555;
}

form {
  display: flex;
  flex-direction: column;
  text-align: left;
  margin-top: 25px;
}

label {
  margin-top: 15px;
  margin-bottom: 7px;
  font-weight: bold;
}

input {
  padding: 13px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 16px;
}

button {
  margin-top: 20px;
  padding: 13px 20px;
  border: none;
  border-radius: 8px;
  background: #2563eb;
  color: white;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

button:hover {
  background: #1d4ed8;
}

.error {
  color: red;
  margin-top: 12px;
}

.result {
  margin-top: 30px;
  padding: 20px;
  background: #f0f7ff;
  border-radius: 12px;
}

.result h2 {
  color: #2563eb;
}

.categories {
  margin: 25px 0;
  padding: 15px;
  background: #f8fafc;
  border-radius: 10px;
}

a {
  display: inline-block;
  margin-top: 20px;
  color: #2563eb;
  text-decoration: none;
  font-weight: bold;
}

@media (max-width: 600px) {
  .container {
    width: 90%;
    margin: 40px auto;
    padding: 25px;
  }

  h1 {
    font-size: 28px;
  }

  input,
  button {
    width: 100%;
  }
}
```

## main.jsx
```
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

## index.css

```
body {
  margin: 0;
}
```

## OUTPUT
<img width="1322" height="596" alt="Screenshot 2026-09-13 011439" src="https://github.com/user-attachments/assets/0410c416-f917-4088-a247-cca00aeb4ca1" />
<img width="1327" height="560" alt="image" src="https://github.com/user-attachments/assets/0e660dc0-ec5b-48e0-a769-6730cd4d50a4" />


## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
