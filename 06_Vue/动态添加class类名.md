# vue 中动态添加 class 类名
```html
<div>
    <h2>动态添加类名</h2>

    <!-- 第一种：对象的形式 -->
    <!-- 第一个参数：类名，第二个参数：Boolean值 -->
    <!-- 对象的形式：用花括号包裹，类名用引号 -->
    <!-- 优点：以对象的形式可以写多个，用逗号隔开 -->
    <p :class="{'p1':true}">对象的形式</p>
    <p :class="{'p1': false, 'p': true }"></p>

    <!-- 第二种方式: 三元表达式，放在数组里，类名用引号 -->

    <p :class="[ 1 < 2 ? 'p1' : 'p' ]" >三元表示式(文字的颜色)</p>


    <!-- 第三种方式: 数组的形式 -->
    <p :class="[isTrue, isFalse]">数组的形式(文字的颜色)</p>

    <!-- 数组中用对象 -->
    <p :class="[{'p1': false}, isFalse]">数组中使用对象(文字的颜色)</p>


    <!--补充:  class中还可以传方法，在方法中返回类名-->
    <p :class="setClass">通过方法设置class类名</p>

</div>


<!-- === 添加样式 === -->

<div id="box">
    <!--直接添加样式-->
    <p style="background-color: blue;">sssss</p>
    <!--绑定样式-->
    <p v-bind:style="'background-color: red;'">sssss</p>
    <!--将vue中的属性作为样式设置-->
    <p :style="obj">sssss</p>
    <!--将多个属性作为样式设置-->
    <p :style="[obj,obj1]">sssss</p>
</div>
<script type="text/javascript">
    var vm=new Vue({
        el:"#box",
        data:{
            obj:{
                backgroundColor:"gold"
            },
            obj1:{
                fontSize: "30px"
            }
        },
    });
</script>

```
```js
export default{
	data () {
        return {
            isTrue: 'p1',
            isFalse: 'p'
        }；
    },
    method: {
	  setclass () {
      	  return 'p1';
      }
  	}
}

```
