# todolist
토이 프로젝트<br>
👉🏻 바닐라 자바스크립트로 TO DO LIST 만들기

## ✨ 개요
#### 설명
> 바닐라 자바스크립트로 투 두 리스트 구현하기<br>

저번 momentum 클론 코딩 이후 투 두 리스트에 아쉬움이 남아 이틀동안 개발하게 되었다.
#### 완성된 화면
<img width="1791" alt="스크린샷 2022-02-08 오후 11 16 13" src="https://user-images.githubusercontent.com/80568332/153004882-dfb4f4a4-a70b-494a-9593-0b8fc0ec6f07.png">

#### 개발 기간
2022.02.07~02.08 총 2일<br>
#### 사용 언어
Html, CSS, JavaScript<br>
#### 기록 날짜
- 1차 : 2022.02.09

## ✨ 사용 방법
1. https://soyoung2022.github.io/todolist/ 에 접속한다.
2. 할일을 적으세요 라고 적혀있는 칸에 자신의 할 일을 적고 엔터를 누른다.
  ex) 토플 공부하기
3. 만약 할 일을 적는 과정 중에 삭제하고 싶은 항목이 있다면 해당 항목 오른쪽에 있는 X 버튼을 누른다.
4. 끝마친 일에는 항목 왼쪽에 있는 동그란 버튼을 누른다.
5. 만약 작성한 할 일을 모두 삭제하고 싶다면 "Delete All" 버튼을 누른다.
6. 만약 모든 항목들을 끝마쳤으면 "Select All" 버튼을 누른다.
7. 할 일이 몇 개 남았는지 알고 싶다면 하단에 Left를 보면 된다.
<img width="1095" alt="스크린샷 2022-02-08 오후 11 20 55" src="https://user-images.githubusercontent.com/80568332/153005749-f8f237a6-1776-4787-b35a-f6071aa96005.png">

## ✨ 개발 과정 기록
### 📍 index.html
#### 구상
화면 구상은 아이패드에 직접 어느 위치에 어떤 기능을 추가할 것인지 그려보고 태그들을 가지 형태로 그려나갔다.

### 📍 style.css
#### display
flex-direction: row, column, justify-content: center, space-between이 자주 사용되었다.

### 📍 todo.js
아래 기능 순서대로 코드를 작성해나갔다.
#### 기능1. 할 일 작성하기
- form, input:text 태그를 이용했다.
- required로 빈 한 일을 받아오지 못하게 했다.
- sumbit 이벤트가 발생할 때 원래는 브라우저가 새로고침되는데, 그것을 막기 위해 preventDefault() 메서드를 사용했다.
- 입력된 할 일은 todos 배열에 저장된다.
- todos 배열에 저장된 할 일들은 localStorage에 각각의 아이디, done:flase(기능4,5와 관련된 것으로, 완료한 일인지에 대한 여부를 나타낸다.)와 함께 저장되도록 했다.
- 아이디는 리스트 맨 위의 것이 list0, 그 다음이 list1, ... 이 되도록 했다.

#### 기능2. 할 일 삭제하기
- x 버튼을 누르면 해당 리스트를 삭제할 수 있다.
- 버튼을 누르면 해당 버튼이 존재하는 div 태그의 아이디로 todos 배열에서 해당 리스트를 찾아 삭제했다.
- 새로고침한 후 다시 리스트가 보이지 않도록 id를 이용해 localStorage에서 해당 할 일을 찾아 삭제했다.

#### 기능3. 전체 리스트 삭제하기
- Delete All 버튼을 누르면 모든 할 일을 삭제할 수 있다.
- todos 배열을 아예 비우고 saveToDo() 메서드로 localStorage에 존재하는 할 일 목록도 삭제했다.

#### 기능4. 완료한 일 체크하기
- 리스트 왼쪽 동그라미 버튼을 누르면 할 일을 완료했다는 의미로 버튼이 꽉 차고 할 일 텍스트에 중간줄이 그어진다.
- 버튼의 click 이벤트가 발생하면 todos 배열과 localStorage에서 해당 목록의 done의 값이 true가 되도록 했다.
- 해당 할 일의 done 값이 true이면 완료 버튼, 텍스트, 삭제 버튼을 포함하는 부모 태그 div에 doneList라는 class를 추가하도록 했다.
  👉🏻(checkListDone() 메서드에 정의했다.)

#### 기능5. 전체 리스트 완료 체크하기
- Select All 버튼을 누르면 전체 일을 완료했다는 의미로 모든 동그라미 버튼이 꽉 차고 모든 할 일 텍스트에 중간줄이 그어진다.
- for 반복문으로 todos 배열의 각 할 일을 가져와 해당 할 일의 done값을 true로 만들고 checkListDone()를 호출했다.

#### 기능6. 총 리스트 개수, 완료한 일 개수, 남은 할 일 개수 하단 부분에서 확인하기
- 총 리스트 개수는 할일이 저장된 todos 배열의 길이로 설정했고 개수를 구하는 함수 countAllList()를 정의했다.
- 할 일이 삭제되거나 추가로 작성될 때마다 countAllList()함수를 호출하여 화면에서 수정되어 보이도록 했다.
- 완료한 일 개수는 localStorage에서 done의 value가 true인 것의 개수로 설정했고 이를 구하는 함수 countDoneList()를 정의했다.
- 할 일이 삭제되거나 완료 버튼을 누르거나 Select All 버튼을 누르는 등 완료한 일의 개수에 변화가 생길 때 countDoneList() 함수를 호출하여 화면에서 수정되어 보이도록 했다.
- 남은 할 일 개수는 localStorage에서 done의 value가 false인 것의 개수로 설정했고 이를 구하는 함수 countLeftList()를 정의했다.
- 할 일이 삭제되거나 추가되는 등 남은 할 일의 개수에 변화가 생길 때 countLeftList() 함수를 호출하여 화면에서 수정되어 보이도록 했다.

## 👩🏻‍💻 후기 및 다음 목표
제일 먼저 아이패드에 화면 구상을 하고 시작했는데, 직접 구상부터 개발까지 하니 저번에 했던 클론 코딩보다 스스로 생각을 많이 할 수 있어서 좋았다. display:flex도 완벽하지는 않지만 이번에 사용하면서 좀 더 익숙해진 듯 하다. 이번 투 두 리스트에서는 완료한 할 일을 line-through 적용하는 것에서 더 나아가 위치를 분리시키지 못해서 아쉬웠고, 계속 보다보니 더 추가하고 싶은 기능들이 보이는 것 같다. 가장 시간이 많이 걸렸던 부분은 완료한 할 일을 새로고침했을 때도 유지시키는 것이었다. 이 부분은 id와 text만 key로 가지고 있었던 todos와 localStorage에 디폴트로 done을 key로, false를 value로 주고 완료한 일의 done에 true 값을 대입하고 checkListDone() 메서드를 호출하여 해결했다. 남은 방학과 이번 학기 중으로 제이쿼리나 리액트를 사용해 추가 기능들을 적용하고, 다음 토이 프로젝트를 진행해볼 예정이다.
