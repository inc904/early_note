###  Mongoose: `findOneAndUpdate()` and `findOneAndDelete()` without the `useFindAndModify` option set to false are deprecated. 

警告：Mongoose:不推荐使用未将“useFindAndModify”选项设置为false的“FindAndDupDate（）”和“FindAndDelete（）”。

使用mongoose的findOneAndUpdate、FindAndDelete两个方法，返回的数据是未更新的数据，但是库里的数据已经更新了；



- 解决 :

默认值是返回未更改的文档。 如果您希望返回新的更新文档，则必须传递一个附加参数： new属性设置为true的对象。

```js
 UserModel.findByIdAndUpdate(user_id, user, {new: true}, function (error, oldedData) {}
```

