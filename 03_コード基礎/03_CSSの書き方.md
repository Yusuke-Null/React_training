# CSSの書き方
ReactではCSSファイルを直接JS内にインポートして読み込める  
※ **複数のコンポーネントに同じクラスがぶつかってしまうのを避けるためにCSSモジュールを使う**  
1. .module.cssというファイルを設定し、その中にcssを記載する
2. jsxファイルで「**import 変数名 from 'パス';**」で1を読み込む
3. タグにクラスを設定するが、classで指定するのでなく、**className={2の変数名.クラス名}で指定する**必要がある
```jsx
import styles from "./Button.module.css";

function Button(props){
  const { type, disabled, children, onClick } = props;
	return (
		<button className={styles.button} type={type} disabled={disabled} onClick={onClick}>
			{children}
		</button>
	)
}

export default Button;
```

HTMLを見るとクラス名が「button_xxx」のようなランダムな文字列に変換され、クラス名のバッティングを避けてくれる  
実行時に見たクラス名
> class="_button_12uqb_1"
