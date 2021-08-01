# 구글 스프레드 시트 크롤링

- 구글 시트 api를 활용해 구글 스프레드 시트 크롤링하기

### [1-1] Google Sheet API 활용하기

- API Key를 발급받아 구글 시트 API 활용하는 방법
- 장점 : 별도의 인증 처리 없이 구글 시트를 크롤링 할 수 있다
- 단점 : 시트의 공유 옵션이 '링크가 있는 모든 사용자에게 공유' 여야 함. 보안 이슈가 있다.

```jsx
// 예시
export async function getCustomerList(SHEET_ID, SHEET_NAME) {
  const SHEET_NAME_ENCODE = encodeURI(SHEET_NAME);
  const API_URL =
    BASE_URL + SHEET_ID + "/values/" + SHEET_NAME_ENCODE + "?key=" + API_KEY;

  try {
    const response = await axios.get(API_URL, QUERY_PARAM);
    const sheetData = await response.data.values;
	....
```

### [1-2] google-spreadsheet 라이브러리 활용하기

- 장점 : 클라이언트 인증 과정이 매우 간단
- 단점 : 시트의 첫번째를 header로 자동 인식해 getter/setter로 지정후 데이터를 반환함. 헤더를 변경해서 사용할 경우 변경할 수 없다.

### [1-3] OAuth 2.0 인증 받기

해결→ auth 인증 처리 해결

- 그래서 Oauth 인증이 필요

```jsx
import { google } from "googleapis";
const keys = require("./auth");
//...
const client = new google.auth.JWT(keys.client_email, null, keys.private_key, [
  GOOGLE_API,
]);

client.authorize(function (err, tokens) {
  try {
    console.log("client connected");
    runApp(client);
  } catch (err) {
    console.log("authorize error");
  }
});
```
