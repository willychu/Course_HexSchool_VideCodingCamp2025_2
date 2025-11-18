# Vibe Coding 課程作業

作業說明：https://discord.com/channels/801807326054055996/1428276906691792988/1440144478559010889

# Prompt（使用 GPT-5.1 Thinking）

以下是使用簡單的 HTML、CSS、JavaScript，幫名字叫做「妙麗」的寵物狗做一個年齡計算機，主要能計算並顯示： 
- 他狗的年齡是幾歲 
- 換算人類的年齡是幾歲

請嘗試幫我美化妙麗年齡計算機，並且我希望重新整理畫面後，也能出現上次運算結果（請使用 localstorage 語法）。

## HTML

```
<div class="container">
  <h1>🐶 妙麗歲數計算機</h1>

  <div>
    <label for="birthDate">狗狗的出生日期：</label>
    <!-- 可預填妙麗的生日，使用者也可以自行修改 -->
    <input type="date" id="birthDate" value="2023-02-28">
  </div>

  <button id="calcBtn">開始計算</button>

  <div id="result" class="result"></div>
</div>
```

## CSS

```
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  background-color: #f5f5f5;
  margin: 0;
  padding: 20px;
}

.container {
  max-width: 420px;
  margin: 40px auto;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.06);
  padding: 20px 24px 24px;
}

h1 {
  font-size: 20px;
  margin: 0 0 16px;
  display: flex;
  align-items: center;
  gap: 6px;
}

label {
  display: block;
  font-size: 14px;
  margin-bottom: 6px;
}

input[type="date"] {
  width: 100%;
  padding: 8px 10px;
  font-size: 14px;
  border-radius: 6px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

button {
  margin-top: 14px;
  padding: 8px 14px;
  font-size: 14px;
  border-radius: 6px;
  border: 1px solid #1976d2;
  background-color: #1976d2;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #145ca5;
  border-color: #145ca5;
}

.result {
  margin-top: 18px;
  font-size: 14px;
  line-height: 1.6;
}
```

## JavaScript

```
function calculateAges() {
  var birthInput = document.getElementById("birthDate").value;
  var resultEl = document.getElementById("result");

  if (!birthInput) {
    resultEl.textContent = "請先選擇妙麗的出生日期～";
    return;
  }

  var birthDate = new Date(birthInput);
  var today = new Date();

  if (birthDate > today) {
    resultEl.textContent = "出生日期不能晚於今天唷！";
    return;
  }

  // 計算妙麗實際狗年齡（以年為單位）
  var diffMs = today - birthDate;
  var dogAge = diffMs / (1000 * 60 * 60 * 24 * 365.25); // 以 365.25 天當一年

  if (dogAge <= 0) {
    resultEl.textContent = "妙麗還太小啦，暫時無法計算。";
    return;
  }

  // 最新公式：human_age = 16 * ln(dog_age) + 31
  var humanAge = 16 * Math.log(dogAge) + 31;

  // 顯示到一位小數
  var dogAgeDisplay = dogAge.toFixed(1);
  var humanAgeDisplay = humanAge.toFixed(1);

  resultEl.innerHTML =
    '妙麗現在大約 <strong>' + dogAgeDisplay +
    '</strong> 歲狗年齡，<br>換算成人類年齡大約是 <strong>' +
    humanAgeDisplay + '</strong> 歲。';
}

document.getElementById("calcBtn").addEventListener("click", calculateAges);
```