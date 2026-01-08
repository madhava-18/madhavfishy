1)<!DOCTYPE html>
<html>
<head>
<title>Simple Page</title>
</head>
<body>
<h1>My Web Page</h1>
<p>This is a simple web page. Click the buttons below:</p>
<!-- Buttons -->
<button onclick="changeFont()">Change Font</button>
<button onclick="changeColour()">Change Colour</button>
<script>
function changeFont() {
// Pick a random font
var fonts = ["Arial"
,
"Georgia"
"Courier New"
"Verdana"
,
,
,
"Tahoma"];
var randomFont = fonts[Math.floor(Math.random() * fonts.length)];
document.body.style.fontFamily = randomFont;
}
function changeColour() {
// Pick a random background/text color
var colours = [
{bg: "white"
, text: "black"},
{bg: "black"
, text: "white"},
{bg: "lightblue"
, text: "darkblue"},
{bg: "yellow"
, text: "darkred"},
{bg: "gray"
, text: "white"}
];
var random = colours[Math.floor(Math.random() * random.length)];
document.body.style.backgroundColor = random.bg;
document.body.style.color = random.text;
}
</script>
</body>
</html>
2)<!DOCTYPE html>
<html>
<head>
<title>Super Simple Form</title>
</head>
<body>
<h1>Details Form</h1>
<label>Name:</label>
<input type="text" id="nameInput"><br><br>
<label>Reg.No:</label>
<input type="number" id="regnoInput"><br><br>
<label>Dept:</label>
<select id="deptInput">
<option>CSE</option>
<option>ECE</option>
<option>EEE</option>
<option>Mech</option>
<option>Civil</option>
</select><br><br>
<button onclick="displayDetails()">Submit</button>
<div id="output"></div>
<script>
function displayDetails() {
// Get values from the inputs
var name = document.getElementById('nameInput').value;
var regno = document.getElementById('regnoInput').value;
var dept = document.getElementById('deptInput').value;
// Display the results
document.getElementById('output').innerHTML =
'<h2>Submitted:</h2>' +
'<p>Name: ' + name + '</p>' +
'<p>Reg.No: ' + regno + '</p>' +
'<p>Dept: ' + dept + '</p>';
}
</script>
</body>
</html>  
4)Notification manager
<!DOCTYPE html>
<html lang="en">
<head>
<title>Short Notifier</title>
<style>
/* Condensed CSS */
body { display: flex; justify-content: center; align-items: center; height: 100vh; font-family:
sans-serif; background-color: #f0f0f0; }
.container { display: flex; flex-direction: column; gap: 10px; padding: 2rem; background:
white; border-radius: 8px; }
input, button { font-size: 1.2rem; padding: 0.5rem; border-radius: 4px; border: 1px solid
#ccc; }
button { background-color: #007bff; color: white; cursor: pointer; border: none; }
</style>
</head>
<body>
<div class="container">
<input id="messageText" placeholder="Message">
<button id="notifyButton">Notify</button>
</div>
<script>
// Shortened JavaScript logic
document.getElementById('notifyButton').onclick = () => {
// Defines a function to create the notification
const fireNotification = () => {
let text = document.getElementById('messageText').value;
new Notification("New Notification", { body: text || "You have a new message!" });
};
// Checks permission and then fires the notification
if (Notification.permission === 'granted') {
fireNotification();
} else if (Notification.permission !== 'denied') {
Notification.requestPermission().then(permission => {
if (permission === 'granted') {
fireNotification();
}
});
}
};
</script>
</body>
</html>
5)shapes
<!DOCTYPE html>
<html>
<head>
<title>Shapes</title>
<style>
body {
text-align: center;
}
.shape-container {
width: 100px;
height: 100px;
margin: 20px;
border: 1px solid black;
display: inline-block;
}
.circle {
border-radius: 50%;
}
.square {
}
.triangle {
width: 0;
height: 0;
border-left: 50px solid transparent;
border-right: 50px solid transparent;
border-bottom: 100px solid blue;
}
</style>
</head>
<body>
<h1>Shapes</h1>
<div class="shape-container circle"></div>
<div class="shape-container square"></div>
<div class="shape-container triangle"></div>
</body>
</html>

6)GPS Location
<!DOCTYPE html>
<html lang="en">
<head>
<title>GPS Short</title>
<style>
/* Condensed CSS */
body { display: flex; justify-content: center; align-items: center; height: 100vh; font-family:
sans-serif; text-align: center; }
button { font-size: 1.2rem; padding: 0.8rem 1.5rem; cursor: pointer; border-radius: 5px;
border: none; background: #28a745; color: white; }
p { font-size: 1.1rem; margin-top: 1rem; }
</style>
</head>
<body>
<div>
<button onclick="getLocation()">Retrieve Location</button>
<p id="loc">Your location will be shown here.</p>
</div>
<script>
// Shortened JavaScript logic
function getLocation() {
const locElement = document.getElementById('loc');
// Define success and error handlers as arrow functions
const success = (pos) => {
const { latitude, longitude } = pos.coords;
locElement.innerHTML = `Latitude: ${latitude.toFixed(4)} <br> Longitude:
${longitude.toFixed(4)}`;
};
const error = (err) => {
const errorMessages = {
1: "Permission denied.",
2: "Position unavailable.",
3: "Request timed out."
};
locElement.textContent = errorMessages[err.code] || "An unknown error occurred.";
};
// Check for geolocation support and request the position
if ('geolocation' in navigator) {
navigator.geolocation.getCurrentPosition(success, error);
} else {
locElement.textContent = "Geolocation is not supported by your browser.";
}
}
</script>
</body>
</html>
7)Basic calculator
Basic Calculator
<!DOCTYPE html>
<html>
<head>
<title>Basic Calculator</title>
<style>
body {
font-family: Arial, sans-serif;
text-align: center;
}
input[type="text"] {
width: 150px;
padding: 10px;
margin: 5px;
}
input[type="button"] {
width: 50px;
padding: 10px;
margin: 5px;
}
</style>
</head>
<body>
<h1>Basic Calculator</h1>
<input type="text" id="result" readonly>
<br>
<input type="button" value="1" onclick="display('1')">
<input type="button" value="2" onclick="display('2')">
<input type="button" value="3" onclick="display('3')">
<input type="button" value="+" onclick="display('+')">
<br>
<input type="button" value="4" onclick="display('4')">
<input type="button" value="5" onclick="display('5')">
<input type="button" value="6" onclick="display('6')">
<input type="button" value="-" onclick="display('-')">
<br>
<input type="button" value="7" onclick="display('7')">
<input type="button" value="8" onclick="display('8')">
<input type="button" value="9" onclick="display('9')">
<input type="button" value="*" onclick="display('*')">
<br>
<input type="button" value="C" onclick="clearResult()">
<input type="button" value="0" onclick="display('0')">
<input type="button" value="=" onclick="calculate()">
<input type="button" value="/" onclick="display('/')">
<script>
function display(value) {
document.getElementById("result").value += value;
}
function clearResult() {
document.getElementById("result").value = "";
}
function calculate() {
let expression = document.getElementById("result").value;
let result = eval(expression);
document.getElementById("result").value = result;
}
</script>
</body>
</html>
8)message alert app
<!DOCTYPE html>
<html>
<head>
<title>Message Alert APP</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
<h2>Message Alert Application</h2>
<input type="text" id="messageInput" placeholder="Type a message here">
<button onclick="receive_message()">Send message</button>
<script>
function receive_message() {
var message = document.getElementById("messageInput").value;
if (message.trim() === "") {
alert("Please Enter a Message Before Sending");
} else {
alert("New message received: " + message);
document.getElementById("messageInput").value = "";
}
}
</script>
</body>
</html>
9)RSS FEED READER
<!DOCTYPE html>
<html>
<head>
<title>RSS Feed Reader</title>
<metaname="viewport"content="width=device-width=device width;initial-scale=1.0">
</head>
<body>
<h1>RSS Feed Reader</h1>
<ulid="feed"></ul>
<script src="https:||ajax.googleapis.coom/ajax/libs/jquery/3.6.01 jquerymin.js")
</script>
<script>$(document)ready(function)
{
$ajax
{
url:https:||feeds feed burner.com|Tech crunch||
Replace with your desired RSS feed URL
data Type:"xml"
success:function(xml){$(xml).find("item").each(function)
{
var title=$(this).find("title").text();
var link=$(this).find("link").text();
var discription=$(this).find("discription").text();
</script>
</body>
</html>
10)simple alarm
<!DOCTYPE html>
<html>
<head>
<title>Simple Alarm</title>
</head>
<body>
<h2>Simple Alarm Application</h2>
<label>Select Alarm Time: </label>
<input type="time" id="alarmTime">
<button onclick="setAlarm()">Set Alarm</button>
<p id="status"></p>
<script>
var alarmTime = null;
function setAlarm() {
alarmTime = document.getElementById("alarmTime").value;
document.getElementById("status").innerHTML = "Alarm set for " + alarmTime;
checkAlarm();
}
function checkAlarm() {
setInterval(function() {
var now = new Date();
var currentTime = now.getHours().toString().padStart(2,'0') + ":" +
now.getMinutes().toString().padStart(2,'0');
if (alarmTime === currentTime) {
alert("Alarm Ringing!");
}
}, 1000);
}
</script>
</body>
</html>
11)SEND EMAIL
<!DOCTYPE html>
<html>
<head>
<title>Send Email</title>
</head>
<body>
<h1>Send Email</h1>
<form>
<label for="email">To:</label><br>
<input type="email" id="email" name="email" required><br><br>
<label for="subject">Subject:</label><br>
<input type="text" id="subject" name="subject" required><br><br>
<label for="message">Message:</label><br>
<textarea id="message" name="message" rows="4" required></textarea><br><br>
<button type="submit">Send Email</button>
</form>
<script>
function submitForm() {
var toEmail = document.getElementById("email").value;
var subject = document.getElementById("subject").value;
var message = document.getElementById("message").value;
var mailtoUrl = "mailto:" + toEmail + "?subject=" + encodeURIComponent(subject) +
"&body=" + encodeURIComponent(message);
window.location.href = mailtoUrl;
}
document.querySelector('form').addEventListener('submit'
, function(event) {
event.preventDefault();
submitForm();
});
</script>
</body>
</html>



