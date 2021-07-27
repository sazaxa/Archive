1. 문제점

서버로부터 제공받은 지정된 시간에 종료되는 타이머를 제작해야하는데 서버로부터 받아오는 시간 포멧이
js에서 제공하는 기본 포멧과 다름 
`20210701T121212[Z] = YYYYMMDDTHHMMSS[Z]`이를 Date.parse를 통해 parsing하면
시간이 어긋나 계산하는데 문제가 발생함.


2. 문제의 해결
- 해결방안으로 생각한 것은 크게 두 가지.
[1] 서버로부터 받아오는 시간을 문자열로 변경하고 필요한 부분만 slice를 통해 가져온다.
[2] moment.js를 통해 parsing한다.

선택한 방법은 moment.js를 사용하는 것인데 시간 관련 library 중 가장 흔하고 새로운 library를 통해 업데이트도 지속적임

3. 배운점
- 시간 표기 format이 다르면 계산하는데 문제가 발생한다는 점. 따라서 설계과정에서 시간 format을 통일하도록 하자 (like UCT)

4. 느낀점

만약 react functional로 작업을 하고 있다면 useEffect를 통해 fetch하고 useEffect 내에서 state의 변화를 주고,
그 변화에 따른 function이 이어져야 하는 경우 state를 observing하는 useEffect를 하나 더 만들자.

useEffect는 순서대로 실행된다.



