# styled components study

### **styled 사용법** 

```javascript
const Button = styled.button`
	border-radius : 50px;
	padding : 5px;
	
    &:active {
        outline : none;
    }
	background-color : ${props => (props.danger ? "white" : "red")};
`

// withComponent를 이용해서 태그만 변경한채로 스타일을 가져올수 있고
// extend를 이용해서 추가로 스타일을 넣을수도 있다.
const Anchor = Button.withComponent("a").extend`
	text-decoration:none;
`
```



### **전역으로 사용할 스타일 설정**

```javascript
import styled, { injextGlobal} from 'styled-components';

// 공통으로 사용할 경우 injectGlobal을 사용할수 있음.
injectGlobal`
    body{
		padding : 0;
		margin : 0;
    }
`
```

### 

### **애니메이션 사용**

```javascript
import styled, { injextGlobal, keyframes} from 'styled-components';

const Button = styled.button`
  border-radius: 50px;
  padding: 5px;
  min-width: 120px;
  color: white;
  font-weight: 600;
  -webkit-appearance: none;
  cursor: pointer;
  &:active,
  &:focus {
    outline: none;
  }
  background-color: ${props => (props.danger ? "#e74c3c" : "#2ecc71")};
  ${props => {
    if (props.danger) {
      return `animation: ${rotation} ${props.rotationTime}s linear infinite`;
    }
  }};
`;

const rotation = keyframes`
  from{
    transform: rotate(0deg);
  }
  to{
    transform: rotate(360deg);
  }
`;

```



### HTML태그의 속성을 추가해 주는 방법

 태그 다음에 attrs라는 메소드에 객체를 전달한다음 필요한 속성을 정의해주면 된다.

- input태그의 required속성을 주는 예제 

```javascript
const Input = styled.input.attrs({
  required : true
})`
`;
```



### Mixin 같이 공동된 속성을 정의해서 가져다가 쓰는 방법 

```javascript
import styled, { injectGlobal, css } from "styled-components";
// css를 이용해서 공통되는 부분을 정의한 변수를 만듭니다.
const awesomeCard = css`
  box-shadow: 0 4px 6px rgba(50, 50, 93, 0.11), 0 1px 3px rgba(0, 0, 0, 0.08);
  background-color: white;
  border-radius: 10px;
  padding: 20px;
`;

// 사용할 부분에 변수를 넣어주면됩니다.
const Input = styled.input.attrs({
  required : true
})`
  ${awesomeCard}
`;
```

