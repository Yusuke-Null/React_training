# JSXの基本
Reactの拡張子は「.jsx」でJSX記法というReact特有の文法でJSを書くときに使う(TypeScriptは.tsx)

``` jsx
function Button(){
	return <button type="button">クリック</button>
}

export default Button;
```
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
