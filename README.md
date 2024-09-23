mkdir nodejs-tasks
cd nodejs-tasks
npm init -y

npm install generate-password nodemailer

// hello-world.js
console.log("HELLO WORLD");


// server.js
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/html');
  res.end('<h1>Hello Node!!!!</h1>\n');
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});


// file-system.js
const fs = require('fs');

// Write to 'welcome.txt'
fs.writeFile('welcome.txt', 'Hello Node', (err) => {
  if (err) throw err;
  console.log('File has been written.');

  // Read from 'welcome.txt'
  fs.readFile('welcome.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log('Content of welcome.txt:', data);
  });
});

// password-generator.js
const generatePassword = require('generate-password');

function createPassword() {
  const password = generatePassword.generate({
    length: 12,
    numbers: true,
  });
  console.log('Generated Password: ', password);
}

createPassword();

// email-sender.js
const nodemailer = require('nodemailer');

// Set up the transporter
let transporter = nodemailer.createTransport({
  service: 'gmail',
  auth: {
    user: 'your-email@gmail.com',  // Replace with your Gmail email
    pass: 'your-email-password'    // Replace with your Gmail password
  }
});

// Email details
let mailOptions = {
  from: 'your-email@gmail.com',    // Your email
  to: 'recipient-email@gmail.com', // Recipient email
  subject: 'Hello from Node.js',
  text: 'This is a test email sent from a Node.js app.'
};

// Send the email
transporter.sendMail(mailOptions, (error, info) => {
  if (error) {
    return console.log(error);
  }
  console.log('Email sent: ' + info.response);
});
