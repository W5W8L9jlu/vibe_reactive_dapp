---
timezone: UTC+8
---

# W5W8L9jlu

**GitHub ID:** W5W8L9jlu

**Telegram:**

## Self-introduction

Let’s vibe Reactive dApp

## Notes

<!-- Content_START -->
# 2026-03-14
<!-- DAILY_CHECKIN_2026-03-14_START -->


---

# solidity语法基础回顾（啃basic demo在回顾一下吧

<aside>
💡

https://github.com/CryptozombiesHQ/cryptozombies-lesson-code

</aside>

## **版本指令**

所有的 Solidity 源码都必须冠以 "version pragma" — 标明 Solidity 编译器的版本. 以避免将来新的编译器可能破坏你的代码。

例如: `pragma solidity ^0.4.19;` (当前 Solidity 的最新版本是 0.4.19).

综上所述， 下面就是一个最基本的合约 — 每次建立一个新的项目时的第一段代码:

```
pragma solidity ^0.4.19;

contract HelloWorld {

}
```

## **状态变量和整数**

***状态变量***是被永久地保存在合约中。也就是说它们被写入以太币区块链中. 想象成写入一个数据库。

### 例子:

```solidity
contract Example{
  // 这个无符号整数将会永久的被保存在区块链中
  uint myUnsignedInteger = 100;
}
```

在上面的例子中，定义 `myUnsignedInteger` 为 `uint` 类型，并赋值100。

## **数学运算**

在 Solidity 中，数学运算很直观明了，与其它程序设计语言相同:

- 加法: `x + y`
- 减法: `x - y`,
- 乘法: `x * y`
- 除法: `x / y`
- 取模 / 求余: `x % y` *(例如, `13 % 5` 余 `3`, 因为13除以5，余3)*

Solidity 还支持 ***乘方操作*** (如：x 的 y次方） // 例如： 5 ** 2 = 25

```
uint x = 5 ** 2; // equal to 5^2 = 25
```

## **结构体**

有时你需要更复杂的数据类型，Solidity 提供了 **结构体**:

```csharp
struct Person {
  uint age;
  string name;
}
```

结构体允许你生成一个更复杂的数据类型，它有多个属性。

> *注：我们刚刚引进了一个新类型, `string`。 字符串用于保存任意长度的 UTF-8 编码数据。 如： `string greeting = "Hello world!"`。*
> 

## **数组**

如果你想建立一个集合，可以用 **_数组_**这样的数据类型. Solidity 支持两种数组: **_静态_** 数组和**_动态_** 数组:

```
// 固定长度为2的uint类型静态数组:
uint[2] fixedArray;
// 固定长度为5的string类型的静态数组:
string[5] stringArray;
// uint类型动态数组，长度不固定，可以动态添加元素:
uint[] dynamicArray;
```

你也可以建立一个 ***结构体***类型的数组 例如，上一章提到的 `Person`:

```
Person[] people; // 这是类型为结构体（或者说Person）的名为people的动态数组，可以不断添加元素
```

记住：状态变量被永久保存在区块链中。所以在你的合约中创建动态数组来保存成结构的数据是非常有意义的。

## **公共数组**

你可以定义 `public` 数组, Solidity 会自动创建 ***getter*** 方法. 语法如下:

```
Person[] public people;
```

其它的合约可以从这个数组读取数据（但不能写入数据），所以这在合约中是一个有用的保存公共数据的模式。

## **定义函数**

在 Solidity 中函数定义的句法如下:

```
function eatHamburgers(string _name, uint _amount) {

}//函数 eatHamburgers 有两个参数，分别是 string 类型的 _name 和 unit 类型的 _amount
```

这是一个名为 `eatHamburgers` 的函数，它接受两个参数：一个 `string`类型的 和 一个 `uint`类型的。现在函数内部还是空的。

> *注：: 习惯上函数里的变量都是以(`_`)开头 (但不是硬性规定) 以区别全局变量。我们整个教程都会沿用这个习惯。*
> 

我们的函数定义如下:

```
eatHamburgers("vitalik", 100);
```

## **创建新的结构体**

还记得上个例子中的 `Person` 结构体：

```csharp
struct Person {
  uint age;
  string name;
}

Person[] public people;
```

现在创建新的 `Person` 结构，然后把它加入到名为 `people` 的数组中.

```solidity
// 创建一个新的Person:
Person satoshi = Person(172, "Satoshi");

// 将新创建的satoshi添加进people数组:
people.push(satoshi);
```

你也可以两步并一步，用一行代码更简洁:

```solidity
people.push(Person(16, "Vitalik"));
```

> *注：`array.push()` 在数组的 **尾部** 加入新元素 ，所以元素在数组中的顺序就是我们添加的顺序， 如:*
> 

```solidity
uint[] numbers;
numbers.push(5);
numbers.push(10);
numbers.push(15);
// The `numbers` array is now equal to [5, 10, 15]
```

## **私有 / 公共函数**

Solidity 定义的函数的属性默认为`公共`。 这就意味着任何一方 (或其它合约) 都可以调用你合约里的函数。

显然，不是什么时候都需要这样，而且这样的合约易于受到攻击。 所以将自己的函数定义为`私有`是一个好的编程习惯，只有当你需要外部世界调用它时才将它设置为`公共`。

如何定义一个私有的函数呢？

```solidity
uint[] numbers;

function _addToArray(uint _number) private{
  numbers.push(_number);
}
```

这意味着只有我们合约中的其它函数才能够调用这个函数，给 `numbers` 数组添加新成员。

> 可以看到，在函数名字后面使用关键字 `private` 即可。和函数的参数类似，私有函数的名字用(`_`)起始。
> 

## **返回值**

要想函数返回一个数值，按如下定义：

```solidity
string greeting = "What's up dog";

function sayHello() public returns (string){
  return greeting;
}
```

Solidity 里，函数的定义里可包含返回值的数据类型(如本例中 `string`)。

## **函数的修饰符**

上面的函数实际上没有改变 Solidity 里的状态，即，它没有改变任何值或者写任何东西。

这种情况下我们可以把函数定义为 ***view***, 意味着它**只能读取数据不能更改数据:**

```solidity
function sayHello() public view returns (string){
```

Solidity 还支持 ***pure*** 函数, 表明这个函数甚至都**不访问应用里的数据**，例如：

```solidity
function _multiply(uint a, uint b) private pure returns (uint){
  return a * b;
}
```

这个函数甚至都不读取应用里的状态 — 它的返回值**完全取决于它的输入参数**，在这种情况下我们把函数定义为 ***pure***.

> *注：可能很难记住何时把函数标记为 pure/view。 幸运的是， Solidity 编辑器会给出提示，提醒你使用这些修饰符。*
> 

## **Keccak256**

如何让 `_generateRandomDna` 函数返回一个全(半) 随机的 `uint`?

Ethereum 内部有一个散列函数`keccak256`，它用了SHA3版本。一个散列函数基本上就是**把一个字符串转换为一个256位的16进制数字**。字符串的一个微小变化会引起散列数据极大变化。

这在 Ethereum 中有很多应用，但是现在我们只是用它造一个伪随机数。

例子:

```
//6e91ec6b618bb462a4a6ee5aa2cb0e9cf30f7a052bb467b0ba58b8748c00d2e5
keccak256("aaaab");
//b1f078126895a1424524de5321b339ab00408010b7cf0e6ed451514981e58aa9
keccak256("aaaac");
```

显而易见，输入字符串只改变了一个字母，输出就已经天壤之别了。

> *注: 在区块链中安全地产生一个随机数是一个很难的问题， 本例的方法不安全，但是在我们的Zombie DNA算法里不是那么重要，已经很好地满足我们的需要了。*
> 

## **类型转换**

有时你需要变换数据类型。例如:

```solidity
uint8 a = 5;
uint b = 6;
// 将会抛出错误，因为 a * b 返回 uint, 而不是 uint8:
uint8 c = a * b;
// 我们需要将 b 转换为 uint8:
uint8 c = a * uint8(b);
```

上面, `a * b` 返回类型是 `uint`, 但是当我们尝试用 `uint8` 类型接收时, 就会造成潜在的错误。如果把它的数据类型转换为 `uint8`, 就可以了，编译器也不会出错。

## **事件（event）**

**事件** 是合约和区块链通讯的一种机制。你的前端应用“监听”某些事件，并做出反应。

例子:

```solidity
// 这里建立事件
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public{
  uint result = _x + _y;
  //触发事件，通知app
  IntegersAdded(_x, _y, result);
  return result;
}
```

你的 app 前端可以监听这个事件。JavaScript 实现如下:

```solidity
YourContract.IntegersAdded(function(error, result){
  // 干些事
})
```

<aside>
💡

存疑：{ } 外不需 ；

</aside>

## **Addresses （地址）**

以太坊区块链由 **_ account _** (账户)组成，你可以把它想象成银行账户。一个帐户的余额是 **_以太_** （在以太坊区块链上使用的币种），你可以和其他帐户之间支付和接受以太币，就像你的银行帐户可以电汇资金到其他银行帐户一样。

每个帐户都有一个“地址”，你可以把它想象成银行账号。这是账户唯一的标识符，它看起来长这样：

`0x0cE446255506E92DF41614C46F1d6df9Cc969183` 

**地址属于特定用户（或智能合约）**

## **Mapping（映射）**

**除了 _ 结构体 _** 和 **_ 数组 _ ，** **_映射_** 是另一种在 Solidity 中存储有组织数据的方法。

映射是这样定义的：

```solidity
//对于金融应用程序，将用户的余额保存在一个 uint类型的变量中：
mapping (address => uint) public accountBalance;
//或者可以用来通过userId 存储/查找的用户名
mapping (uint => string) userIdToName;
```

映射本质上是存储和查找数据所用的键-值对。在第一个例子中，键是一个 `address`，值是一个 `uint`，在第二个例子中，键是一个`uint`，值是一个 `string`。

## **msg.sender**

在 Solidity 中，有一些全局变量可以被所有函数调用。 其中一个就是 `msg.sender`，它指的是当前调用者（或智能合约）的 `address`。

> *注意：在 Solidity 中，功能执行始终需要从外部调用者开始。 一个合约只会在区块链上什么也不做，除非有人调用其中的函数。所以 `msg.sender`总是存在的。*
> 

以下是使用 `msg.sender` 来更新 `mapping` 的例子：

```solidity
mapping (address => uint) favoriteNumber;

function setMyNumber(uint _myNumber) public{
  // 更新我们的 `favoriteNumber` 映射来将 `_myNumber`存储在 `msg.sender`名下
  favoriteNumber[msg.sender] = _myNumber;
  // 存储数据至映射的方法和将数据存储在数组相似
}

function whatIsMyNumber() public view returns (uint){
  // 拿到存储在调用者地址名下的值
  // 若调用者还没调用 setMyNumber， 则值为 `0`
  return favoriteNumber[msg.sender];
}
```

在这个小小的例子中，任何人都可以调用 `setMyNumber` 在我们的合约中存下一个 `uint` 并且与他们的地址相绑定。 然后，他们调用 `whatIsMyNumber` 就会返回他们存储的 `uint`。

使用 `msg.sender` 很安全，因为它具有以太坊区块链的安全保障 —— 除非窃取与以太坊地址相关联的私钥，否则是没有办法修改其他人的数据的。

跟在 JavaScript 中一样， 在 Solidity 中你也可以用 `++` 使 `uint` 递增。

```solidity
uint number = 0;
number++;
// `number` 现在是 `1`了
```

*注意：在 Solidity 中，关键词放置的顺序并不重要*

# **Require**

在 `require`使得函数在执行过程中，当不满足某些条件时抛出错误，并停止执行：

```solidity
function sayHiToVitalik(string _name) public returns (string){
  // 比较 _name 是否等于 "Vitalik". 如果不成立，抛出异常并终止程序
  // (敲黑板: Solidity 并不支持原生的字符串比较, 我们只能通过比较
  // 两字符串的 keccak256 哈希值来进行判断)
  require(keccak256(_name) == keccak256("Vitalik"));
  // 如果返回 true, 运行如下语句
  return "Hi!";
}
```

如果你这样调用函数 `sayHiToVitalik（“Vitalik”）` ,它会返回“Hi！”。而如果调用的时候使用了其他参数，它则会抛出错误并停止执行。

因此，在调用一个函数之前，用 `require` 验证前置条件是非常有必要的。

## **继承（Inheritance）**

有个让 Solidity 的代码易于管理的功能，就是合约 ***inheritance*** (继承)：

```solidity
contract Doge{
  function catchphrase() public returns (string){
    return "So Wow CryptoDoge";
  }
}

contract BabyDoge is Doge{
  function anotherCatchphrase() public returns (string){
    return "Such Moon BabyDoge";
  }
}
```

由于 `BabyDoge` 是从 `Doge` 那里 ***inherits*** （继承)过来的。 这意味着当你编译和部署了 `BabyDoge`，它将可以访问 `catchphrase()` 和 `anotherCatchphrase()`和其他我们在 `Doge` 中定义的其他**公共函数**。

这可以用于逻辑继承（比如表达子类的时候，`Cat` 是一种 `Animal`）。 但也可以简单地将类似的逻辑组合到不同的合约中以组织代码。

## **引入（Import）**

Solidity 中，当你有多个文件并且想**把一个文件导入另一个文件**时，可以使用 `import` 语句：

```
import "./someothercontract.sol";

contract newContract is SomeOtherContract {

}
```

这样当我们在合约（contract）目录下有一个名为 `someothercontract.sol` 的文件（ `./` 就是同一目录的意思），它就会被编译器导入。

## ***Storage*** & ***Memory***

***Storage*** 变量是指**永久存储在区块链中的变量**。 ***Memory*** 变量则是**临时的**，当**外部函数对某合约调用完成时，内存型变量即被移除**。 你可以把它想象成存储在你电脑的硬盘或是RAM中数据的关系。

大多数时候你都用不到这些关键字，默认情况下 Solidity 会自动处理它们。 状态变量（在函数之外声明的变量）默认为“存储”形式，并永久写入区块链；而在函数内部声明的变量是“内存”型的，它们函数调用结束后消失。

然而也有一些情况下，你需要手动声明存储类型，主要用于处理函数内的 **_ 结构体 _** 和 **_ 数组 _** 时：

```solidity
contract SandwichFactory{
  struct Sandwich {
    string name;
    string status;
  }

  Sandwich[] sandwiches;

  function eatSandwich(uint _index) public{
    // Sandwich mySandwich = sandwiches[_index];

    // ^ 看上去很直接，不过 Solidity 将会给出警告
    // 告诉你应该明确在这里定义 `storage` 或者 `memory`。

    // 所以你应该明确定义 `storage`:
    Sandwich storage mySandwich = sandwiches[_index];
    // ...这样 `mySandwich` 是指向 `sandwiches[_index]`的指针
    // 在存储里，另外...
    mySandwich.status = "Eaten!";
    // ...这将永久把 `sandwiches[_index]` 变为区块链上的存储

    // 如果你只想要一个副本，可以使用`memory`:
    Sandwich memory anotherSandwich = sandwiches[_index + 1];
    // ...这样 `anotherSandwich` 就仅仅是一个内存里的副本了
    // 另外
    anotherSandwich.status = "Eaten!";
    // ...将仅仅修改临时变量，对 `sandwiches[_index + 1]` 没有任何影响
    // 不过你可以这样做:
    sandwiches[_index + 1] = anotherSandwich;
    // ...如果你想把副本的改动保存回区块链存储
  }
}
```

## **internal 和 external**

除 `public` 和 `private` 属性之外，Solidity 还使用了另外两个描述函数可见性的修饰词：`internal`（内部） 和 `external`（外部）。

`internal` 和 `private` 类似，不过， 如果某个合约继承自其父合约，这个合约即**可以访问父合约中定义的“内部”函数**。

`external` 与`public` 类似，只不过这些函数**只能在合约之外调用** - 它们不能被合约内的其他函数调用。

声明函数 `internal` 或 `external` 类型的语法，与声明 `private` 和 `public`类 型相同：

```solidity
contract Sandwich{
  uint private sandwichesEaten = 0;

  function eat() internal{
    sandwichesEaten++;
  }
}

contract BLT is Sandwich{
  uint private baconSandwichesEaten = 0;

  function eatWithBacon() public returns (string){
    baconSandwichesEaten++;
    // 因为eat() 是internal 的，所以我们能在这里调用
    eat();
  }
}
```

## ***interface*** (接口)

如果我们的合约需要和区块链上的其他的合约会话，则需先定义一个 ***interface*** (接口)。

先举一个简单的栗子。 假设在区块链上有这么一个合约：

```solidity
contract LuckyNumber{
  mapping(address => uint) numbers;

  function setNum(uint _num) public{
    numbers[msg.sender] = _num;
  }

  function getNum(address _myAddress) public view returns (uint){
    return numbers[_myAddress];
  }
}
```

这是个很简单的合约，您可以用它存储自己的幸运号码，并将其与您的以太坊地址关联。 这样其他人就可以通过您的地址查找您的幸运号码了。

现在假设我们有一个外部合约，使用 `getNum` 函数可读取其中的数据。

首先，我们定义 `LuckyNumber` 合约的 ***interface*** ：

```solidity
contract NumberInterface{
  function getNum(address _myAddress) public view returns (uint);
}
```

请注意，这个过程虽然看起来像在定义一个合约，但其实内里不同：

首先，我们只声明了要与之交互的函数 —— 在本例中为 `getNum` —— 在其中我们没有使用到任何其他的函数或状态变量。

其次，我们并没有使用大括号（`{` 和 `}`）定义函数体，我们单单用分号（`;`）结束了函数声明。这使它看起来像一个合约框架。

编译器就是靠这些特征认出它是一个接口的。

在我们的 app 代码中使用这个接口，合约就知道其他合约的函数是怎样的，应该如何调用，以及可期待什么类型的返回值。

> 
> 
> 
> ***public/externa*l vs *interface***
> 
> ```
> public/external
> ```
> 
> 解决的是：
> 
> ```
> 函数能不能被调用,往往你需要知道函数源码（函数体的内容）
> ```
> 
> 而 interface 解决的是：
> 
> ```
> 在没有源码的情况下如何调用别人的合约
> ```
> 

继续前面 `NumberInterface` 的例子，我们既然将接口定义为：

```solidity
contract NumberInterface{
  function getNum(address _myAddress) public view returns (uint);
}
```

我们可以在合约中这样使用：

```solidity
contract MyContract{
  address NumberInterfaceAddress = 0xab38...;
  // ^ 这是FavoriteNumber合约在以太坊上的地址
  NumberInterface numberContract = NumberInterface(NumberInterfaceAddress);
  // 现在变量 `numberContract` 指向另一个合约对象

  function someFunction() public{
    // 现在我们可以调用在那个合约中声明的 `getNum`函数:
    uint num = numberContract.getNum(msg.sender);
    // ...在这儿使用 `num`变量做些什么
  }
}
```

通过这种方式，只要将您合约的可见性设置为`public`(公共)或`external`(外部)，它们就可以与以太坊区块链上的任何其他合约进行交互。

## **处理多返回值**

`getKitty` 是我们所看到的第一个返回多个值的函数。我们来看看是如何处理的：

```solidity
function multipleReturns() internal returns(uint a, uint b, uint c){
  return (1, 2, 3);
}

function processMultipleReturns() external{
  uint a;
  uint b;
  uint c;
  // 这样来做批量赋值:
  (a, b, c) = multipleReturns();//意思就是：a = 1，b = 2，c = 3
}

// 或者如果我们只想返回其中一个变量:
function getLastReturnValue() external{
  uint c;
  // 可以对其他字段留空:
  (,,c) = multipleReturns();
}
```

## **if 语句**

if语句的语法在 Solidity 中，与在 JavaScript 中差不多：

```solidity
function eatBLT(string sandwich) public{
  // 看清楚了，当我们比较字符串的时候，需要比较他们的 keccak256 哈希码
  if (keccak256(sandwich) == keccak256("BLT")) {
    eat();
  }
}
```

## **智能协议的永固性**

到现在为止，我们讲的 Solidity 和其他语言没有质的区别，它长得也很像 JavaScript。

但是，在有几点以太坊上的 DApp 跟普通的应用程序有着天壤之别。

第一个例子，在你把智能协议传上以太坊之后，它就变得***不可更改***, 这种永固性意味着你的代码永远不能被调整或更新。

你编译的程序会一直，永久的，不可更改的，存在以太坊上。这就是 Solidity 代码的安全性如此重要的一个原因。如果你的智能协议有任何漏洞，即使你发现了也无法补救。你只能让你的用户们放弃这个智能协议，然后转移到一个新的修复后的合约上。

但这恰好也是智能合约的一大优势。代码说明一切。如果你去读智能合约的代码，并验证它，你会发现，一旦函数被定义下来，每一次的运行，程序都会严格遵照函数中原有的代码逻辑一丝不苟地执行，完全不用担心函数被人篡改而得到意外的结果

## hard code（硬编码）

### 硬编码

```
uint fee = 100;
```

手续费永远 100。

### 非硬编码

```
uint public fee;

function setFee(uint _fee) public {
    fee = _fee;
}
```

这里手续费可以：

```
随时修改
```

不是写死的。

## **OpenZeppelin库的`Ownable` 合约**

下面是一个 `Ownable` 合约的例子： 来自 **_ OpenZeppelin _** Solidity 库的 `Ownable` 合约。 OpenZeppelin 是主打安保和社区审查的智能合约库，您可以在自己的 DApps中引用。

**`Ownable`** 合约**：给智能合约加一个“管理员系统”，只有管理员才能执行某些操作，并且管理员可以转让。**

把楼下这个合约读读通：

```solidity
/**
 * @title Ownable
 * @dev The Ownable contract has an owner address, and provides basic authorization control
 * functions, this simplifies the implementation of "user permissions".
 */
contract Ownable{
  address public owner;
  event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);

  /**
   * @dev The Ownable constructor sets the original `owner` of the contract to the sender
   * account.
   */
  function Ownable() public{
    owner = msg.sender;
  }

  /**
   * @dev Throws if called by any account other than the owner.
   */
  modifier onlyOwner(){
    require(msg.sender == owner);
    _;
  }

  /**
   * @dev Allows the current owner to transfer control of the contract to a newOwner.
   * @param newOwner The address to transfer ownership to.
   */
  function transferOwnership(address newOwner) public onlyOwner{
    require(newOwner != address(0));
    OwnershipTransferred(owner, newOwner);
    owner = newOwner;
  }
}
```

- 构造函数：`function Ownable()`是一个 **_ constructor_** (构造函数)，构造函数不是必须的，它与合约同名，**构造函数一生中唯一的一次执行，就是在合约最初被创建的时候**。现在的新版solidity，一般写为：

```
constructor() {
    owner = msg.sender;
}
```

- 函数修饰符：`modifier onlyOwner()`。 修饰符跟函数很类似，不过是用来修饰其他已有函数用的， **在其他语句执行前，为它检查下先验条件**。 在这个例子中，我们就可以写个修饰符 `onlyOwner` 检查下调用者，确保只有合约的主人才能运行本函数。奇怪的`_;，`表示**继续执行原函数**。具体而言，当你调用 `transferOwnership` 时，首先执行 `onlyOwner` 中的代码， 执行到 `onlyOwner` 中的 `_`; 语句时，程序再返回并执行 `transferOwnership` 中的代码。
- `indexed` 关键字：给日志**加索引**，方便别人查记录。

所以`Ownable` 合约基本都会这么干：

1. 合约创建，构造函数先行，将其 `owner` 设置为`msg.sender`（其部署者）
2. 为它加上一个修饰符 `onlyOwner`，它会限制陌生人的访问，将访问某些函数的权限锁定在 `owner` 上。
3. 允许将合约所有权转让给他人。

`onlyOwner` 简直人见人爱，大多数人开发自己的 Solidity DApps，都是从复制/粘贴 `Ownable` 开始的，从它再继承出的子类，并在之上进行功能开发。

## GAS

### **为什么要用 *gas* 来驱动？**

以太坊就像一个巨大、缓慢、但非常安全的电脑。当你运行一个程序的时候，网络上的每一个节点都在进行相同的运算，以验证它的输出 —— 这就是所谓的“去中心化” 由于数以千计的节点同时在验证着每个功能的运行，这可以确保它的数据不会被被监控，或者被刻意修改。

可能会有用户用无限循环堵塞网络，抑或用密集运算来占用大量的网络资源，为了防止这种事情的发生，以太坊的创建者为以太坊上的资源制定了价格，想要在以太坊上运算或者存储，你需要先付费。

> *注意：如果你使用侧链，倒是不一定需要付费。*
> 

### **省 gas 的招数：结构封装 （Struct packing）**

除了基本版的 `uint` 外，还有其他变种 `uint`：`uint8`，`uint16`，`uint32`等。

通常情况下我们不会考虑使用 `uint` 变种，因为无论如何定义 `uint`的大小，Solidity 为它保留256位的存储空间。例如，使用 `uint8` 而不是`uint`（`uint256`）不会为你节省任何 gas。

除非，把 `uint` 绑定到 `struct` 里面。

如果一个 `struct` 中有多个 `uint`，则尽可能使用较小的 `uint`, Solidity 会将这些 `uint` 打包在一起，从而占用较少的存储空间。例如：

```solidity
struct NormalStruct {
  uint a;
  uint b;
  uint c;
}

struct MiniMe {
  uint32 a;
  uint32 b;
  uint c;
}

// 因为使用了结构打包，`mini` 比 `normal` 占用的空间更少
NormalStruct normal = NormalStruct(10, 20, 30);
MiniMe mini = MiniMe(10, 20, 30);
```

所以，当 `uint` 定义在一个 `struct` 中的时候，尽量使用最小的整数子类型以节约空间。 并且把同样类型的变量放一起（即在 struct 中将把变量按照类型依次放置），这样 Solidity 可以将存储空间最小化。例如，有两个 `struct`：

`uint c; uint32 a; uint32 b;` 和 `uint32 a; uint c; uint32 b;`

前者比后者需要的gas更少，因为前者把`uint32`放一起了。

## **时间单位**

Solidity 使用自己的本地时间单位。

变量 `now` 将返回当前的unix时间戳（自1970年1月1日以来经过的秒数）。我写这句话时 unix 时间是 `1515527488`。

> *注意：Unix时间传统用一个32位的整数进行存储。这会导致“2038年”问题，当这个32位的unix时间戳不够用，产生溢出，使用这个时间的遗留系统就麻烦了。所以，如果我们想让我们的 DApp 跑够20年，我们可以使用64位整数表示时间，但为此我们的用户又得支付更多的 gas。真是个两难的设计啊！*
> 

Solidity 还包含`秒(seconds)`，`分钟(minutes)`，`小时(hours)`，`天(days)`，`周(weeks)` 和 `年(years)` 等时间单位。它们都会转换成对应的秒数放入 `uint` 中。所以 `1分钟` 就是 `60`，`1小时`是 `3600`（60秒×60分钟），`1天`是`86400`（24小时×60分钟×60秒），以此类推。

下面是一些使用时间单位的实用案例：

```solidity
uint lastUpdated;

// 将‘上次更新时间’ 设置为 ‘现在’
function updateTimestamp() public{
  lastUpdated = now;
}

// 如果到上次`updateTimestamp` 超过5分钟，返回 'true'
// 不到5分钟返回 'false'
function fiveMinutesHavePassed() public view returns (bool){
  return (now >= (lastUpdated + 5 minutes));
}
```

## **storage（将结构体作为参数传入）**

由于结构体的存储指针可以以参数的方式传递给一个 `private` 或 `internal` 的函数，因此结构体可以在多个函数之间相互传递。

遵循这样的语法：

```
function _doStuff(Zombie storage _zombie) internal {
  // do stuff with _zombie
}
```

_zombie 不是新变量，而是指向原来 Zombie 数据的“引用”，改它就等于改原数据。

Solidity 使用storage(存储)是相当昂贵的，”写入“操作尤其贵。这是因为，无论是写入还是更改一段数据， 这都将永久性地写入区块链。需要在全球数千个节点的硬盘上存入这些数据，随着区块链的增长，拷贝份数更多，存储量也就越大。

为了降低成本，不到万不得已，避免将数据写入存储。这也会导致效率低下的编程逻辑 - 比如每次调用一个函数，都需要在 memory(内存) 中重建一个数组，而不是简单地将上次计算的数组给存储下来以便快速查找。

在大多数编程语言中，遍历大数据集合都是昂贵的。但是在 Solidity 中，使用一个标记了external view的函数，遍历比 storage 要便宜太多，因为 view 函数不会产生任何花销。

## **带参数的函数修饰符**

之前我们已经读过一个简单的函数修饰符了：`onlyOwner`。函数修饰符也可以带参数。例如：

```solidity
// 存储用户年龄的映射
mapping (uint => uint) public age;

// 限定用户年龄的修饰符
modifier olderThan(uint _age, uint _userId){
  require(age[_userId] >= _age);
  _;
}

// 必须年满16周岁才允许开车 (至少在美国是这样的).
// 我们可以用如下参数调用`olderThan` 修饰符:
function driveCar(uint _userId) public olderThan(16, _userId){
  // 其余的程序逻辑
}
```

## **“view” 函数不花 “gas”**

当玩家从外部调用一个`view`函数，是不需要支付一分 gas 的。

这是因为 `view` 函数不会真正改变区块链上的任何数据 - 它们**只是读取**。因此用 `view` 标记一个函数，意味着告诉 `web3.js`，运行这个函数只需要查询你的本地以太坊节点，而不需要在区块链上创建一个事务（事务需要运行在每个节点上，因此花费 gas）。

稍后我们将介绍如何在自己的节点上设置 web3.js。但现在，你关键是要记住，在所能只读的函数上标记上表示“只读”的“`external view` 声明，就能为你的玩家减少在 DApp 中 gas 用量。

> *注意：如果一个 `view` 函数在另一个函数的内部被调用，而调用函数与 `view` 函数的不属于同一个合约，也会产生调用成本。这是因为如果主调函数在以太坊创建了一个事务，它仍然需要逐个节点去验证。所以标记为 `view` 的函数**只有在外部调用时才是免费的**。*
>
<!-- DAILY_CHECKIN_2026-03-14_END -->

# 2026-03-12
<!-- DAILY_CHECKIN_2026-03-12_START -->
solidity持续中...其实今天还把basic demo拉下来读了，还没通读完，明天继续，并且把文档和demo中的内容对一对

# solidity语法基础回顾（啃basic demo在回顾一下吧

<aside> 💡

[https://github.com/CryptozombiesHQ/cryptozombies-lesson-code](https://github.com/CryptozombiesHQ/cryptozombies-lesson-code)

</aside>

## **版本指令**

所有的 Solidity 源码都必须冠以 "version pragma" — 标明 Solidity 编译器的版本. 以避免将来新的编译器可能破坏你的代码。

例如: `pragma solidity ^0.4.19;` (当前 Solidity 的最新版本是 0.4.19).

综上所述， 下面就是一个最基本的合约 — 每次建立一个新的项目时的第一段代码:

```
pragma solidity ^0.4.19;

contract HelloWorld {

}
```

## **状态变量和整数**

**_状态变量_**是被永久地保存在合约中。也就是说它们被写入以太币区块链中. 想象成写入一个数据库。

### 例子:

```solidity
contract Example{
  // 这个无符号整数将会永久的被保存在区块链中
  uint myUnsignedInteger = 100;
}
```

在上面的例子中，定义 `myUnsignedInteger` 为 `uint` 类型，并赋值100。

## **数学运算**

在 Solidity 中，数学运算很直观明了，与其它程序设计语言相同:

-   加法: `x + y`
    
-   减法: `x - y`,
    
-   乘法: `x * y`
    
-   除法: `x / y`
    
-   取模 / 求余: `x % y` _(例如,_ `13 % 5` _余_ `3`_, 因为13除以5，余3)_
    

Solidity 还支持 **_乘方操作_** (如：x 的 y次方） // 例如： 5 \*\* 2 = 25

```
uint x = 5 ** 2; // equal to 5^2 = 25
```

## **结构体**

有时你需要更复杂的数据类型，Solidity 提供了 **结构体**:

```csharp
struct Person {
  uint age;
  string name;
}
```

结构体允许你生成一个更复杂的数据类型，它有多个属性。

> _注：我们刚刚引进了一个新类型,_ `string`_。 字符串用于保存任意长度的 UTF-8 编码数据。 如：_ `string greeting = "Hello world!"`_。_

## **数组**

如果你想建立一个集合，可以用 **_数组_这样的数据类型. Solidity 支持两种数组: _静态_ 数组和_动态_** 数组:

```
// 固定长度为2的uint类型静态数组:
uint[2] fixedArray;
// 固定长度为5的string类型的静态数组:
string[5] stringArray;
// uint类型动态数组，长度不固定，可以动态添加元素:
uint[] dynamicArray;
```

你也可以建立一个 **_结构体_**类型的数组 例如，上一章提到的 `Person`:

```
Person[] people; // 这是类型为结构体（或者说Person）的名为people的动态数组，可以不断添加元素
```

记住：状态变量被永久保存在区块链中。所以在你的合约中创建动态数组来保存成结构的数据是非常有意义的。

## **公共数组**

你可以定义 `public` 数组, Solidity 会自动创建 **_getter_** 方法. 语法如下:

```
Person[] public people;
```

其它的合约可以从这个数组读取数据（但不能写入数据），所以这在合约中是一个有用的保存公共数据的模式。

## **定义函数**

在 Solidity 中函数定义的句法如下:

```
function eatHamburgers(string _name, uint _amount) {

}//函数 eatHamburgers 有两个参数，分别是 string 类型的 _name 和 unit 类型的 _amount
```

这是一个名为 `eatHamburgers` 的函数，它接受两个参数：一个 `string`类型的 和 一个 `uint`类型的。现在函数内部还是空的。

> _注：: 习惯上函数里的变量都是以(_`_`_)开头 (但不是硬性规定) 以区别全局变量。我们整个教程都会沿用这个习惯。_

我们的函数定义如下:

```
eatHamburgers("vitalik", 100);
```

## **创建新的结构体**

还记得上个例子中的 `Person` 结构体：

```csharp
struct Person {
  uint age;
  string name;
}

Person[] public people;
```

现在创建新的 `Person` 结构，然后把它加入到名为 `people` 的数组中.

```solidity
// 创建一个新的Person:
Person satoshi = Person(172, "Satoshi");

// 将新创建的satoshi添加进people数组:
people.push(satoshi);
```

你也可以两步并一步，用一行代码更简洁:

```solidity
people.push(Person(16, "Vitalik"));
```

> _注：_`array.push()` _在数组的_ **_尾部_** _加入新元素 ，所以元素在数组中的顺序就是我们添加的顺序， 如:_

```solidity
uint[] numbers;
numbers.push(5);
numbers.push(10);
numbers.push(15);
// The `numbers` array is now equal to [5, 10, 15]
```

## **私有 / 公共函数**

Solidity 定义的函数的属性默认为`公共`。 这就意味着任何一方 (或其它合约) 都可以调用你合约里的函数。

显然，不是什么时候都需要这样，而且这样的合约易于受到攻击。 所以将自己的函数定义为`私有`是一个好的编程习惯，只有当你需要外部世界调用它时才将它设置为`公共`。

如何定义一个私有的函数呢？

```solidity
uint[] numbers;

function _addToArray(uint _number) private{
  numbers.push(_number);
}
```

这意味着只有我们合约中的其它函数才能够调用这个函数，给 `numbers` 数组添加新成员。

> 可以看到，在函数名字后面使用关键字 `private` 即可。和函数的参数类似，私有函数的名字用(`_`)起始。

## **返回值**

要想函数返回一个数值，按如下定义：

```solidity
string greeting = "What's up dog";

function sayHello() public returns (string){
  return greeting;
}
```

Solidity 里，函数的定义里可包含返回值的数据类型(如本例中 `string`)。

## **函数的修饰符**

上面的函数实际上没有改变 Solidity 里的状态，即，它没有改变任何值或者写任何东西。

这种情况下我们可以把函数定义为 **_view_**, 意味着它只能读取数据不能更改数据:

```solidity
function sayHello() public view returns (string){
```

Solidity 还支持 **_pure_** 函数, 表明这个函数甚至都不访问应用里的数据，例如：

```solidity
function _multiply(uint a, uint b) private pure returns (uint){
  return a * b;
}
```

这个函数甚至都不读取应用里的状态 — 它的返回值完全取决于它的输入参数，在这种情况下我们把函数定义为 **_pure_**.

> _注：可能很难记住何时把函数标记为 pure/view。 幸运的是， Solidity 编辑器会给出提示，提醒你使用这些修饰符。_

## **Keccak256**

如何让 `_generateRandomDna` 函数返回一个全(半) 随机的 `uint`?

Ethereum 内部有一个散列函数`keccak256`，它用了SHA3版本。一个散列函数基本上就是**把一个字符串转换为一个256位的16进制数字**。字符串的一个微小变化会引起散列数据极大变化。

这在 Ethereum 中有很多应用，但是现在我们只是用它造一个伪随机数。

例子:

```
//6e91ec6b618bb462a4a6ee5aa2cb0e9cf30f7a052bb467b0ba58b8748c00d2e5
keccak256("aaaab");
//b1f078126895a1424524de5321b339ab00408010b7cf0e6ed451514981e58aa9
keccak256("aaaac");
```

显而易见，输入字符串只改变了一个字母，输出就已经天壤之别了。

> _注: 在区块链中安全地产生一个随机数是一个很难的问题， 本例的方法不安全，但是在我们的Zombie DNA算法里不是那么重要，已经很好地满足我们的需要了。_

## **类型转换**

有时你需要变换数据类型。例如:

```solidity
uint8 a = 5;
uint b = 6;
// 将会抛出错误，因为 a * b 返回 uint, 而不是 uint8:
uint8 c = a * b;
// 我们需要将 b 转换为 uint8:
uint8 c = a * uint8(b);
```

上面, `a * b` 返回类型是 `uint`, 但是当我们尝试用 `uint8` 类型接收时, 就会造成潜在的错误。如果把它的数据类型转换为 `uint8`, 就可以了，编译器也不会出错。

## **事件**

我们的合约几乎就要完成了！让我们加上一个**事件**.

**事件** 是合约和区块链通讯的一种机制。你的前端应用“监听”某些事件，并做出反应。

例子:

```solidity
// 这里建立事件
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public{
  uint result = _x + _y;
  //触发事件，通知app
  IntegersAdded(_x, _y, result);
  return result;
}
```

你的 app 前端可以监听这个事件。JavaScript 实现如下:

```solidity
YourContract.IntegersAdded(function(error, result){
  // 干些事
})
```

<aside> 💡

存疑：{ } 外不需 ；

</aside>

## **Addresses （地址）**

以太坊区块链由  **_account_**  (账户)组成，你可以把它想象成银行账户。一个帐户的余额是 **_以太_** （在以太坊区块链上使用的币种），你可以和其他帐户之间支付和接受以太币，就像你的银行帐户可以电汇资金到其他银行帐户一样。

每个帐户都有一个“地址”，你可以把它想象成银行账号。这是账户唯一的标识符，它看起来长这样：

`0x0cE446255506E92DF41614C46F1d6df9Cc969183`

**地址属于特定用户（或智能合约）**

## **Mapping（映射）**

**除了  _结构体_**  和  **_数组_  ，** **_映射_** 是另一种在 Solidity 中存储有组织数据的方法。

映射是这样定义的：

```solidity
//对于金融应用程序，将用户的余额保存在一个 uint类型的变量中：
mapping (address => uint) public accountBalance;
//或者可以用来通过userId 存储/查找的用户名
mapping (uint => string) userIdToName;
```

映射本质上是存储和查找数据所用的键-值对。在第一个例子中，键是一个 `address`，值是一个 `uint`，在第二个例子中，键是一个`uint`，值是一个 `string`。

## **msg.sender**

在 Solidity 中，有一些全局变量可以被所有函数调用。 其中一个就是 `msg.sender`，它指的是当前调用者（或智能合约）的 `address`。

> _注意：在 Solidity 中，功能执行始终需要从外部调用者开始。 一个合约只会在区块链上什么也不做，除非有人调用其中的函数。所以_ `msg.sender`_总是存在的。_

以下是使用 `msg.sender` 来更新 `mapping` 的例子：

```solidity
mapping (address => uint) favoriteNumber;

function setMyNumber(uint _myNumber) public{
  // 更新我们的 `favoriteNumber` 映射来将 `_myNumber`存储在 `msg.sender`名下
  favoriteNumber[msg.sender] = _myNumber;
  // 存储数据至映射的方法和将数据存储在数组相似
}

function whatIsMyNumber() public view returns (uint){
  // 拿到存储在调用者地址名下的值
  // 若调用者还没调用 setMyNumber， 则值为 `0`
  return favoriteNumber[msg.sender];
}
```

在这个小小的例子中，任何人都可以调用 `setMyNumber` 在我们的合约中存下一个 `uint` 并且与他们的地址相绑定。 然后，他们调用 `whatIsMyNumber` 就会返回他们存储的 `uint`。

使用 `msg.sender` 很安全，因为它具有以太坊区块链的安全保障 —— 除非窃取与以太坊地址相关联的私钥，否则是没有办法修改其他人的数据的。

跟在 JavaScript 中一样， 在 Solidity 中你也可以用 `++` 使 `uint` 递增。

```solidity
uint number = 0;
number++;
// `number` 现在是 `1`了
```

_注意：在 Solidity 中，关键词放置的顺序并不重要_

# **Require**

在 `require`使得函数在执行过程中，当不满足某些条件时抛出错误，并停止执行：

```solidity
function sayHiToVitalik(string _name) public returns (string){
  // 比较 _name 是否等于 "Vitalik". 如果不成立，抛出异常并终止程序
  // (敲黑板: Solidity 并不支持原生的字符串比较, 我们只能通过比较
  // 两字符串的 keccak256 哈希值来进行判断)
  require(keccak256(_name) == keccak256("Vitalik"));
  // 如果返回 true, 运行如下语句
  return "Hi!";
}
```

如果你这样调用函数 `sayHiToVitalik（“Vitalik”）` ,它会返回“Hi！”。而如果调用的时候使用了其他参数，它则会抛出错误并停止执行。

因此，在调用一个函数之前，用 `require` 验证前置条件是非常有必要的。

## **继承（Inheritance）**

有个让 Solidity 的代码易于管理的功能，就是合约 **_inheritance_** (继承)：

```solidity
contract Doge{
  function catchphrase() public returns (string){
    return "So Wow CryptoDoge";
  }
}

contract BabyDoge is Doge{
  function anotherCatchphrase() public returns (string){
    return "Such Moon BabyDoge";
  }
}
```

由于 `BabyDoge` 是从 `Doge` 那里 **_inherits_** （继承)过来的。 这意味着当你编译和部署了 `BabyDoge`，它将可以访问 `catchphrase()` 和 `anotherCatchphrase()`和其他我们在 `Doge` 中定义的其他**公共函数**。

这可以用于逻辑继承（比如表达子类的时候，`Cat` 是一种 `Animal`）。 但也可以简单地将类似的逻辑组合到不同的合约中以组织代码。

## **引入（Import）**

Solidity 中，当你有多个文件并且想把一个文件导入另一个文件时，可以使用 `import` 语句：

```
import "./someothercontract.sol";

contract newContract is SomeOtherContract {

}
```

这样当我们在合约（contract）目录下有一个名为 `someothercontract.sol` 的文件（ `./` 就是同一目录的意思），它就会被编译器导入。
<!-- DAILY_CHECKIN_2026-03-12_END -->

# 2026-03-11
<!-- DAILY_CHECKIN_2026-03-11_START -->

“崩溃😩，满课的1天根本多少事件看，，，明天只有一节早八😋好好勤能补拙一下”

# solidity语法基础回顾（啃basic demo在回顾一下吧

## **版本指令**

所有的 Solidity 源码都必须冠以 "version pragma" — 标明 Solidity 编译器的版本. 以避免将来新的编译器可能破坏你的代码。

例如: `pragma solidity ^0.4.19;` (当前 Solidity 的最新版本是 0.4.19).

综上所述， 下面就是一个最基本的合约 — 每次建立一个新的项目时的第一段代码:

```
pragma solidity ^0.4.19;

contract HelloWorld {

}
```

## **状态变量和整数**

**_状态变量_**是被永久地保存在合约中。也就是说它们被写入以太币区块链中. 想象成写入一个数据库。

### 例子:

```solidity
contract Example{
  // 这个无符号整数将会永久的被保存在区块链中
  uint myUnsignedInteger = 100;
}
```

在上面的例子中，定义 `myUnsignedInteger` 为 `uint` 类型，并赋值100。

## **数学运算**

在 Solidity 中，数学运算很直观明了，与其它程序设计语言相同:

-   加法: `x + y`
    
-   减法: `x - y`,
    
-   乘法: `x * y`
    
-   除法: `x / y`
    
-   取模 / 求余: `x % y` _(例如,_ `13 % 5` _余_ `3`_, 因为13除以5，余3)_
    

Solidity 还支持 **_乘方操作_** (如：x 的 y次方） // 例如： 5 \*\* 2 = 25

```
uint x = 5 ** 2; // equal to 5^2 = 25
```

## **结构体**

有时你需要更复杂的数据类型，Solidity 提供了 **结构体**:

```csharp
struct Person {
  uint age;
  string name;
}
```

结构体允许你生成一个更复杂的数据类型，它有多个属性。

> _注：我们刚刚引进了一个新类型,_ `string`_。 字符串用于保存任意长度的 UTF-8 编码数据。 如：_ `string greeting = "Hello world!"`_。_

## **数组**

如果你想建立一个集合，可以用 **_数组_这样的数据类型. Solidity 支持两种数组: _静态_ 数组和_动态_** 数组:

```
// 固定长度为2的uint类型静态数组:
uint[2] fixedArray;
// 固定长度为5的string类型的静态数组:
string[5] stringArray;
// uint类型动态数组，长度不固定，可以动态添加元素:
uint[] dynamicArray;
```

你也可以建立一个 **_结构体_**类型的数组 例如，上一章提到的 `Person`:

```
Person[] people; // 这是类型为结构体（或者说Person）的名为people的动态数组，可以不断添加元素
```

记住：状态变量被永久保存在区块链中。所以在你的合约中创建动态数组来保存成结构的数据是非常有意义的。

## **公共数组**

你可以定义 `public` 数组, Solidity 会自动创建 **_getter_** 方法. 语法如下:

```
Person[] public people;
```

其它的合约可以从这个数组读取数据（但不能写入数据），所以这在合约中是一个有用的保存公共数据的模式。

## **定义函数**

在 Solidity 中函数定义的句法如下:

```
function eatHamburgers(string _name, uint _amount) {

}//函数 eatHamburgers 有两个参数，分别是 string 类型的 _name 和 unit 类型的 _amount
```

这是一个名为 `eatHamburgers` 的函数，它接受两个参数：一个 `string`类型的 和 一个 `uint`类型的。现在函数内部还是空的。

> _注：: 习惯上函数里的变量都是以(_`_`_)开头 (但不是硬性规定) 以区别全局变量。我们整个教程都会沿用这个习惯。_

我们的函数定义如下:

```
eatHamburgers("vitalik", 100);
```

## **创建新的结构体**

还记得上个例子中的 `Person` 结构体：

```csharp
struct Person {
  uint age;
  string name;
}

Person[] public people;
```

现在创建新的 `Person` 结构，然后把它加入到名为 `people` 的数组中.

```solidity
// 创建一个新的Person:
Person satoshi = Person(172, "Satoshi");

// 将新创建的satoshi添加进people数组:
people.push(satoshi);
```

你也可以两步并一步，用一行代码更简洁:

```solidity
people.push(Person(16, "Vitalik"));
```

> _注：_`array.push()` _在数组的_ **_尾部_** _加入新元素 ，所以元素在数组中的顺序就是我们添加的顺序， 如:_

```solidity
uint[] numbers;
numbers.push(5);
numbers.push(10);
numbers.push(15);
// The `numbers` array is now equal to [5, 10, 15]
```

## **私有 / 公共函数**

Solidity 定义的函数的属性默认为`公共`。 这就意味着任何一方 (或其它合约) 都可以调用你合约里的函数。

显然，不是什么时候都需要这样，而且这样的合约易于受到攻击。 所以将自己的函数定义为`私有`是一个好的编程习惯，只有当你需要外部世界调用它时才将它设置为`公共`。

如何定义一个私有的函数呢？

```solidity
uint[] numbers;

function _addToArray(uint _number) private{
  numbers.push(_number);
}
```

这意味着只有我们合约中的其它函数才能够调用这个函数，给 `numbers` 数组添加新成员。

> 可以看到，在函数名字后面使用关键字 `private` 即可。和函数的参数类似，私有函数的名字用(`_`)起始。

<aside> 💡

存疑：{ } 外不需 ；

</aside>
<!-- DAILY_CHECKIN_2026-03-11_END -->

# 2026-03-10
<!-- DAILY_CHECKIN_2026-03-10_START -->


# 导论

> # **Why Reactive Contracts 为什么选择反应式合同**
> 
> In the Ethereum world, smart contracts have revolutionized how we conceive of executing trustless agreements. Traditionally, these contracts spring into action only upon a user-initiated transaction. This presents inherent limitations. For one, smart contracts can't autonomously initiate actions or respond to blockchain events without an external prompt — either from a user or an automated script like a trading bot. This requires holding private keys and introducing a centralized point of control.在以太坊世界中，智能合约彻底改变了我们对执行无信任协议的认知。传统上，这些合同只有在用户发起的交易时才会生效。这带来了固有的局限性。首先，智能合约无法在没有外部提示的情况下自主发起动作或响应区块链事件——无论是来自用户还是像交易机器人这样的自动脚本。这需要持有私钥并引入集中控制点。
> 
> Reactive Contracts (RCs) emerge as a solution to this constraint. RCs are designed to autonomously react to events in the Ethereum Virtual Machine (EVM) and trigger subsequent actions across the blockchain ecosystem. This capability for the implementation of complex logic that can source information from multiple chains and enact changes or transactions across various platforms without a central oversight.反应式合约（RCs）作为解决这一限制的方案而出现。RCs 设计为自主响应以太坊虚拟机（EVM）中的事件，并触发区块链生态系统内的后续作。这种能力实现了复杂逻辑，能够从多条链中获取信息，并在不同平台上执行变更或交易，而无需中央监督

1.  智能合约是什么
    

以前做交易需要**信任第三方**

比如：

-   信任银行
    
-   信任中介
    
-   信任律师
    

通过第三方的背书完成交易

**智能合约可以自动执行规则（执行无信任协议）**。

比如：

写一段代码

```
if 如果 A 给钱 : 
	就自动把 NFT 给 A
```

整个过程：

-   没人能作弊
    
-   不需要中间人
    
-   代码自动执行
    

1.  智能合约的局限
    

智能合约是非自动的，需要**靠用户/机器人 bot 调用执行**。

举个例子（Uniswap 交换代币）：

点击 swap → 签名交易 → 发送交易 → 合约才开始运行。如果没有人为触发，合约就一直睡觉。

智能合约的触发，必须有人持有**私钥**，并且产生一个中心化的控制点。

比如： 机器人监听链上事件 → 发现机会 → 用**私钥**发交易。这个机器人控制私钥并决定什么时候触发 = 一个中心控制点。

而这个中心控制点**违背了去中心化**

1.  **Reactive Contracts**
    

**Reactive Contracts，“无需别’人‘触发，会自己反应的合约” =** 监听链上的事件，满足特定条件时，自动对 EVM（以太坊虚拟机）中的事件做出反应。

RCs能从**多条区块链获取信息**，在**不同平台执行**操作或交易

举例：

Reactive Contract 可以同时看很多链（ETH链/BSC/Arbitrum/Polygon）的信息，然后做判断——如果A链价格低、B链价格高，就套利

RCs 不需要中央监管，因此不会造成中心控制点。

RCs 不需要：

-   中心服务器
    
-   执行策略
    
-   管理员
    
-   私钥控制
    

1.  RCs 的优势
    

-   去中心化：RC 在区块链上独立运行，消除集中控制点，通过降低作或失败的风险提升安全性。
    
-   自动化：RC 自动响应链上事件执行智能合约逻辑，减少人工干预需求，实现高效、实时的响应。
    
-   跨链互作性：RC 可以与多个区块链交互，实现复杂的跨链交互，提升多样性并弥合网络间的差距。
    
-   提升效率与功能性： 通过对实时数据的响应，RC 提升了智能合约的效率，支持复杂金融工具、动态 NFT 和创新 DeFi 应用等先进功能。
    
-   DeFi 及其他领域的创新：RC 为 DeFi 及其他区块链应用（如自动化交易和动态治理）带来了新可能，打造了一个更具响应性和互联互通的区块链生态系统。
    

* * *

# lesson 1

> Reactive vs. Traditional Contracts: Unlike traditional smart contracts, RCs autonomously monitor blockchain events and execute actions without user intervention, providing a more dynamic and responsive system. 反应式合约与传统合约： 与传统的智能合约不同，反应式合约能够自主监控区块链事件并执行操作，无需用户干预，从而提供更动态、响应更迅速的系统。
> 
> Inversion of Control: RCs invert the traditional execution model by allowing the contract itself to decide when to execute based on predefined events, eliminating the need for external triggers like bots or users. 控制反转： RC 合约通过允许合约本身根据预定义的事件决定何时执行，从而颠覆了传统的执行模型，消除了对机器人或用户等外部触发器的需求。
> 
> Decentralized Automation: RCs enable fully decentralized operations, automating processes like data collection, DEX trading, and liquidity management without centralized intermediaries. 去中心化自动化： RC 实现完全去中心化的运营，无需中心化的中介机构即可自动执行数据收集、DEX 交易和流动性管理等流程。
> 
> Cross-Chain Interactions: RCs can interact with multiple blockchains and sources, enabling sophisticated use cases like cross-chain arbitrage and multi-oracle data aggregation. 跨链交互： RC 可以与多个区块链和数据源进行交互，从而实现复杂的用例，例如跨链套利和多预言机数据聚合。
> 
> Practical Applications: RCs have diverse applications, including collecting data from oracles, implementing UniSwap stop orders, executing DEX arbitrage, and automatically rebalancing pools across exchanges. 实际应用： RC 有多种应用，包括从预言机收集数据、实施 UniSwap 止损单、执行 DEX 套利以及自动在交易所之间重新平衡资金池。

1.  控制反转（IoC）
    

传统智能合约是：机器人/用户 → 调用合约。依赖机器人/用户

Reactive Contract ：链上事件 → 自动触发合约。事件驱动，合约内部执行。

1.  Reactive Contract 是怎么工作的
    

创建 RC 时，需要先告诉它三件事：

### 1 要监听哪些链

比如

```
Ethereum
Arbitrum
Polygon
```

### 2 要监听哪些合约

例如

```
Uniswap pool
某个借贷协议
某个预言机
```

### 3 要监听哪些事件

例如

```
Swap
Transfer
Loan
Vote
Whale交易
```

然后系统就会：

```
监听事件
↓
事件发生
↓
触发 RC
↓
执行逻辑
↓
发交易
↓
更新**状态**

```

**状态包括：**

-   **记录历史数据**
    
-   **积累数据**
    
-   **根据条件触发操作**
    

1.  Reactive Contract 能做什么
    

## 1 预言机数据整合

RC 可以监听多个预言机：

例如：

```
Chainlink
Pyth
其他oracle
```

然后：

```
取平均价格
↓
执行操作
```

比如：

```
比赛结果 → 自动派奖
```

## 2 Uniswap 自动止损

RC 可以监听：

```
Uniswap swap事件
```

然后计算：

```
当前价格
```

如果价格达到：

```
止损价
```

就自动：

```
执行 swap
```

## 3 DEX 套利

RC 可以：

同时监听多个池子

例如：

```
Uniswap
SushiSwap
Balancer
```

如果发现：

```
价格差
```

就自动：

```
套利交易
```

可以：

-   单链套利（flash loan）
    
-   跨链套利
    

## 4 流动性池自动再平衡

RC 还可以：

监控多个交易所的流动性。

例如：

```
A链池子太多资金
B链池子太少
```

RC 就会：

```
自动转移资金
```

实现：

**自动再平衡 liquidity pools**

* * *
<!-- DAILY_CHECKIN_2026-03-10_END -->
<!-- Content_END -->
