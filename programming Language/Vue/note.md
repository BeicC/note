* npm
npm 类似于Java中的maven
* package.json
package.json中的dependencies与devDependencies的区别
一个是生产环境，一个是开发环境
```bash
npm install -D # 安装开发环境的依赖
npm install # 安装生产环境的依赖
```
# Vue指令
* v-on
```vue
<button v-on:click="handleClick">Click me</button> 
# 简写
<button @click="handleClick">Click me</button> 
```
v-on:click可以缩写为@click
@click中的click可以是动态的
```vue
<button @[envent]="handleClick(123)">Click me</button> 
<script>
    const event = 'click'
</script>
```
```
<button @click.stop>Click me</button>
```
@click.stop可以阻止事件冒泡

* v-bind
v-bind简写为:
```vue
<img :src="imageSrc" />
```
上面的代码意思是将imageSrc的值绑定到img标签的src属性上；这样src的值是动态的
