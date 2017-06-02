# scss或者说这类预处理器,是现在前端工程化写CSS的标配了,用惯了的话会觉得用原生的方式来写CSS很不习惯,也很反人类.

## 什么是SCSS

- 总之就是一款工程化的CSS工具了,很强大.

## 为什么要用?

- 因为可以装逼(当然不是,某些大型前端项目中CSS文件过多的时候可以便于维护和管理以及有效减少代码量)

## 遇到的问题:

- 公共某块的提取与导入:

```css
//common.scss

$b-pink: #FF8EB3;
$b-blue: #01ADFF;
$kakuya: #E593C3;
$mokou: #AE0104;
$m-dark: #333333;
$m-white: #FFFFFF;
$mokou: mokou;

// main.scss

@import './common.scss'

```

- 公共前缀的提取与使用

```css
$mokou: mokou;

.#{$mokou} {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    align-items:center;
    background-color: rgba($m-dark,.75);
    opacity: 0.75;
    &-img {
        width: 100%;
        height: 100%;
        background-repeat: no-repeat;
        background-size: cover;
        z-index: -99999;
    }
}
```

这里的.#($mokou)除了最前面的选择器.之外后面是scss定义好的使用方式,选择器可以更换成#或者不写,下面的&自动继承父元素的选择器变量
