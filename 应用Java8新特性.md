# 应用Java8新特性

Java 8的Stream流，我们使用stream()函数从一个集合中获取一个stream对象。接下来是一些操作

（filter，sorted，map，collect）连接在一起形成了一个管道，管道可以被看做是类似数据库查询数据的一种方式。

filter（通过给定一个谓词来过滤元素）

sorted（通过给定一个比较器实现排序）

map (用于提取信息)

除了collect其他操作都会返回Stream

这样就可以形成一个管道将它们连接起来，我们可以把这个链看做是一个对源的查询条件。

在collect被调用之前其实什么实质性的东西都都没有被调用。collect被调用后将会开始处理管道，最终返回结果（结果是一个list）。

如何处理并行？

在Java8中非常简单：只需要使用parallelStream()取代stream()就可以了

1，提取出list对象中的一个属性

List<Student> stuList = new ArrayList<Student>();

List<String> stIdList1 = stuList.stream().map(Student::getId).collect(Collectors.toList());

stIdList1.forEach(s -> System.out.print(s+" "));

2，提取出list对象中的一个属性并去重

List<String> stIdList2 = stuList.stream().map(Student::getId).distinct().collect(Collectors.toList());

]