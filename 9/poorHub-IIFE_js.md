/*
```js
*/

(function(){
  // 创建按钮
  const button = document.createElement('button');
  button.className = 'sec_btn';
  button.innerText = 'Add to feature vector';
  button.onclick = toggleMenu;
  document.body.appendChild(button);

  // 创建菜单容器
  const wrapper = document.createElement('div');
  wrapper.className = 'selectWrapper';
  wrapper.id = 'menuWrapper';

  // 创建滚动容器
  const scrollContainer = document.createElement('div');
  scrollContainer.className = 'scrollContainer';
  scrollContainer.id = 'scrollContainer';
  wrapper.appendChild(scrollContainer);

  document.body.appendChild(wrapper);

  // 定义菜单数据
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

  // 生成菜单层
  menus.forEach((menuItems, index) => {
    const menuDiv = document.createElement('div');
    menuDiv.className = 'multiSelect';
    menuDiv.id = `menu-${index}`;
    menuItems.forEach(item => {
      const div = document.createElement('div');
      div.innerText = item.text;
      if (item.class) div.className = item.class;
      if (item.type === 'item') {
        div.onclick = () => selectItem(item.text);
      } else if (item.type === 'nav') {
        div.className = (div.className ? div.className + ' ' : '') + 'iconDiv topBorder';
        div.onclick = () => goToMenu(item.target);
      } else if (item.type === 'back') {
        div.className = (div.className ? div.className + ' ' : '') + 'topBorder';
        div.onclick = () => goToMenu(item.target);
      }
      menuDiv.appendChild(div);
    });
    scrollContainer.appendChild(menuDiv);
  });

  // 切换菜单
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
    const width = scrollContainer.clientWidth;
    scrollContainer.scrollTo({
      left: width * index,
      behavior: 'smooth'
    });
  }

  function selectItem(name) {
    alert(`Selected: ${name}`);
    toggleMenu();
  }

  // 点击外部关闭菜单
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