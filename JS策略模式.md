考虑这么一个需求:
公司年终要计算每个人的奖金,需要写一个程序来做这件事情,那么一般来说会怎么写?

首先要考虑接受的参数,每个人的奖金至少和绩效考核等级和工资数额相关,也就是说至少得要接受两个参数'绩效等级','基本工资',好,一般来说我会这么写:

```
    var calcBonus = function(level, salary) {
        switch(level) {
            case 'S':
                return salary * 4;
                break;
            case 'A':
                return salary * 3;
                break;
            case 'B':
                return salary * 2;
                break;
            case 'C':
                return salary * 1;
                break;
            case 'D':
                return salary * 0;
                break;
        }
    };
    calcBonus('S', 12000); // 48000
    calcBonus('A', 12000); // 36000
```
一般来说这个简单的函数对于一般年底临时来计算奖金来说是没有什么问题了,但是显然这段代码虽然简单易懂但是存在很多缺陷:

- 计算奖金的函数过于庞大,里面包含了许多的条件判断语句.

- 缺乏弹性,如果说加入了新的绩效等级或者是对应等级的绩效奖金需要调整都只能从函数内部入手,违反封闭-开放原则.

- 复用性差,如果在其他地方想用这段函数只能复制粘贴.

一般来说对于这种相似的地方较多的代码我们很容易想到拆出来将大函数拆成很多小函数,但是这种方式的改善非常有限:

```
    var  calcS = function() {
        return salary * 4;
    };
    var  calcA = function() {
        return salary * 3;
    };
    var  calcB = function() {
        return salary * 2;
    };
    var  calcC = function() {
        return salary * 1;
    };
    var  calcD = function() {
        return salary * 0;
    };
    var calcBonus = function(level, salary) {
        switch(level) {
            case 'S':
                calcS();
                break;
            case 'A':
                calcA();
                break;
            case 'B':
                calcB();
                break;
            case 'C':
                calcC();
                break;
            case 'D':
                calcD();
                break;
        }
    };
    calcBonus('S', 12000); // 48000
    calcBonus('A', 12000); // 36000
```
下面我们考虑用策略模式重构代码(策略模式具体是什么意思还是看代码吧,目的就是将算法的使用和算法的实现分离开):

```
    var strategies = {
        S: function(salary) {
            return salary * 4;
        },
        A: function(salary) {
            return salary * 3;
        },
        B: function(salary) {
            return salary * 2;
        },
        C: function(salary) {
            return salary * 1;
        },
        D: function(salary) {
            return salary * 0;
        }
    };
    var calcBonus = function(level, salary) {
        return strategies[level](salary);
    };
    calcBonus('S', 12000); //48000
    calcBonus('A', 12000); //36000
```
这段代码中包含了两个函数,一个专门用来实现计算的类,还有一个负责传参的calc函数,这个函数虽然叫calc但是本身却并不负责calc,而是将运算委托给startegies类去负责执行具体的运算,然后返回结果,这种方式就叫做策略模式,下面我看看可能对工作更加有用的场景`动画`:

首先简单说下JS动画的基本原理:`利用JS定时器和一系列的参数连续地改变DIV或者是IMG的位置形成最终的动画效果`

一个完整的动画就不得不考虑以下几点:
- 动画开始时元素所在的位置.

- 动画目标位置.

- 动画开始的时间.

- 动画持续的时间.

考虑一个小球运动的缓动算法,一般来说一个JS动画函数创建一个setInterval定时器,指定每隔 1 / 60 S 执行一次(requestAnimationFrame)然后在定时器中每一次执行都会把动画已经消耗的时间,原始的位置和目标位置等信息传入缓动算法,该算法会根据这些参数计算出小球当前的位置并且更新对应的CSS属性.

```

```
