

# 1. 아래의 설명을 읽고 T/F 여부를 작성하시오

* T
* F
* T



# 2. 아래의 코드가 실행되었을 때 Web API, Task Queue, Call Stack 그리고 Event Loop에서 어떤 동작이 일어나는지 서술하시오.

1. console.log('Hello SSAFY!')가 Call Stack으로 들어간 후 출력됨 -> Hi
2. setTimeout(function () {console.log('I am from setTimeout')}, 1000) 이 Call Stack으로 들어감
3. setTimeout 은 바로 수행이 되지 않으므로 Web API로 넘어가서 수행됨
4. 기다리는 동안 console.log('Bye')가 Call Stack으로 들어간 후 출력됨 -> Bye
5. Web API에서 처리된 setTimeout 안의 함수가 Task Queue로 넘어감
6. Event Loop가 Call Stack이 빈 것을 확인하면 Task Queue 내에 가장 오래된 처리를 Call Stack으로 이동시킴
7. console.log('I am from setTimeout')이 Call Stack으로 들어간 후 출력됨 -> I am from setTimeout
