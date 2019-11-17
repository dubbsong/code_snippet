#### 01

```js
const allBtn = document.querySelectorAll('.tab-button');
const allContent = document.querySelectorAll('.tab-content');

// When click 1st btn
allBtn[0].addEventListener('click', function() {
  allBtn[1].classList.remove('orange');
  allBtn[2].classList.remove('orange');
  allBtn[0].classList.add('orange');
  allContent[1].classList.remove('show');
  allContent[2].classList.remove('show');
  allContent[0].classList.add('show');
});

// When click 2nd btn
allBtn[1].addEventListener('click', function() {
  allBtn[0].classList.remove('orange');
  allBtn[2].classList.remove('orange');
  allBtn[1].classList.add('orange');
  allContent[0].classList.remove('show');
  allContent[2].classList.remove('show');
  allContent[1].classList.add('show');
});

// When click 3rd btn
allBtn[2].addEventListener('click', function() {
  allBtn[0].classList.remove('orange');
  allBtn[1].classList.remove('orange');
  allBtn[2].classList.add('orange');
  allContent[0].classList.remove('show');
  allContent[1].classList.remove('show');
  allContent[2].classList.add('show');
});
```

<br>

#### 02

```js
for (let i = 0; i < 3; i++) {
  allBtn[i].addEventListener('click', function() {
    allBtn[0].classList.remove('orange');
    allBtn[1].classList.remove('orange');
    allBtn[2].classList.remove('orange');
    allBtn[i].classList.add('orange');
    allContent[0].classList.remove('show');
    allContent[1].classList.remove('show');
    allContent[2].classList.remove('show');
    allContent[i].classList.add('show');
  });
}
```

