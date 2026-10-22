# 💰 Interest Calculator

## 📌 About the Project

The Interest Calculator is a responsive web application developed using HTML, CSS, and JavaScript. It helps users calculate different types of interest, estimate loan repayments, and manage their calculation history.

## ✨ Features

- Calculate Simple Interest.
- Calculate Compound Interest.
- Estimate Savings Account and Fixed Deposit interest.
- Calculate Loan EMI and total repayment.
- Estimate Credit Card interest.
- View and manage calculation history.
- Automatically delete history records older than 30 days.
- Store calculation history using IndexedDB.
- Responsive design for mobile and desktop devices.

## 🛠️ Technologies Used

- **HTML5** – Structures the webpage.
- **CSS3** – Provides styling and responsive layout.
- **JavaScript** – Performs calculations and manages user interactions.
- **IndexedDB** – Stores calculation history in the browser.

## 🧮 Formulas Used

**1. Simple Interest**

SI = (P × R × T) / 100

**2. Compound Interest**

A = P(1 + R / 100n)^(nT)

CI = A − P

**3. Loan EMI**

The EMI is calculated using the standard loan repayment formula based on the principal, monthly interest rate, and number of monthly payments.

Where:

- P = Principal amount
- R = Annual interest rate
- T = Time in years
- n = Compounding frequency per year
- A = Total amount

## 🚀 How to Run the Project

1. Download or clone the project repository.
2. Save the code in a file named `index.html`.
3. Open `index.html` in a modern web browser.
4. Select an interest type.
5. Enter the amount, annual interest rate, and duration.
6. Click **Calculate Now** to view the result.
7. Open **History** to view or delete saved calculations.

## 📂 Project Structure

Interest-Calculator/
│
├── index.html
└── README.md

The HTML file contains the HTML structure, CSS styling, and JavaScript functionality.

## 💾 Data Storage

The application uses IndexedDB to store calculation records in the user's browser. Records older than 30 days are automatically deleted when the application initializes or the history is opened.

## ⚠️ Disclaimer

This application provides estimates for educational purposes. Actual bank interest, loan EMIs, fixed deposit returns, and credit card charges may differ depending on financial institution rules, fees, taxes, payment schedules, and applicable terms.

## 👨‍💻 Author

Developed as a beginner-friendly web development project to practice HTML, CSS, JavaScript, and browser-based data storage.

## 📄 License

This project is available for educational and personal learning purposes.
