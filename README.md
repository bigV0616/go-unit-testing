## 单元测试（英语：Unit Testing）又称为模块测试：
是针对程序模块（软件设计的最小单位）来进行正确性检验的测试工作。程序单元是应用的最小可测试部件。在过程化编程中，一个单元就是单个程序、函数、过程等；对于面向对象编程，最小单元就是方法，包括基类（超类）、抽象类、或者派生类（子类）中的方法。 通常来说，程序员每修改一次程序就会进行最少一次单元测试，在编写程序的过程中前后很可能要进行多次单元测试，以证实程序达到软件规格书要求的工作目标，没有程序错误；虽然单元测试不是什么必须的，但也不坏，这牵涉到项目管理的政策决定。

> [说得直接一些程序功能尽量要拆分最小单元模块，功能独立的模块，进行预知功能测试，单元测试对于程序员来说很重要，新手可能一气呵成把所有功能写完了然后再进行测试这样会有很多隐藏的bug，反而会更耽误很多时间在调试bug上，如果每完成一个模块就做一下单元测试的话，你会体验到其中的乐趣😄。]

>* 文件名必须是_test.go结尾的，这样在执行go test的时候才会执行到相应的代码 
>* 你必须import testing这个包 
>* 所有的测试用例函数必须是Test开头 
>* 测试用例会按照源代码中写的顺序依次执行 
>* 测试函数TestXxx()的参数是testing.T，我们可以使用该类型来记录错误或者是测试状态 
>* 测试格式：func TestXxx (t *testing.T),Xxx部分可以为任意的字母数字的组合，但是首字母不能是小写字母[a-z]，例如Testintdiv是错误的函数名。    
>* 函数中通过调用testing.T的Error, Errorf, FailNow, Fatal, FatalIf方法，说明测试不通过，调用Log方法用来记录测试的信息

```
import (
    // "fmt"
    "testing"
)

func Test_SetConfig(t *testing.T) {
    conf := SetConfig("../conf/conf.ini")
    host := conf.GetValue("database", "host")
    t.Log(host)
}
```
## 执行方法
>* go test config_test.go config.go 加上原文件config.go
## 官方对testing模块Log的解释
```
// Log formats its arguments using default formatting, analogous to Println,
// and records the text in the error log. For tests, the text will be printed only if
// the test fails or the -test.v flag is set. For benchmarks, the text is always
// printed to avoid having performance depend on the value of the -test.v flag.
func (c *common) Log(args ...interface{}) { c.log(fmt.Sprintln(args...)) }
```
>* go test -v config_test.go config.go 如果使用了t.Log 则加上-v


