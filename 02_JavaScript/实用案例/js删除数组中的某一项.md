##  js删除数组中某一项,

###  splice()

用来添加或者删除数组的数据，只返回被删除的数据（组合成数组返回），**改变原数组**

splice(index, howmany, item1, item2)

index:：必需，添加或者删除的位置，值为负数从数组结尾处规定位置。

howmany：必需，删除的项目数量，值为0，则不会删除项目。

item1, item2 itemX：可选，向数组中添加的新项目。

```
var id = '3'
var tagList = [{"parentTagId":"1","parentTagName":"学校","childTagId":"3","childTagName":"高中"},
                {"parentTagId":"1","parentTagName":"学校","childTagId":"4","childTagName":"初中"}]
for(var i = 0; i < tagList.length; i++){
    if(tagList[i].childTagId === id){
        tagList.splice(i,1);
    }
}
console.log(JSON.stringify(tagList))
```

或者直接是拿对象过来也行，一样的方法：

```
var obj = {
    parentTagId : '1',
    parentTagName:"学校",
    childTagId: '3',
    childTagName:"高中"
}
var tagList = [{"parentTagId":"1","parentTagName":"学校","childTagId":"3","childTagName":"高中"},
                {"parentTagId":"1","parentTagName":"学校","childTagId":"4","childTagName":"初中"}]
for(var i = 0; i < tagList.length; i++){
    if(tagList[i].childTagId === obj.childTagId){
        tagList.splice(i,1);
    }
}
console.log(JSON.stringify(tagList))
```

### slice()

返回两个索引之间的数据，**不改变数组**

slice(start, end) start 必需，end 选填。返回值不包括end

```js
var heros=["李白",'蔡文姬','韩信','赵云','甄姬','阿珂','貂蝉','妲己'];
console.log(heros.slice(1,4))//  [ "蔡文姬", "韩信", "赵云" ]开始索引为1 结束索引为4(不包括4)
console.log(heros)// 不改变原数组  [ "李白", "蔡文姬", "韩信", "赵云", "甄姬", "阿珂", "貂蝉", "妲己" ]
```

若`开始索引`为负数,则将该值加上数组长度后作为开始索引,如果此时还是负数,开始索引为0。

```js
var heros=["李白",'蔡文姬','韩信','赵云','甄姬','阿珂','貂蝉','妲己'];
console.log(heros.slice(-6,4))//  [ "韩信", "赵云" ]开始索引为2 结束索引为4(不包括4)
console.log(heros.slice(-10,4))//  [ "李白", "蔡文姬", "韩信", "赵云" ]开始索引为0 结束索引为4(不包括4)
```

如果开始索引大于或等于数组的长度或大于或等于结束索引，则slice()返回一个空数组。

```js
var heros=["李白",'蔡文姬','韩信','赵云','甄姬','阿珂','貂蝉','妲己'];
console.log(heros.slice(8,4))//  [ ]
console.log(heros.slice(10,4))//  [ ]
console.log(heros.slice(4,4)) //[ ]
console.log(heros.slice(5,4)) //[ ]
```

如果`结束索引`省略，截取到数组的末尾。如果为负,数组长度加上该值即为结束索引,如果此时还为负数,返回空数组

```js
var heros=["李白",'蔡文姬','韩信','赵云','甄姬','阿珂','貂蝉','妲己'];
console.log(heros.slice(1))// [ "蔡文姬", "韩信", "赵云", "甄姬", "阿珂", "貂蝉", "妲己" ]
console.log(heros.slice(1,-4))//  [ "蔡文姬", "韩信", "赵云" ] 开始索引1  结束索引8+(-4)=4
console.log(heros.slice(1,-10)) //[ ] 开始索引1  结束索引8+(-10)=-2
```

