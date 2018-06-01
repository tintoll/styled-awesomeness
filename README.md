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



### Theming - 공통된 테마 값을 불러와서 사용하는 방법 

1. 공통으로 사용할 값들을 정의한 객체를 하나 만들어준다.
2. ThemeProvider 컴포넌트의 prop으로 그 값을 넣어준다.
3. ThemeProvider 안의 컴포넌트들에서 공통으로정의한 값들을 prop를 통해 사용할수 있다.

```javascript
// theme.js
const theme = {
  mainColor: "#3498db",
  dangerColor: "#e74c3c",
  successColor: "#2ecc71"
};

export default theme;

// App.js
import styled, { injectGlobal, ThemeProvider } from "styled-components";
import theme from './theme';

const Container = styled.div`
  height: 100vh;
  width: 100%;
  background-color: pink;
`;

const Card = styled.div`
  background-color: red;
`;

const Button = styled.button`
  border-radius: 30px;
  padding: 25px 15px;
  background-color: ${props => props.theme.successColor};
`;

const Form = () => (
  <Card>
    <Button>Hello</Button>
  </Card>
);

class App extends Component {
  render() {
    return (
      <ThemeProvider theme={theme}>
        <Container>
          <Form />
        </Container>
      </ThemeProvider>
    );
  }
}

export default App;
```

ThemeProvider 설정 방법이 Redux의 스토어를 정의해주는 방법이랑 비슷하다.



