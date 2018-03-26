### 对于实施者来说，这是一个开放标准，用于实现可靠的，可互操作的JavaScript promise

     一个promise最终结果通过异步操作。主要通过 **then** 方法实现，注册回调函数接受一个promise最终的value或者promise没完成(fulfilled)的一个reason。

     本规范详细介绍了then方法的行为，提供了一个可互操作的基础，所有Promise / A+符合承诺实现都可以依赖提供。因此，规范被认为是很稳定的。虽然Promise /A+ 组织可能会偶尔修改规范，向后兼容更改以解决新发现的角落案例，但只有在仔细考虑，讨论和测试之后，我们才会整合大型或向后不兼容的更改。

   历史上，Promises / A +阐明了先前Promises / A提案的行为条款，将其扩展为涵盖事实上的行为，并省略了未指定或存在问题的部分

   最后，核心Promises / A +规范不涉及如何创建，履行或拒绝Promise，而是选择专注于提供可互操作的方法。未来的配套规范工作可能涉及这些主题。

1. 术语
1.1 Promise 是一个对象或方法有then 方法符合这个规范的方法
1.2 thenable 是一个对象或者方法设置一个then方法
1.3 value是一个合法的JavaScript的值，包括undefined，thenable或者一个promise
1.4 exception 是一个值throw 




