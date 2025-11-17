# Props
親コンポーネントから子コンポーネントへ値を渡す仕組み  
EX) disabledやtype等の属性を外部から設定したい場合に使う  

App.jsx(親,外部)でButtonの属性を設定する
``` jsx
import './App.css'
import Button from './Button.jsx'

function App() {

  return (
    <>
      <b1>Hello World</b1>
      <Button type="button" />
    </>
  )
}

export default App
```
親コンポーネントから受け取った属性を引数に取って、タグで使うことができる  
const {属性名} = 引数名で取得でき、タグ内で{引数名}で変数を展開できる
``` jsx
function Button(props){
  const { type, disabled } = props;

	return (
		<button type={type} disabled={disabled}>
			クリック
		</button>
	)
}

export default Button;
```
## children
さらに**children**という特殊なPropsがあり、親で設定しなくても使える  
これは親側のコンポーネント内で書いた要素やテキストを受け取るためのもの
``` jsx
import './App.css'
import Button from './Button.jsx'

function App() {
  return (
    <>
      <b1>Hello World</b1>
      <Button type="submit" disabled={false}>
        ボタンクリック
      </Button>
    </>
  )
}

export default App
```
{children}にはボタンクリックというテキストが渡される
```jsx
function Button(props){
  const { type, disabled, children } = props;

	return (
		<button type={type} disabled={disabled}>
			{children}
		</button>
	)
}

export default Button;
```
