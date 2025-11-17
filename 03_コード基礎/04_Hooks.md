# Hooks
ReactにはuseState,useEffect等、頭に「use」が付く特別な関数が標準搭載されている  
-> Reactコンポーネント内で使用することで、ステート管理や副作用処理ができるようになる

最も代表的なのがuseState,useEffectでこういったものをまとめたものがHooks
- useState: 状態を管理するためのフック
- useEffect: 副作用(サイドエフェクト)を扱うためのフック

## useState
Q.Buttonクリックするたびにカウントを増やすコンポーネントを作る  
1. useStateを使うには、「**import { useState} from 'react';**」を記述する
2. const [状態を持たせる変数, 変数を更新する関数] = useState(初期値)を定義する
-> 状態を持った変数とそれを更新するだけの関数は毎回セットで定義する。ここの変数は他の関数ではいじろうとしてもできない  
3. 変数を更新する関数を定義する
4. onClickなどで呼び出す2で定義した関数をセットする
5. タグ内で状態を持った変数を使う
``` jsx
import styles from "./Button.module.css";
// 手順1
import { useState } from "react";

function Button(props){
	const [count, setCount] = useState(0);
  // 手順2
  const { type, disabled, children } = props;
  // 手順3
	const handleClick = () => {
		setCount(count + 1);
	}
	return (
    // 手順4
		<button className={styles.button} type={type} disabled={disabled} onClick={handleClick}>
      // 手順5
      カウント: {count}
		</button>
	)
}

export default Button;
```

また、Reactではコンポーネント間で状態を共有することができる  
-> 上位のコンポーネントにuseStateを持たせて、子コンポーネントにPropsで渡す  
``` jsx
-- App.jsx(親)
import './App.css'
import Button from './Button.jsx'
import { useState } from "react";

function App() {
	const [count, setCount] = useState(0);
  const handleClick = () => {
		setCount(count + 1);
	}

  return (
    <>
      <h1>Hello World</h1>
      <Button type="button" disabled={false} onClick={handleClick}>
        カウント: {count}
      </Button>
    </>
  )
}

export default App

-- Button.jsx(子)
import { Children } from "react";
import styles from "./Button.module.css";

function Button(props){
  	const { type, disabled, onClick, children } = props;

	return (
		<button className={styles.button} type={type} disabled={disabled} onClick={onClick}>
			{children}
		</button>
	)
}

export default Button;
```

### 複数コンポーネント間での状態管理
Q. カウントを表示用のコンポーネントを作成する  
Button.jsxではカウントするコンポーネントとする
``` jsx
import { Children } from "react";
import styles from "./Button.module.css";

function Button(props){
  	const { type, disabled, onClick, children } = props;

	return (
		<button className={styles.button} type={type} disabled={disabled} onClick={onClick}>
			{children}
		</button>
	)
}

export default Button;
```
Display.jsxを作成し、カウントを表示する為のコンポーネントとする
``` jsx
function Display(props) {
	const { count, children } = props;
	return (
		<div>
			カウント: {count}
		</div>
	)
}

export default Display;
```
最上位の親であるApp.jsxでDisplayを呼び出し、Propsでカウント数を渡す
``` jsx
import './App.css'
import { useState } from "react";
import Button from './components/Button/Button.jsx'
import Display from './components/Display/Display.jsx';

function App() {
	const [count, setCount] = useState(0);
  const handleClick = () => {
		setCount(count + 1);
	}

  return (
    <>
      <h1>Hello World</h1>
      <Button type="button" disabled={false} onClick={handleClick}>
        ボタン
      </Button>
      <Display count={count} />
    </>
  )
}

export default App
