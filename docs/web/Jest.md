<!--
 * @Author: zhangkai
 * @Date: 2020-11-03 16:04:55
 * @LastEditTime: 2020-11-03 16:05:25
 * @LastEditors: zhangkai
 * @Description: 
-->

#### Jest 入门：使用 JS 进行单元测试

### 一，什么是测试？
用行话说，**测试表示检查我们的代码是否满足一些期望**。<br>
例如，一个名为 `transformer` 的函数在**接收一个输入（input）后，返回一个预期输出（expected output）**。

测试分为很多类型，大致总结的话主要有三类：
- **单元测试**
- **基层测试**
- **UI 测试**

本文介绍的 Jest 教程覆盖的是**单元测试**。

### 二，Jest 是什么？
[Jest](https://www.jestjs.cn/) 是一个 JavaScript **测试框架**，旨在确保任何 JavaScript 代码的正确性。它为你提供了 易于理解、熟悉且功能丰富的 API 来编写测试用例，并快速地反馈结果。


### 三，我怎么知道要测试什么？
提到测试的时候，即使是最简单的一个代码块可能都让初学者不知所措。最常问的问题的是“**我怎么知道要测试什么？**”。如果你正在写一个 web 应用，那么你每个页面每个页面的测试用户交互的方式，就是一个很好的开端了。但 Web 应用也是由很多个**函数和模块组成**的代码单元，也是需要测试的。通常有两种情况：
- 你接手的遗留代码没有写测试用例
- 你必须从无到有的实现一个新功能

该怎么办呢？对于上面两种场景，你可以把测试视为**代码的一部分**来编写。我所说的这些代码，是用来检查给定的函数是否产生预期输出结果的。 一个典型的测试流程如下
1. 引入要测试的函数
2. 给函数一个输入
3. 定义预期输出
4. 检查函数是否返回了预期的输出结果

就这么多。这样看测试也没那么可怕的嘛：输入 —— 预期输出 —— 验证结果。好了，现在就要开始介绍 Jest 了，它几乎可以准确地检测我们刚才说过的内容。

### 四，快速开始
每个 JavaScript 项目都需要一个 **NPM 环境**（确保系统中安装了 Node）。下面，我们创建一个新的文件夹，并且初始化项目。

```bash
$ mkdir getting-started-with-jest && cd $_
$ npm init -y
```

接下来，再安装 Jest：

```bash
$ npm i jest --save-dev
```

然后我们配置下 NPM 脚本，为了能够在命令行执行我们的测试用例。打开 **package.json**，将执行 Jest 的命令命名为“test”：

```json
"scripts": {
  "test": "jest"
},
```
现在可以开始了！

### 五，规范和测试驱动开发

开发者都喜欢创意自由。但当涉及到的事情很严肃的时候，大多数时候就没有那么多的特权了。通常我们必须遵循**规范**，这是指，一个书面上的或者口头上的构建描述。

在本教程中，我们从项目经理那儿拿来的是一个相当简单的规范。一个非常重要的客户需要一个**能够过滤出数组中我们所需对象的函数**。

对数组中每个对象，我们都要检查它的“`url`”属性，**是否属性值跟我们给定的项目匹配**。在最终的结果数组里，包含的都是我们匹配到的对象成员。想要成为一个精通测试的 JavaScript 开发人员，需要遵循 **测试驱动开发**（test-driven development模式，这种模式要求在开始编写代码之前，**先编写失败的测试用例**。

默认 Jest 会在名为 **tests** 的项目文件夹中寻找测试文件。我们来创建一个新文件夹：
```bash
$ cd getting-started-with-jest
$ mkdir __tests__
```
接下来在 **tests** 文件夹中创建一个文件 **filterByTerm.spec.js**。你可能存在疑问，为什么文件名中包含一个“.spec”？这其实是从 Ruby 借鉴而来的一种约定，用于将文件标记为特定功能的规范。

现在开始测试!

### 六，测试结构 & 第一个失败测试
好了，现在常见第一个 Jest 测试用例。打开文件 **filterByTerm.spec.js**，创建一个测试块：

```js
describe("Filter function", () => {
  // test stuff
});
```
我们的第一个朋友叫 **describe**，这个 Jest 方法用来包含一个或一个以上的相关测试。<br>
每次为一个功能开始编写新的测试套件的时候，都要包在 **describe** 里。这个方法接收两个参数：测试套件的描述以及包装实际测试用例的回调函数。

接下来就要介绍另一个函数 **test** 了，这里用来定义实际的测试代码块：

```js
describe("Filter function", () => {
  test("it should filter by a search term (link)", () => {
    // actual test
  });
});
```

现在可以准备写测试了。记住，测试是关于**输入、函数和预期结果**的事情。首先，我们定义一个简单的输入——一个包含对象成员的数组：

```js
describe("Filter function", () => {
  test("it should filter by a search term (link)", () => {
    const input = [
      { id: 1, url: "https://www.url1.dev" },
      { id: 2, url: "https://www.url2.dev" },
      { id: 3, url: "https://www.link3.dev" }
    ];
  });
});
```

再来定义我们的**预期结果**。根据规范，被测试函数应该去掉 `url` 属性与给定搜索项不匹配的对象。比如，我们的搜索项是“`link`”，期望的结果是一个仅包含一个对象成员的数组：

```js
describe("Filter function", () => {
  test("it should filter by a search term (link)", () => {
    const input = [
      { id: 1, url: "https://www.url1.dev" },
      { id: 2, url: "https://www.url2.dev" },
      { id: 3, url: "https://www.link3.dev" }
    ];

    const output = [{ id: 3, url: "https://www.link3.dev" }];
  });
});
```

现在可以写实际测试代码了。我们要用到 Jest 的 **expect** 函数和 **匹配器（matcher）** 来检查我们假想的（当前是）函数调用时是否返回预期结果。下面给出了代码:

```js
expect(filterByTerm(input, "link")).toEqual(output);
```

或者将代码分解，调用函数的部分单拎出来：

```js
filterByTerm(input, "link");
```

在 Jest 测试中，我们把测试函数包装在 **expect** 里面，并且搭配 **匹配器** （用来检查输入的 Jest 函数）一起使用，来完成测试。下面列出了完整测试代码：

```js
describe("Filter function", () => {
  test("it should filter by a search term (link)", () => {
    const input = [
      { id: 1, url: "https://www.url1.dev" },
      { id: 2, url: "https://www.url2.dev" },
      { id: 3, url: "https://www.link3.dev" }
    ];

    const output = [{ id: 3, url: "https://www.link3.dev" }];

    expect(filterByTerm(input, "link")).toEqual(output);

  });
});
```
现在，运行一波测试：
```bash
$ npm test
```

你会看到测试失败了:

```bash
FAIL  tests/filterByTerm.spec.js
  Filter function
    ✕ it should filter by a search term (link) (3 ms)

  ● Filter function › it should filter by a search term (link)

    ReferenceError: filterByTerm is not defined

       9 |     const output = [{ id: 3, url: "https://www.link3.dev" }];
      10 | 
    > 11 |     expect(filterByTerm(input, "link")).toEqual(output);
         |     ^
      12 | 
      13 |   });
      14 | });

      at Object.<anonymous> (tests/filterByTerm.spec.js:11:5)

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 total
Snapshots:   0 total
Time:        3.232 s
```
“`ReferenceError: filterByTerm is not defined`”. 意思很明显啦，没有定义 **filterByTerm**，接下来我们来修复它。

### 七，修复测试（并再一次测试失败）
我们还没实现 **filterByTerm** 呢。为了方便，我们把这个函数的定义跟咱们的测试用例放在一起。当然，**在实际新项目中，测试用例和要测试的函数往往是为了不同文件中的，测试函数的时候是需要从别的文件引入的**。

filterByTerm 函数内部，需要借助原生的数组方法 filter 实现，来过滤出我们需要的成员：

```js
function filterByTerm(inputArr, searchTerm) {
  return inputArr.filter(function(arrayElement) {
    return arrayElement.url.match(searchTerm);
  });
}
```

说明下函数的工作原理：我们检查输入数组里的每个对象成员的“url”属性值，是否与 match 方法里的正则表达式匹配。下面是完整代码:

```js
function filterByTerm(inputArr, searchTerm) {
  return inputArr.filter(function(arrayElement) {
    return arrayElement.url.match(searchTerm);
  });
}

describe("Filter function", () => {
  test("it should filter by a search term (link)", () => {
    const input = [
      { id: 1, url: "https://www.url1.dev" },
      { id: 2, url: "https://www.url2.dev" },
      { id: 3, url: "https://www.link3.dev" }
    ];

    const output = [{ id: 3, url: "https://www.link3.dev" }];

    expect(filterByTerm(input, "link")).toEqual(output);
  });
});
```

再次运行测试 `npm test`

```bash
PASS  tests/filterByTerm.spec.js
  Filter function
    ✓ it should filter by a search term (link) (5 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        3.049 s
Ran all test suites.
```

测试通过！

很棒。但是完了吗？还没。怎样让函数再次调用失败呢？接下里，我们用大写的搜索项调用下函数：

```js
function filterByTerm(inputArr, searchTerm) {
  return inputArr.filter(function(arrayElement) {
    return arrayElement.url.match(searchTerm);
  });
}

describe("Filter function", () => {
  test("it should filter by a search term (link)", () => {
    const input = [
      { id: 1, url: "https://www.url1.dev" },
      { id: 2, url: "https://www.url2.dev" },
      { id: 3, url: "https://www.link3.dev" }
    ];

    const output = [{ id: 3, url: "https://www.link3.dev" }];

    expect(filterByTerm(input, "link")).toEqual(output);

    expect(filterByTerm(input, "LINK")).toEqual(output); // New test

  });
});
```

执行测试……嗯，失败了。来吧，我们再来修复下。


### 八，修复测试：兼容大写搜索项
**filterByTerm** 应该也要把大写搜索项考虑进去。也就是说，即使是搜索内容是大写的，也要以忽略大小写的形式返回对应的匹配对象。

```js
filterByTerm(inputArr, "link");
filterByTerm(inputArr, "LINK");
```

为了测试这种状况，我们需要引入一个新的测试：

```js
expect(filterByTerm(input, "LINK")).toEqual(output); // New test
```
为了通过测试，我们需要稍微调整下 `match` 方法的正则表达式：

```js
function filterByTerm(inputArr, searchTerm) {
  const regex = new RegExp(searchTerm, "i");
  return inputArr.filter(function(arrayElement) {
    return arrayElement.url.match(regex);
  });
}
```

完整代码如下:

```js
describe("Filter function", () => {
  test("it should filter by a search term (link)", () => {
    const input = [
      { id: 1, url: "https://www.url1.dev" },
      { id: 2, url: "https://www.url2.dev" },
      { id: 3, url: "https://www.link3.dev" }
    ];

    const output = [{ id: 3, url: "https://www.link3.dev" }];

    expect(filterByTerm(input, "link")).toEqual(output);

    expect(filterByTerm(input, "LINK")).toEqual(output);
  });
});

function filterByTerm(inputArr, searchTerm) {
  const regex = new RegExp(searchTerm, "i");
  return inputArr.filter(function(arrayElement) {
    return arrayElement.url.match(regex);
  });
}
```

执行测试后，会看到通过了。
作为联系，你可以写一个新的测试来检查下列条件：
1. 测试如果搜索项为"`uRl`"的情况
2. 测试空搜索项。函数如何去处理它？


### 九，代码覆盖率
什么是**代码覆盖率**？在谈论这个之前，我们先对代码做下调整。在项目根目录下创建一个名为 **src** 的文件夹，再在里面创建一个名为 **filterByTerm.js** 的文件。我们在这里 **export** 出这个函数：

```js
function filterByTerm(inputArr, searchTerm) {
  if (!searchTerm) throw Error("searchTerm cannot be empty");
  const regex = new RegExp(searchTerm, "i");
  return inputArr.filter(function(arrayElement) {
    return arrayElement.url.match(regex);
  });
}

module.exports = filterByTerm;
```

现在假设我是你们公司新来的同事。我对测试一无所知，在不清楚我们开发环境的情况下，我在这个函数里加了一个 **if 语句**：

```js
function filterByTerm(inputArr, searchTerm) {
  if (!searchTerm) throw Error("searchTerm cannot be empty");
  if (!inputArr.length) throw Error("inputArr cannot be empty"); // new line
  const regex = new RegExp(searchTerm, "i");
  return inputArr.filter(function(arrayElement) {
    return arrayElement.url.match(regex);
  });
}

module.exports = filterByTerm;
```

我们在 **filterByTerm** 里加了一行新代码，但没有被测试。除非我告诉你“这里有个新语句需要测试”，你是不会知道要测试什么的。几乎不可能知道我们的代码会走的所有路径，因此**需要一种工具来帮助我们发现这些盲点**。

这种工具称为**代码覆盖率**,它是我们工具箱里的一个强大工具。Jest 内置了代码覆盖率工具，你可以使用两种方式激活它：
1. 在命令行中通过"`–coverage`"指定
2. 在`package.json`中手动配置


再执行覆盖率测试之前，确保在 **tests/filterByTerm.spec.js** 中 引入了 **filterByTerm** 函数。

执行覆盖率测试：
```bash
$ npm test -- --coverage
```

结果如下:

```bash
PASS  tests/filterByTerm.spec.js
  Filter function
    ✓ it should filter by a search term (link) (8 ms)

-----------------|---------|----------|---------|---------|-------------------
File             | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s 
-----------------|---------|----------|---------|---------|-------------------
All files        |      75 |       50 |     100 |     100 |                   
 filterByTerm.js |      75 |       50 |     100 |     100 | 2-3               
-----------------|---------|----------|---------|---------|-------------------
Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        3.133 s
Ran all test suites.
```

这是对我们函数测试覆盖率的一个很好的总结。我们看见**第 2、3 行没有覆盖**。现在来测试我新添加的 if 语句，来达到 100% 的代码覆盖率。

完整代码如下:

```js
const filterByTerm = require('../src/filterByTerm');

describe("Filter function", () => {
  const input = [
    { id: 1, url: "https://www.url1.dev" },
    { id: 2, url: "https://www.url2.dev" },
    { id: 3, url: "https://www.link3.dev" }
  ];

  test("it should filter by a search term (link)", () => {
    const output = [{ id: 3, url: "https://www.link3.dev" }];

    expect(filterByTerm(input, "link")).toEqual(output);

    expect(filterByTerm(input, "LINK")).toEqual(output);
  });

  test("执行搜索项为 uRl", () => {
    const output = [
      { id: 1, url: "https://www.url1.dev" },
      { id: 2, url: "https://www.url2.dev" }
    ];

    expect(filterByTerm(input, "uRl")).toEqual(output);
  })

  test("过滤 searchTerm 为空字符串", () => {
    const input = [];
    expect(() => {
      filterByTerm(input, "");
    }).toThrowError(Error("searchTerm cannot be empty"));
  })

  test("过滤 input 为空数组", () => {
    const input = [];
    expect(() => {
      filterByTerm(input, "link");
    }).toThrowError(Error("inputArr cannot be empty"));
  })
});
```

执行结果如下：

```bash
PASS  tests/filterByTerm.spec.js
  Filter function
    ✓ it should filter by a search term (link) (49 ms)
    ✓ 执行搜索项为 uRl (1 ms)
    ✓ 过滤 searchTerm 为空字符串 (28 ms)
    ✓ 过滤 input 为空数组 (1 ms)

-----------------|---------|----------|---------|---------|-------------------
File             | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s 
-----------------|---------|----------|---------|---------|-------------------
All files        |     100 |      100 |     100 |     100 |                   
 filterByTerm.js |     100 |      100 |     100 |     100 |                   
-----------------|---------|----------|---------|---------|-------------------
Test Suites: 1 passed, 1 total
Tests:       4 passed, 4 total
Snapshots:   0 total
Time:        3.076 s
Ran all test suites.
```

如果想要在每次测试的时候，都要做代码覆盖率检查，可以在 package.json 对 jest 做出如下配置：

```json
"scripts": {
  "test": "jest"
},
"jest": {
  "collectCoverage": true
},
```

### 十，写在末尾
- 本文转载自 [掘金-Jest 入门教程](https://juejin.im/post/6844904030972411912)
- [gitHub 源码](https://github.com/zhangkai0621/started-with-jest)