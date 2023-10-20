window 객체는 웹 브라우저의 창(window)을 나타낸다.

window 객체는 브라우저에 의해 자동으로 생성된다.

[##_Image|kage@Baviq/btsyPBS3rzp/gFPnqPthNY49SnNHT6a7l1/img.png|CDM|1.3|{"originWidth":1294,"originHeight":868,"style":"alignCenter"}_##]

콘솔 창에 window라고 치면 window(현재 창) 정보가 쭉 나오는데 밑으로 쭉 더 있다.

window 객체를 이용해서

1.  브라우저의 창에 대한 정보를 알 수 있고, 이 창을 제어할 수 있다.
2.  또한 var 키워드로 변수를 선언하거나 함수를 선언하면 이 window 객체의 property가 된다.

> var a = 1; → window.a  

```
let outerHeight = window.outerHeight;
let innerHeight = window.innerHeight;

let outerWidth = window.outerWidth;
let innerWidth = window.innerWidth;

console.log(`outerHeight : ${outerHeight}`);
console.log(`outerWidth : ${outerWidth}`);
console.log(`innerHeight : ${innerHeight}`);
console.log(`innerWidth : ${innerWidth}`);

let scrollY = window.scrollY;
let scrollX = window.scrollX;

console.log(`scrollY : ${scrollY}`);
console.log(`scrollX : ${scrollX}`);

let windowLocation = window.location;   //해당 웹사이트의 주소

console.log(`windowLocation : ${windowLocation}`);

//window.location.href = '<http://google.com>';   //해당 주소로 이동

//window.history.go(1); //history 객체에는 사용자가 방문한 URL(브라우저 창에서)이 포함된다.

console.log(window.navigator);  //navigator - 브라우저에 대한 정보가 포함되어있다.
```

### outerHeight 와 innerHeight의 차이

[##_Image|kage@bKVngD/btsyLPdTYpR/3cEc9KCuwHdpaDOAkFLpC1/img.png|CDM|1.3|{"originWidth":639,"originHeight":376,"style":"alignCenter","caption":"출처 :&amp;nbsp;https://developer.mozilla.org/en-US/docs/Web/API/Window/outerHeight"}_##]

-   innerHeight - 안쪽 화면의 크기
-   outerHeight - 최상단부터 최하단까지의 화면의 크기
-   innerWidth - 좌측부터 우측까지 스크롤바를 제외한 화면의 크기
-   outerWidth - 최좌측부터 최우측까지 화면의 크기

### scrollY와 scrollX

-   scrollY - 상하 스크롤이 최상단부터 0으로 시작해 스크롤을 밑으로 내릴수록 증가
-   scrollX - 좌우 스크롤이 좌측부터 0으로 싲가해 스크롤을 우측으로 내릴수록 증가

### 그 외

-   window.location - 해당 웹 사이트의 주소(프로토콜 방식, 주소, 포트 등등)
-   window.location.href = ‘[http://www.xxxxx.com/](http://www.xxxxx.com/)[’](http://www.xxxxx.com/%E2%80%99) - 해당 주소로 이동
-   window.history - 사용자가 방문한 URL을 포함하여 앞 뒤로 사이트 이동
    -   window.history.back() - 이전 페이지로 이동
    -   window.history.forward() - 다음 페이지로 이동
    -   window.history.go(1) - 양수 입력 시 입력한 숫자만큼 다음 페이지로 이동 / 음수 입력시 이전 페이지로
-   window.navigator - 브라우저에 대한 정보가 담겨있다.window 객체는 웹 브라우저의 창(window)을 나타낸다..