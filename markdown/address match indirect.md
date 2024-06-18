# address match indirect

## 样例

![image-20230403163100606](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230403163100606.png)

![image-20230403163921129](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230403163921129.png)

## 按前后顺序用到MATCH、ADDRESS、INDIRECT

### MATCH：用来找内容在哪个行或列（所以只能确定一个行或一个列，不能找到单元格）

### 样例

![image-20230403163226215](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230403163226215.png)

match函数用来找到Lookup_value里的内容在Lookup_array里的哪个位置（最后的位置用相对位置来表示）

lookup_value:你要找的内容

lookuparray：你要在哪找lookup_value

match_type:等于0表示找完全相同的内容，其他的不知道你用不用的到，就先贴个图（我猜不会用到

![image-20230403163740299](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230403163740299.png)



这个看我第一个录屏



## ADDRESS：用来找内容在哪里（找到单元格）

### 样例

![image-20230403164002859](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230403164002859.png)

row_num:要找的内容的行号

column_num:要找的内容的列号

abs_num:用什么方式引用

（！注意：因为用match得到了内容对应的行号和列号是相对引用的，所以就用4，表示用相对引用方式引用内容

说白了就是如果row_num,column_num用的是match函数的话，就填4）

A1:如果想让单元格用A1，A2，B1，B2...这种格式表示的话，就填1或TRUE

​	 如果想让单元格用R1C1，R2C1，R1C2，R2C2...这种格式表示的话，就填0或FALSE

​     R就是row 行号 C就是column 列号



## INDIRECT： 找到位置所指的内容

### 样例

![image-20230403164939251](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230403164939251.png)

ref_text:你要在哪找内容？ ref:reference参考    text:文本  就像你查资料，参考文本是啥，但是这里的文本就是指的单元格的位置

A1：和ADDRESS里的A1是同一个意思，不填的话就是默认TRUE

