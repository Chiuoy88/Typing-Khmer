// អត្ថបទខ្មែរ​ច្រើន
const texts = [
  "ការអប់រំគឺជាគ្រឹះសម្រាប់ការអភិវឌ្ឍសង្គម និងអនាគតប្រទេសជាតិ។",
  "ការអានសៀវភៅជួយបង្កើនចំណេះដឹង និងការគិតវិភាគ។",
  "បច្ចេកវិទ្យាជួយអោយជីវិតកាន់តែងាយស្រួល និងលឿនជាងមុន។",
  "ការអនុវត្តជាបន្តបន្ទាប់គឺជាគន្លឹះនៃភាពជោគជ័យ។",
  "សុខភាពល្អគឺជាទ្រព្យសម្បត្តិដ៏មានតម្លៃបំផុត។"
];

// DOM
const testTextElement = document.getElementById("testText");
const inputText = document.getElementById("inputText");
const timeDisplay = document.getElementById("time");
const speedDisplay = document.getElementById("speed");

let timeLeft = 60;
let timer = null;
let start = false;

// ជ្រើសអត្ថបទ random
function loadRandomText() {
  const randomIndex = Math.floor(Math.random() * texts.length);
  testTextElement.innerText = texts[randomIndex];
}

// ចាប់ផ្តើមដោយ random ម្តង
loadRandomText();

inputText.addEventListener("input", () => {
  if (!start) {
    start = true;
    timer = setInterval(countDown, 1000);
  }

  const typedLength = inputText.value.length;
  const timeSpent = 60 - timeLeft;

  if (timeSpent > 0) {
    const cpm = Math.round((typedLength / timeSpent) * 60);
    speedDisplay.innerText = cpm;
  }
});

function countDown() {
  timeLeft--;
  timeDisplay.innerText = timeLeft;

  if (timeLeft <= 0) {
    clearInterval(timer);
    inputText.disabled = true;
  }
}

function restartTest() {
  clearInterval(timer);
  timeLeft = 60;
  start = false;
  inputText.value = "";
  inputText.disabled = false;
  timeDisplay.innerText = 60;
  speedDisplay.innerText = 0;

  // random អត្ថបទថ្មី
  loadRandomText();
}
