# 인스타그램 클론코딩
클론코딩 강의를 통해서 하는 것이 아닌 직접 찾아보고 하는 프로젝트임을 밝힙니다.

---

## 프로젝트를 하는 이유
거의 이제 막 웹 개발을 시작했다고 볼 수 있는 상황에서 요즘 많이 보이는 웹 개발 관련 강의를 하나 들었지만, 강의의 부족함을 많이 느꼈다. 특히 깊이감이 없는 강의의 내용과 단순히 따라하는 식의 코딩 방법은 대학교 1,2학년 시기에 내가 스스로 하던 코딩 방식과 달라 마음에 들지 않았고, 프로그래밍 언어의 원리에 대한 이해도 없어 수박 겉핥기의 느낌이었다. 그래서 책을 따로 사서 공부를 하고 원래 나의 방식대로 코딩을 하고 싶어 이 프로젝트를 시작한다.

---

## 프로젝트 준비
- 이미지 : 크롬 확장프로그램을 이용해 인스타그램 아이콘을 받았고, 웹 제작과정에서 이미지 스프라이트 기법을 활용할 예정이다.
- 개발 언어 
  - 프론트엔드 
    - `HTML/CSS`는 기본으로 사용하고, `SCSS`나 `BOOTSTRAP`은 고민을 해볼 것이며, 가능하다면 수정할 의향이 있다.
    - `JS`는 바닐라 자바스크립트로 코딩할 예정이다.`VUE`나 `REACT`는 방식을 몰라 보류한다.
  - 백엔드
    - `NODE.JS`를 이용할 것이다. 현재 서버 개발 경험이 없고, 아직 노드를 공부하는 중이어서 먼저 프론트엔드 틀을 잡고 리팩토링과 함께 이어나갈 것이다.
    - 데이터베이스는 MySQL을 이용할 생각이지만 이는 바뀔 여지가 있다.
- 개발 방식 : 21.08.05 기준으로 생각하고 있는 것은 메인 페이지 개발을 먼저 한 이후 추가 기능(메시지, 탐색, 이전활동, 프로필확인 등)을 구현할 생각이다. 만약 메인 페이지 개발을 하면서 서버연동이 함께 되지 않는 경우 추가 기능을 먼저 개발할 수 있다.
- 기능 : CRUD를 중점으로 하고, 시간이 된다면 세부적인 기능을 함께 넣을 예정이다.
- 예상되는 점
  - 기간 : 21.08.05기준 ~1년
  - 순서 : HTML/CSS - JS - NODE.JS
  - 갈아엎을 시기 : 처음 JS로 구현 후 서버연동 시 크게 엎을 것으로 예상되나, 내 생각에 서버로 연동할 때 필요할 수 있는 것을 고려하며 JS를 잡을 것이다. 이는 전적으로 내 생각에만 의존할 것이라 갈아엎을 확률이 높다. 물론 구글링을 통해 알아볼 것이다.
- 참고 자료 : `(도서)` 모던 자바스크립트 DEEP DIVE, `(도서)` NODE.JS 교과서 개정2판, `(도서)` 리팩터링 2판
---
# HTML / CSS

## 1. 메인페이지
메인 페이지는 크게 해더, 콘텐츠, 네비게이션, 모달창으로 나누었다.<br>
헤더의 경우 메시지, 탐색 페이지에서도 사용할 예정이다.(js를 이용할 것이다.)<br>
각 태그의 내부에 컨테이너를 두어 뷰 크기를 잡았고, 반응형을 고려할 예정이다. 
<br>
메인 페이지에서 해더와 네비게이션의 경우 고정되어 있고, 콘텐츠만 무한 스크롤이 되도록 할 예정이다. 작업 시 콘텐츠의 경우 임의의 게시물을 만들 것이고 그 틀을 이용해서 추후에 js를 이용해 넘겨받는 식으로 구성할 것이다.

해더
```html
<header id="header"></header>
<section class="content-body">
   <section class="content-body__content">content-body__content</section>
   <nav id="nav" class="content-body__nav">navigation</nav>
</section>
```
``` css
#header{
  width: 100%;
  position: fixed;
  top: 0;
  border-bottom: 1px solid #e3e3e3;
  background-color: #fff;
  z-index: 1;
}
```
- 해더는 고정되어야 하고, 스크롤 시 뒤로 콘텐츠가 들어가야 한다. 이는 배경색을 지정하고, `z-index`를 높여주면 된다. 일단 1로 했고 필요시 더 높은 수를 줄 것이다.
컨테이너
```css
.container{
  max-width: 955px;
  margin: 0 auto;
}
```

아이콘(해더)
```css
/* 실패한 방법 */
#header .search_text::before{
  content: "";
  display: inline-block;
  width: 14px;
  height: 14px;
  margin: -1px;
  background: url("/images/icons1.png") -23px 0 
  no-repeat;
  margin-right: 10px;
}
/* 다음으로 시도한 방법 */
#header .search_icon{
  display: inline-block;
  color: #aaa;
  font-size: 14px;
  margin-right: 5px;
}
#header .search_icon-cancel{
  display: none;
  color: #bbb;
  position: absolute;
  top: 16px;
  right: 5px;
  font-size: 16px;
}
```
- 아이콘의 경우 이미지 스프라이트를 사용하려 했지만, 현재 아이콘의 위치를 정확히 알 수 없어 실패했다. 대체할 방법은 google material icon을 이용하는 방법 혹은 미리 받은 이미지를 사용하는 방법이 있다. <strong>전자의 경우 html 태그가 늘어난다는 단점이 생긴다.</strong><strong>후자의 경우 이미지 파일을 모두 가지고 있어야 해 비효율적일 것이라 생각한다.</strong>그래서 구글 아이콘 웹폰트를 사용하기로 했다. 구글 아이콘의 경우 npm으로 설치해서 하는 방법도 있는 것 같지만 이번에는 웹폰트를 사용한다. npm으로 따로 알아볼 것이다.
- 구글 웹 폰트를 이용해 아이콘을 다룰 때 같은 종류의 아이콘이 배경이 있거나 테두리만 있는 경우가 거의 없어 선택되기 전의 상태와 선택된 후의 상태를 색으로 구분했다. 이때 선택된 경우 `class = "view"`를 추가했다.
- 이전활동과 프로필의 경우 모달창으로 띄울 예정이기에 링크를 걸지 않았다.

## 2. 모달창
이전활동, 프로필, 검색 기능의 경우 모달창을 띄워야 하므로 모든 페이지에 모달창을 포함한다.
```css
/* MODAL */
#header .modal::before{
  content: "";
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: block;
  width: 100vw;
  height: 100vh;
  opacity: .6;
}
.modal{
  display: none;
  position:absolute;
  border: 1px solid #e5e5e5;
  border-radius: 6px;
  top: 36px;
  box-sizing: border-box;
  z-index: 10;
  background-color: #fff;
}
.modal.view{
  display: block;
}
```
- 모달창이 떴을 때 뒤에 페이지는 기능을 하지 못한다. 즉 클릭을 할 수 없는 상태이므로 모달창의 배경을 화면 전체페이지로 하고 `position: fixed;`로 띄운다.
- 모달의 경우 특정 아이콘이나 버튼 등을 눌렀을 때 보여야 하므로 기본적으로 `display: none;`을 두고, 보여야 할 것은 클래스에 view를 추가하여 보이게 한다.(js 이용)