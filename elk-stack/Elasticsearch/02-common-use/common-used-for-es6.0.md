# 为什么？
为什么要尝试版本6.0，而不是直接到最新版本，而是在某些角度来说版本6.0合理，从某些角度来说其又不合理。
<br>
```
合理的地方：
很好的分层概念，比如我创建一个部门department，相应的我就可以创建下面的一个层次employee，而这点在版本7.0中是不可实现的，这种不可实现的是不可能从访问的URL中提醒。

7.0的主要设计理念：
部门就存储在部门的index中，每个mapping只属于唯一的一个index。
employee就存储在employee的index中。

6.0的设计理念：
xxx/department/employee，也可能同时存在着xxx/department/introduction。
此时employee和introduction同时存储在同一个Index中。


```

# 脚本
最外层首先创建index，然后在二级甚至是三级四级，就可以随便写了。也就是强的约束主要体现在index这一层。
```sh
curl -X PUT "localhost:9200/department" -H 'Content-Type: application/json' -d'
{
    "settings" : {
        "number_of_shards" : 1
    },
    "mappings" : {
        "employee" : {
            "properties" : {
                "title":    { "type": "text"  },
                "name":     { "type": "text"  },
                "created":  { "type": "date"}   }
          }
    }
}
'
```
可见上面创建的是最外层的部门index，下面即将随意的创建department里面的document: employee

```sh
curl -X PUT "localhost:9200/department/employee/1" -H 'Content-Type: application/json' -d'
{
    "title" : "Elasticsearch Department",
	"name":"ESD",
    "age" : 20,
	"created":"2019-05-27"
}
'
```
其中所有属性：title, name, age, created等全部都是随意由用户自己定义。同样我又可以继续向下创建另外的：
```sh
curl -X PUT "localhost:9200/department/employee/2" -H 'Content-Type: application/json' -d'
{
    "user" : "kimchy",
    "post_date" : "2009-11-15T14:12:12",
    "message" : "trying out Elasticsearch",
	"age":30,
	"job": "software engineer"
}
'



curl -X PUT "localhost:9200/department/employee/8" -H 'Content-Type: application/json' -d'
{
    "title" : "The third person",
	"name":"name 3",
    "age" : 20,
	"created":"1560032583658"
}
'

```

上述同样是可以的。从上述的两个创建来看，主要体现在URL上的随意：/department/employee/x，只要index存在那么即可以创建成功。
其中的x为document数据的id。

而在7.0中，就不是这样了。

## Date类型的值
https://www.elastic.co/guide/en/elasticsearch/reference/current/date.html

个人倾向按照UTC Milliseconds的方式来填充date类型的值,因为当我试图使用"date": "2015-01-01T12:10:30Z" 方式来设置值的时候，发现不起作用：
```
curl -X PUT "localhost:9200/department/employee/8" -H 'Content-Type: application/json' -d'
{
    "title" : "The third person",
	"name":"name 3",
    "age" : 20,
	"created":"1560032583658"
}
'
```


常见其他的：
```sh
curl -X GET "localhost:9200/department/employee/3"

```
