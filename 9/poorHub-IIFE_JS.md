/*
```js
*/

(function(){
  // ==================== CSS 注入 ====================
  const style = document.createElement('style');
  style.textContent = `
    :root {
      --bgColor: #869cff;
      --txtColor: #ffffff;
      --borderColor: #cccccc;
    }
    body { font-family: sans-serif; margin: 0; }
    .sec_btn {
      position: fixed; right: 20px; bottom: 20px;
      background: var(--bgColor); color: var(--txtColor);
      border: none; border-radius: 4px; padding: 10px 16px;
      cursor: pointer;
      -webkit-tap-highlight-color: transparent;
    }
    .sec_btn:hover { background: #6279e7; }
    .selectWrapper {
      position: fixed; right: 20px; bottom: 60px;
      min-width: 220px; max-width: 300px;
      background: #fff; border: 1px solid var(--borderColor); border-radius: 4px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.2);
      opacity: 0; pointer-events: none;
      transition: opacity 0.2s; overflow: hidden;
    }
    .scrollContainer {
      display: flex; width: 100%; overflow-x: hidden;
      scroll-behavior: smooth;
    }
    .multiSelect {
      flex: 0 0 100%;
      box-sizing: border-box; background: #fff;
    }
    .multiSelect div {
      padding: 8px 12px;
      cursor: pointer;
      -webkit-tap-highlight-color: transparent;
    }
    .multiSelect div:hover { background: #f0f0f0; }
    .bottomBorder { border-bottom: 1px solid var(--borderColor); }
    .topBorder { border-top: 1px solid var(--borderColor); }
    .iconDiv {
      display: flex; justify-content: space-between; align-items: center;
    }
  `;
  document.head.appendChild(style);

  // ==================== 按钮 ====================
  const button = document.createElement('button');
  button.className = 'sec_btn';
  button.innerText = 'Add to feature vector';
  button.onclick = toggleMenu;
  button.addEventListener('touchend', (e) => { e.preventDefault(); toggleMenu(); }); // 移动端
  document.body.appendChild(button);

  // ==================== 菜单容器 ====================
  const wrapper = document.createElement('div');
  wrapper.className = 'selectWrapper';
  wrapper.id = 'menuWrapper';
  const scrollContainer = document.createElement('div');
  scrollContainer.className = 'scrollContainer';
  scrollContainer.id = 'scrollContainer';
  wrapper.appendChild(scrollContainer);
  document.body.appendChild(wrapper);

  // ==================== 菜单数据 ====================
  const menus = [
    [
      { type: 'text', text: 'New feature vector', class: 'bottomBorder' },
      { type: 'item', text: 'Vector_01' },
      { type: 'item', text: 'myVector' },
      { type: 'item', text: 'featureVector' },
      { type: 'nav', text: 'Other projects', target: 1 }
    ],
    [
      { type: 'text', text: 'Search', class: 'bottomBorder' },
      { type: 'nav', text: 'Project Example', target: 2 },
      { type: 'nav', text: 'David’s project', target: 2 },
      { type: 'nav', text: 'Project Idan', target: 2 },
      { type: 'nav', text: 'Manhattan', target: 2 },
      { type: 'back', text: '◀ Back', target: 0 }
    ],
    [
      { type: 'text', text: 'Project Idan', class: 'bottomBorder' },
      { type: 'item', text: 'Idan Vector' },
      { type: 'item', text: 'Testings' },
      { type: 'item', text: 'Features_120' },
      { type: 'item', text: 'Aggregators' },
      { type: 'back', text: '◀ Back', target: 1 }
    ]
  ];

  // ==================== 生成菜单 ====================
  menus.forEach((menuItems, index) => {
    const menuDiv = document.createElement('div');
    menuDiv.className = 'multiSelect';
    menuDiv.id = `menu-${index}`;

    menuItems.forEach(item => {
      const div = document.createElement('div');
      div.innerText = item.text;
      if (item.class) div.classList.add(...item.class.split(' '));
      // 点击与触摸绑定
      if (item.type === 'item') {
        div.onclick = () => selectItem(item.text);
        div.addEventListener('touchend', (e)=>{ e.preventDefault(); selectItem(item.text); });
      } else if (item.type === 'nav') {
        div.classList.add('iconDiv', 'topBorder');
        div.onclick = () => goToMenu(item.target);
        div.addEventListener('touchend', (e)=>{ e.preventDefault(); goToMenu(item.target); });
      } else if (item.type === 'back') {
        div.classList.add('topBorder');
        div.onclick = () => goToMenu(item.target);
        div.addEventListener('touchend', (e)=>{ e.preventDefault(); goToMenu(item.target); });
      }
      menuDiv.appendChild(div);
    });

    scrollContainer.appendChild(menuDiv);
  });

  // ==================== 功能函数 ====================
  function toggleMenu() {
    if (wrapper.style.opacity === '1') {
      wrapper.style.opacity = '0';
      wrapper.style.pointerEvents = 'none';
      goToMenu(0);
    } else {
      wrapper.style.opacity = '1';
      wrapper.style.pointerEvents = 'all';
    }
  }
  function goToMenu(index) {
  // 确保显示
  wrapper.style.opacity = '1';
  wrapper.style.pointerEvents = 'all';
  // 取容器实际宽度
  const width = scrollContainer.getBoundingClientRect().width;
  scrollContainer.scrollLeft = width * index;
  }
  function selectItem(name) {
    alert(`Selected: ${name}`);
    toggleMenu();
  }

  document.addEventListener('click', (e) => {
    if (!wrapper.contains(e.target) && e.target !== button) {
      wrapper.style.opacity = '0';
      wrapper.style.pointerEvents = 'none';
      goToMenu(0);
    }
  });
})();

/*
```
*/