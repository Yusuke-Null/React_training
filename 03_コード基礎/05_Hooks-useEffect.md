# Hooks-useEffect
副作用とはプログラムが本来の目的以外のことをする場合に使いたい処理  
EX1) カウントが30になったら0に戻す(カウントする本来の目的ではない)  
EX2) タイムラインに動画があれば、自動再生される(スクロールが本筋)

1. useEffectを使うには「**import {  useEffect } from "react";**」でreactから読み込む
2. 関数の中かつreturnの前に「**useEffect(コールバック関数=>{処理}, 配列);**」で定義する  
-> 配列の値に変更があった時だけ、処理の内容が実行される  
※ 配列を空にすると、コンポーネントが画面に初回表示された時だけ実行される  
-> 読み込んだ瞬間に1度だけ実行したい時に使う
``` jsx
// カウントが15になったら0に戻す
useEffect(()=>{
  if(15 < count) {
    setCount(0);
  }
}, [count])
```

Q. 読み込み時にはLoadingを表示する  
※ setTimeoutであえて2秒遅延させて、表示が見えるようにしている
```jsx
import { useEffect, useState } from "react";
function Display(props) {

	const [text, setText] = useState("Loading...");

	useEffect(() => {
		setTimeout(() => {
			setText(`カウント: ${props.count}`);
		},2000);
	}, []);

	return (
		<div>
			{text}
		</div>
	)
}

export default Display;
```

**Hooksは関数コンポーネントのトップレベルでしか呼べないため、記述順に注意**  
``` jsx
// OK
function App() {
	const [count, setCount] = useState(0);
  const handleClick = () => {
		setCount(count + 1);
	}
}

// NG エラーになる
function App() {
  const handleClick = () => {
  		setCount(count + 1);
  	}
	const [count, setCount] = useState(0);
}
