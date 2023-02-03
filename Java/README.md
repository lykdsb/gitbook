# 日期类

java中最常用的日期类主要有 Date 、Calendar、LocalDate、SimpleFormat

## Date类

在java中创建Date主要有两种方式

![](<.gitbook/assets/截屏2023-02-03 下午7.14.37.png>)

其中`java.util.Date` 是最常用的日期类，而`java.sql.Date` 主要是用于处理sql中的日期。`java.sql.Date` 是`java.util.Date` 的子类，其仅存储日期而不保存小时和分钟以及秒:

> To conform with the definition of SQL `DATE`, the millisecond values wrapped by a `java.sql.Date` instance must be 'normalized' **by setting the hours, minutes, seconds, and milliseconds to zero** in the particular time zone with which the instance is associated.

### java.util.Date

