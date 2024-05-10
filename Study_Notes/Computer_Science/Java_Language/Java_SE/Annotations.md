# Java Object Lifecycle





# Some commonly used Annotations
## \@SuppressWarnings
> [!important]





# Self-Designed Annotations
> [!important]
> `@Target`元注解该规定当前注解生效的对象，即可用范围：
> - `ElementType.TYPE`表示对类生效。
> - `ElementType.METHOD`表示对类中的方法生效。
> - `ElementType.FIELD`表示对类中的成员变量生效。
> 
> `@Retention`元注解规定当前注解的生效时间段:
> - `RetentionPolicy.SOURCE`：在源码阶段和编译阶段生效，编译时会查看，编译后丢弃，运行时不可见。
> - `RetentionPolicy.CLASS`: 在编译后保留，但在运行时不可见。
> - `RetentionPolicy.RUNTIME`: 在运行时可见，框架设计的灵魂。
> 
> `@Documented`元注解表示当前注解在帮助文档中保留。


## Examples
> [!example] Execute a method of a class multiple times
> 假设现在我需要在方法上的注解，注解的功能是使得方法被执行`n`次，`n`可由用户自定义配置。
```java
public class Test01 {

    public static void main(String[] args) throws InvocationTargetException, IllegalAccessException {
        @SuppressWarnings("unused")
        Cat myCat = new Cat("Stella");

        // 获取对象方法(including private public default protected)
        Method[] declaredMethods = myCat.getClass().getDeclaredMethods();

		//
        for(Method method: declaredMethods) {
            if (method.isAnnotationPresent(ExecuteMultipleTimes.class)) {
                ExecuteMultipleTimes annotation = method.getAnnotation(ExecuteMultipleTimes.class);
                int times = annotation.value();
                for (int i = 0; i < times; i++) {
                    method.invoke(myCat);
                }
            }
        }
    }
}


@VeryImportant
class Cat {
    private String name;
    public Cat(String name) {
        this.name = name;
    }

	// 执行三次
    @ExecuteMultipleTimes(3)
    public void meow() {
        System.out.println("Miao!");
    }
}
```

