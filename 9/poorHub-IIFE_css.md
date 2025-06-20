/*
```css
*/

:root {
  --bgColor: #869cff;
  --txtColor: #ffffff;
  --borderColor: #cccccc;
}
body {
  font-family: sans-serif;
  margin: 0;
}
.sec_btn {
  position: fixed;
  right: 20px;
  bottom: 20px;
  background: var(--bgColor);
  color: var(--txtColor);
  border: none;
  border-radius: 4px;
  padding: 10px 16px;
  cursor: pointer;
}
.sec_btn:hover {
  background: #6279e7;
}
.selectWrapper {
  position: fixed;
  right: 20px;
  bottom: 60px;
  min-width: 220px;
  max-width: 300px;
  background: #fff;
  border: 1px solid var(--borderColor);
  border-radius: 4px;
  box-shadow: 0 6px 20px rgba(0,0,0,0.2);
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.2s;
  overflow: hidden;
}
.scrollContainer {
  display: flex;
  width: 100%;
  overflow-x: hidden;
  scroll-behavior: smooth;
}
.multiSelect {
  flex: 0 0 100%;
  box-sizing: border-box;
  background: #fff;
}
.multiSelect div {
  padding: 8px 12px;
  cursor: pointer;
}
.multiSelect div:hover {
  background: #f0f0f0;
}
.bottomBorder { border-bottom: 1px solid var(--borderColor); }
.topBorder { border-top: 1px solid var(--borderColor); }
.iconDiv {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/*
```
*/