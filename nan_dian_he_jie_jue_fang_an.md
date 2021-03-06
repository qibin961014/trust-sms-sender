# <center>难点和解决方案


---


* **页面间信息的传递**

　　为增添用户体验和减少操作难度，我们设计了功能不同的多个页面。页面间的信息传递就显得十分重要。APP INVENTER提供的页面间传递信息有两种途径。
　　1. 页面间直接传值。<br>
　　2. 保存数据于位微数据库，并通过微数据库数据的写入和调用实现页面间信息的传递。<br>

　　我们选择了第二种。这种的优势在于，信息传递的可控性较好，能够一次传递多个数据，且多页面共享。

* **微数据库数据结构的设计**

　　群组的存储和调用都涉及到了微数据库的使用。数据库结构的设计尤为关键。需要存储的数据类型主要有：

　　1. 群组名称 <br>
　　2. 群组长度 <br>
　　3. 联系人姓名 <br>
　　4. 联系人电话号码 <br>
　　5. 页面间需要传递的信息 <br>

　　需要解决的难点主要是，数据间的相互调用和影响。为此，我们队数据库结构进行如下设计。（以群组“家人”，联系人“爸爸 139xxxxxxxx” “妈妈 152xxxxxxxx” 为例）

　　1. 存储数据“家人”，标签“列表1”。<br>
　　2. 存储数据“4”，标签“列表1长度”。<br>
　　3. 存储数据“爸爸”，标签“家人1”。<br>
　　4. 存储数据“139xxxxxxxx”，标签为“家人2” <br>
　　5. 存储数据“妈妈”，标签“家人3”。<br>
　　6. 存储数据“152xxxxxxxx”，标签为“家人4” <br>[^姓名存储为奇数，电话号码存储为偶数，列表总长度为群组中联系人个数的两倍]

　　这样，我们就得到了这样的一个数据库：

| <center>**数据** | <center>**标签** |
| -- | -- |
| <center>家人 | <center>列表1 |
| <center>4 | <center>列表1长度 |
| <center>爸爸 | <center>家人1 |
| <center>139xxxxxxxx | <center>家人2 |
| <center>妈妈 | <center>家人3 |
| <center>152xxxxxxxx | <center>家人4 |

　　这样我们通过数据间元素的相互调用，就能实现对于数据库中任何一个对应元素的精确定位、调用和编辑。

　　至于页面间的信息传递，我们也通过数据库完成，具体保存方式视信息内容和形式而定。


