# 日期类

java中最常用的日期类主要有 Date 、Calendar、LocalDate、SimpleFormat

## Date类

在java中创建Date主要有两种方式

![](<.gitbook/assets/截屏2023-02-03 下午7.14.37.png>)

其中`java.util.Date` 是最常用的日期类，而`java.sql.Date` 主要是用于处理sql中的日期。`java.sql.Date` 是`java.util.Date` 的子类，其仅存储日期而不保存小时和分钟以及秒:

> To conform with the definition of SQL `DATE`, the millisecond values wrapped by a `java.sql.Date` instance must be 'normalized' **by setting the hours, minutes, seconds, and milliseconds to zero** in the particular time zone with which the instance is associated.

### java.util.Date

`Date` 使用两种构造方法（其余已经过时）

* `new Date()` :获得当前的时间
* `new Date(long date)` :传入一个long变量表示从1970年到对应日期之间毫秒数

`Date` 中主要使用的方法有：

| Method             | What               |
| ------------------ | ------------------ |
| `compareTo()`      | 返回两个日期之间的先后顺序      |
| `getTime()`        | 返回对应时间到1970年之间的毫秒数 |
| `after()/before()` | 返回两个日期之间的先/后       |
| `toInstant()`      | 将时间转换为标准时间         |

{% hint style="warning" %}
不要使用`Date`中的`getYear()`/`setYear()这一类的get`

`，方法。这些已经过时，并且都在Calendar类中实现了`<img src=".gitbook/assets/截屏2023-02-03 下午7.51.34.png" alt="" data-size="original"> ``&#x20;


{% endhint %}

### SimpleDateFormat

可以使用`SimpleDateFormat`用来格式化日期并进行输出

```java
Date date = new Date();
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
System.out.println(sdf.format(date));
----
2023-02-03 20:02:46
```

完整的patter列表如下：

| Letter | Date or Time Component                           |
| ------ | ------------------------------------------------ |
| `G`    | Era designator                                   |
| `y`    | Year                                             |
| `Y`    | Week year                                        |
| `M`    | Month in year                                    |
| `w`    | Week in year                                     |
| `W`    | Week in month                                    |
| `D`    | Day in year                                      |
| `d`    | Day in month                                     |
| `F`    | Day of week in month                             |
| `E`    | Day name in week                                 |
| `u`    | Day number of week (1 = Monday, ..., 7 = Sunday) |
| `a`    | Am/pm marker                                     |
| `H`    | Hour in day (0-23)                               |
| `k`    | Hour in day (1-24)                               |
| `K`    | Hour in am/pm (0-11)                             |
| `h`    | Hour in am/pm (1-12)                             |
| `m`    | Minute in hour                                   |
| `s`    | Second in minute                                 |
| `S`    | Millisecond                                      |
| `z`    | Time zone                                        |
| `Z`    | Time zone                                        |
| `X`    | Time zone                                        |

### java.sql.Date

这个类没有无参构造方法，只能接收一个`long` 的毫秒值。一般在创建的过程中使用`new java.util.Date().getTime()`

```java
Date date =new Date(new java.util.Date().getTime());
System.out.println(date);
----
2023-02-03
```

## Calendar 类

`Calendar` 同样经常用于java中的时间的表示，需要注意的是，其是一个抽象类，不能进行实例化，因此我们需要使用`getInstance()` 方法取得实例

```java
public abstract class Calendar implements Serializable, Cloneable, Comparable<Calendar> {
    ...
}
```

需要注意的是`Calendar` 的自带`toString()`方法比较复杂，因此最好将其转换为`Date`类型进行输出比较好

```java
Calendar calendar = Calendar.getInstance();
System.out.println(calendar);
----
java.util.GregorianCalendar[time=1675426549167,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Hong_Kong",offset=28800000,dstSavings=0,useDaylight=false,transitions=71,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2023,MONTH=1,WEEK_OF_YEAR=5,WEEK_OF_MONTH=1,DAY_OF_MONTH=3,DAY_OF_YEAR=34,DAY_OF_WEEK=6,DAY_OF_WEEK_IN_MONTH=1,AM_PM=1,HOUR=8,HOUR_OF_DAY=20,MINUTE=15,SECOND=49,MILLISECOND=167,ZONE_OFFSET=28800000,DST_OFFSET=0]
----
System.out.println(calendar.getTime());
----
Fri Feb 03 20:15:49 HKT 2023
```

`Calendar` 主要有以下的方法：

| Method                     | What        |
| -------------------------- | ----------- |
| `getTime()`                | 返回Date类型    |
| `get(int field)`           | 返回日期中对应的域的值 |
| `set(int field,int value)` | 设定日期中某一个域的值 |
| `setTime(Date date)`       | 重新设定日期      |

## 新日期类

新日期类主要有三个

* LocalDate：只包含日期
* LocalTime：只包含时间
* LocalDateTime：同时包含日期和时间

这三个日期类构造方法私有，一般通过`LocalDate.now()` 进行实例化

```java
LocalDate date = LocalDate.now();
System.out.println(date);
----
2023-02-03
```

{% hint style="success" %}
&#x20;Calendar、Date、SimpleDateFormat 这三个类是线程不安全的。而LocalDate这三个新日期类不仅是线程安全的，还是和String一样的**不可变类**
{% endhint %}

