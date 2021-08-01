# node mysql 서버 연결하기, mysql 쿼리 날리기

- nodejs mysql 서버 연결하기

### createConnection과 createPool의 차이

- createConnection

  - 서버와 단일연결
  - 연결 요청을 할 때마다 객체를 생성하고 연결이 끝나면 연결을 해제해야 함
  - 여러 요청이 발생할 경우 다른 사람의 커넥션이 끝날 때까지 기다려야 함

```js
const connection = mysql.createConnection({
  host: hostname,
  user: username,
  password: user - password,
  database: database,
});
```

- createPool
  - 하나의 연결 pool을 열어서 pool의 제한인원에 해당하는 것은 동일한 connection으로 처리
  - getConnection을 통해 pool을 생성하고 내부에서 query와 release(연결 반납)을 사용

```js
const pool  = mysql.createPool({
  connectionLimit : number,
  host            : hostname,
  user            : username,
  password        : password,,
  database        : database,
});

// 사용하기
pool.getConnection() -> connection.query() -> connection.release()
```

### mysql 쿼리 날리기

- mysql DB에 입력할 명령어 쿼리와 데이터를 인수로 받아서 query 함수로 요청한다.

```jsx
// 형태
const query = `mysql query...`;
connection.query(query);

// 실제 코드
export const queryListToTable = async (data, site_id) => {
  const QUERY_LIST_DATA = "mysql query...";

  try {
    // mysql 서버 연결
    const connection = await pool.getConnection(async (conn) => conn);
    //....
    try {
      // sql 쿼리 날림
      const result = await connection.query(QUERY_LIST_DATA, [data]);
      // 작업 후 연결 반납
      connection.release();
      return result;
    } catch (err) {
      console.log("insert error");
    }
  } catch (err) {
    console.log("query connection error");
  }
};
```
