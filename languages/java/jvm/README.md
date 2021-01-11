# JVM (Java Virtual Machine)

## Как устроена JVM

[Отличное описание устройства JVM](https://www.freecodecamp.org/news/jvm-tutorial-java-virtual-machine-architecture-explained-for-beginners/)

- Class loader (подгружает классы, подготавливает статические переменные и константы, проводит валидацию, линкует и инициализирует)
- Runtime area (все что касается рантайма: хранение переменных, методов, хип, стэк)
- Execution engine (исполнение кода: интерпритатор, JIT(для ускорения вызовов повторяющихся кусков кода, оптимизации работы с памятью), GC)

# Литература
- [JVM Tutorial - Java Virtual Machine Architecture Explained for Beginners](https://www.freecodecamp.org/news/jvm-tutorial-java-virtual-machine-architecture-explained-for-beginners/)