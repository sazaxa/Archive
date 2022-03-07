## 형식
- 어떠한 문제가 있었는가
-> query getProducts에서 list가 null로 반환되는 문제
- 문제를 어떻게 해결하였는가
-> query의 variable값에서 필수 인자는 아래와 같다.
```ts
      search: {
        // firstCategory: '2c9faa5c764b382c01764be8b5cd0063', // category 구분을 위해 남김 : zerozoo
        firstCategory: '',
        bestseller: true,
        sku: ctx.params?.sku,
      },
      page: {
        pageNumber: 1,
        limit: 1,
        orderBy: 'createdDate',
        type: 'DESC',
      },
```
이 때 pageNumber의 값은 pageNumber > 0 의 값이여야 한다. 
- 배운점
DB의 변경과 함께 이루어져 값을 pageNumber의 값을 건들면 안되었다. DB 문제로 의심될 경우 DB를 잡자..!
- 느낀점
backend의 주기적인 pull과 db의 최신화가 필요하고 gql query의 variables의 값을 확실히 해줄 무언가가 필요하다.

