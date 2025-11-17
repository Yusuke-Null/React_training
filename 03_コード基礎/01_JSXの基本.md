# JSXの基本
Reactの拡張子は「.jsx」でJSX記法というReact特有の文法でJSを書くときに使う(TypeScriptは.tsx)

- **function コンポーネント名でreturn**に出力したいコンポーネントを記述  
※ 複数行書きたい場合はreturn()でカッコ内に書くこと  
- **export default コンポーネント名**でApp.jsxで呼び出せるようになる
``` jsx
function Button(){
	return <button type="button">クリック</button>
}
// function Button(){
// 	return (
// 		<button type="button">
// 			<icon>icon</icon>
// 			<span>クリック</span>
// 		</button>
// 	)
// }

export default Button;
```
jsxで記述した内容をApp.jsxで使うことができる  
- **import コンポーネント名 from 'パス'で**読み込む
- 読み込んだコンポーネントがあたかもタグ化のように使える
``` jsx
import './App.css'
import Button from './Button.jsx'

function App() {
  return (
    <>
      <b1>Hello World</b1>
      <Button />
    </>
  )
}

export default App
```

JSと同様、関数を定義して発火させることもできる
```jsx
function Button(){
	const handClick = () => {
		alert('クリックされました');
	}
	return (
		<button type="button" onClick={handClick}>
			<icon>icon</icon>
			<span>クリック</span>
		</button>
	)
}

export default Button;
```

React仕様の注意点  
- returnの中で複数のタグを書きたいときは空のフラグメント(<></>)で囲わないといけない(1つしかタグがないならいらない)
``` jsx
import './App.css'
import Button from './Button.jsx'

function App() {
  return (
    <>
      <b1>Hello World</b1>
      <Button />
    </>
  )
}
```
