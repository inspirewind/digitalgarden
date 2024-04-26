---
{"dg-publish":true,"permalink":"/笨蛋学渣想发NAR是否搞错了什么/nodejs/mongoose/Getting Started/"}
---


了解`Scheme`和`Model`的概念，创建`Scheme`和`Model`并将其放置在后端项目的对应目录中。

#### MongoDB: Collection, Document
 **Collection**：在MongoDB中，`collection`是一个存储MongoDB文档的容器，类似于关系数据库中的`表`。每个`collection`可以包含多个`document`，这些`document`可以具有***不同***的结构，但通常会有相同或相似的数据结构。
**Document**：MongoDB的`document`是数据的基本单位，类似于关系数据库中的`行`。每个document都是一个键值对的集合，其中数据可以是各种数据类型，如字符串、数字、数组、嵌套文档等。

#### Mongoose: Schema, Model
**Schema**：在Mongoose中，`Schema`是对应于MongoDB collection中`document`的数据结构的定义。Schema定义了document中可以包含的字段及其数据类型、验证规则、默认值等。Schema是一个构造函数，你可以通过它来定义你希望文档包含的所有字段和它们的类型，还可以定义复杂的验证规则或默认值。
**Model**：Mongoose的`Model`是基于Schema构建的，是一个构造函数，并与特定的MongoDB collection关联。它代表数据库中的一个`collection`，并提供了**创建、查询、更新、删除**`documents`的接口。通过Model，你可以实现对collection的操作。一个Model对应MongoDB中的一个collection。

#### Install
```bash
npm install mongoose --save
```

#### 引入mongoose和连接数据库
```javascript
// getting-started.js
const mongoose = require('mongoose');

main().catch(err => console.log(err));

async function main() {
  await mongoose.connect('mongodb://127.0.0.1:27017/test');

  // use `await mongoose.connect('mongodb://user:password@127.0.0.1:27017/test');` if your database has auth enabled
}
```

#### 定义一个Schema
```javascript
const kittySchema = new mongoose.Schema({
  name: String
});
```
每个`Schema`是MongoDB中一个`collection`的映射。在一个`Schema` 中，每个键都定义了`documents`中的一个属性，该属性将被强制转换为其关联的`SchemaType`。
允许的`SchemaType`有：
- [String](https://mongoosejs.com/docs/schematypes.html#strings)
- [Number](https://mongoosejs.com/docs/schematypes.html#numbers)
- [Date](https://mongoosejs.com/docs/schematypes.html#dates)
- [Buffer](https://mongoosejs.com/docs/schematypes.html#buffers)
- [Boolean](https://mongoosejs.com/docs/schematypes.html#booleans)
- [Mixed](https://mongoosejs.com/docs/schematypes.html#mixed)
- [ObjectId](https://mongoosejs.com/docs/schematypes.html#objectids)
- [Array](https://mongoosejs.com/docs/schematypes.html#arrays)
- [Decimal128](https://mongoosejs.com/docs/api/mongoose.html#mongoose_Mongoose-Decimal128)
- [Map](https://mongoosejs.com/docs/schematypes.html#maps)
- [UUID](https://mongoosejs.com/docs/schematypes.html#uuid)

#### 构建Model
```javascript
const Kitten = mongoose.model('Kitten', kittySchema);
```
编译`Schema`生成一个`Model`

在后端服务器中，将`Schema`和`Model`写在一个文件中，并放置在`models`目录下面。如我们有一个表示project的`Schema`，它在`app/models/browse/project.js`文件中，其中`app/models`是node固定目录，`browse`是我们自定义的目录。
##### project.js
```js
const mongoose = require("mongoose");
// const mongooseAggregatePaginate = require('mongoose-aggregate-paginate-v2');
const Schema = mongoose.Schema;

```


``` js
const ProjectSchema = new Schema({
  "dataset_id": {
    type: String,
    index: true,
  },
  "project_id": {
    type: String,
    index: true,
  },
  "data_resource": {
    type: String,
    index: true,
  },
  "species": {
    type: String,
    index: true,
  },
  "tissue_or_cell_line": {
    type: String,
    index: true,
  },
  "submission_date": {
    type: String,
    index: true,
  },
  "disease": {
    type: String,
    index: true,
  },
  "quality_assessment": {
    type: Number,
    index: true,
  },
  "method": {
    type: String,
    index: true,
  }
});

```
在定义`Schema`时，我们将一个对象赋值给`Schema`的键，这个对象除了必要的`type`属性外，还有`index`属性。在[[笨蛋学渣想发NAR是否搞错了什么/nodejs/mongoose/Schemas\|Schemas]]中会详细介绍。

``` js
// set compound index
ProjectSchema.index({
  project_id: 1,
  data_resource: 1,
  species: 1,
  tissue_or_cell_line: 1,
  submission_date: 1,
  disease: 1,
  quality_assessment: 1,
  method: 1,
})

```
这部分代码为`ProjectSchema`设置了一个复合索引，复合索引包括多个字段，可以提高在这些字段上进行查询的效率。索引中字段的值`1`代表按升序排列。

```js
// ProjectSchema.plugin(mongooseAggregatePaginate);

// Mongoose.model( [name], [schema], [collection], [skipInit] )
const Project = mongoose.model("Project", ProjectSchema, "project");

module.exports = Project;
```
使用`mongoose.model`创建`Model`，并将`model`导出。