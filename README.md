# styled components study

styled 사용법 

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



전역으로 사용할 스타일 설정

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



애니메이션 사용

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



