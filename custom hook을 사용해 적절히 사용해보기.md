예를 들면 배달어플의 경우 요식업체의 정보를 매번 불러와야 한다.

이 경우 서버로 계속 같은 형태의 query를 던지게 되는데 이를 각 페이지, 각 컴포넌트 마다 계속 같은 로직을 짜서 넣어주는 것은 좋지못하다.

이를 hook으로 분리해 하나의 hook으로 같은 query 문을 전부 떼워보자.
```js
function reducer(state, action){
    switch (action.type){
        case 'SUCCESS':
            return{
                loading: false,
                data: action.data.data.getProducts.list,
                error:null
            };
        case 'ERROR':
            return{
                loading:false,
                data:null,
                error:action.error
            };
            default:
                throw new Error(`Unhandled action type: ${action.type}`);
    }
}
function useGetData(){
	const [state, dispatch] = useReducer(reducer,{
    	loading:false,
      	data:null,
      	error:false
    });
  
  
  const fetch = async (...someArgs)=>{
    try{
    	const data = await (query 요청);
    };
    dispatch({type:'SUCCESS', data});
    catch(error){
    	dispatch({type:'ERROR', error:error});
      
    }
  
  }
  
  useEffect(()=>{ fetch (...someArgs)},[deps])
  return [state, fetch]
}```
매번 반복되는 endpoint에 요청을 보내는 것이라면 주소까지 그냥 hook 내부에 넣어주어도 되지만 asyc를 담당하는 hook을 하나로 두고 요청을 던질때마다 사용하는 것도 좋다. ( 추상화 수준이 중요 )

해당 custom hook의 주요 기능은 한 가지이다.

-> 데이터를 받아서 상태값과 데이터를 반환해주고, 마지막으로 fetch 함수를 다시 돌려준다.

fetch 함수를 돌려주는 이유는 다른 조건으로 다시 해당 함수를 호출할 수 있도록 돌려주는 것인데 이게 가장 중요한 요점이 된다.

해당 custom hook을 사용해 infinity pagination을 제작할 수 있는데 특정 pagination의 page에 접근하였을 때 해당 fetch를 다시 실행시켜 server로 부터 값을 받아오고 해당 값을 다시 렌더해주면 되기 때문이다.
