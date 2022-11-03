# 1. 아래의 설명을 읽고 T/F 여부를 작성하시오

* F
* T
* T

# 2. Vue는 단방향 데이터 흐름을 지향하는 프론트엔드 프레임워크다. 공식문서를 참고하여 그 이유를 서술하시오.

* 하위 컴포넌트가 실수로 상위 컴포넌트 상태를 변경하여 앱의 데이터 
  흐름을 이해하기 힘들게 만드는 것을 방지하기 위함

# 3. 아래와 같은 Vue 프로젝트에서 2개의 버튼이 동작하는 것을 비교하여 .native 수식어의 역할을 작성하시오.

* 하위 컴포넌트에서 루트 엘리먼트의 네이티브 이벤트를 받기 위해 사용한다.
  
  `<hello-World @click="onClick"></hello-world>` : console 창에 아무 일도 일어나지 않음
  
  `<hello-World @click.native="onClick"></hello-world>` : console 창에 Hello!

# 4. 다음은 자식 컴포넌트에서 이벤트를 발생시켜 부모 컴포넌트의함수를 실행하는 코드이다. 빈칸(a), (b), (c)에 들어갈 코드를 작성하시오.

(a): this.$emit

(b): @add-todo="onAddTodo"

(c): onAddTodo(a){
 console.log(a)
}
