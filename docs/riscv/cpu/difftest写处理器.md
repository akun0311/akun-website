# 使用Difftest写处理器

Difftest适合的场景是，是从一条指令一条指令开始支持，你先把第一条指令给跑通
Difftest适合去验证一条指令
而不适合去验证一个fetch模块，一个decode模块，一个execute模块这样子

当我们使用`Difftest`验证框架去写处理器的时候，其实更适合的是对`CPU`去测试和验证

