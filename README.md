# This is a JavaScript project about typing test

<img width="1128" alt="WeChat Image_20191026153945" src="https://user-images.githubusercontent.com/49086087/67625047-f840cf80-f806-11e9-8b71-22c690ad28d9.png">
<img width="1128" alt="WeChat Image_20191026154000" src="https://user-images.githubusercontent.com/49086087/67625048-f840cf80-f806-11e9-82b2-88116425766b.png">
<img width="1128" alt="WeChat Image_20191026154004" src="https://user-images.githubusercontent.com/49086087/67625049-f840cf80-f806-11e9-9776-465d27d304c7.png">
<img width="1128" alt="WeChat Image_20191026154008" src="https://user-images.githubusercontent.com/49086087/67625050-f840cf80-f806-11e9-80bb-f0341063f581.png">

```javascript
const testWrapper = document.querySelector(".test-wrapper");
const testArea = document.querySelector("#test-area");
const originText = document.querySelector("#origin-text p").innerHTML;
const resetButton = document.querySelector("#reset");
const theTimer = document.querySelector(".timer");

var timer = [0,0,0,0];
var interval;
var timerRunning = false;

// Add leading zero to numbers 9 or below (purely for aesthetics):
function leadingZero(time) {
	if (time <= 9) {
		time = "0" + time;
	}
	return time;
}

// Run a standard minute/second/hundredths timer:
function runTimer() {
	let currentTime = leadingZero(timer[0]) + ":" + leadingZero(timer[1]) + ":" + leadingZero(timer[2]);
	theTimer.innerHTML = currentTime;
	timer[3]++;

	timer[0] = Math.floor((timer[3]/100)/60);
	timer[1] = Math.floor((timer[3]/100) - (timer[0] * 60));
	timer[2] = Math.floor(timer[3] - (timer[1] * 100) - (timer[0] * 6000));
}

// Match the text entered with the provided text on the page:
function spellCheck() {
	let textEntered = testArea.value;
	let originTextMatch = originText.substring(0,textEntered.length);

	if (textEntered == originText) {
		clearInterval(interval);
		testWrapper.style.borderColor = "#429890";
	} else {
		if (textEntered == originTextMatch) {
			testWrapper.style.borderColor = "#65CCf3";
		} else {
			testWrapper.style.borderColor = "#E95D0F";
		}
	}

}

// Start the timer:
function start() {
	let textEnterdLength = testArea.value.length;
	if (textEnterdLength === 0 && !timerRunning) {
		timerRunning = true;
		interval = setInterval(runTimer, 10);
	}

}

// Reset everything:
function reset() {
	clearInterval(interval);
	interval = null;
	timer = [0,0,0,0];
	timerRunning = false;

	testArea.value = "";
	theTimer.innerHTML = "00:00:00";
	testWrapper.style.borderColor = "grey";
}

// Event listeners for keyboard input and the reset
testArea.addEventListener("keypress", start, false);
testArea.addEventListener("keyup", spellCheck);
resetButton.addEventListener("click", reset, false);
```