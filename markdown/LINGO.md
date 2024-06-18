# LINGO

## 适用：解决线性规划、非线性规划、整数规划等优化问题，在求解最优化问题相较于matlab更为简便

## 程序结构

* MODEL
* SETS:“SIX”为集合名称，“S1..S6”表示索引是从S1到S6，“E”为数据

```lingo
	SETS:
		SIX/S1..S6/:E;
		EIGHT/E1..E8/:D;
		SIXEIGHT(SIX,EIGHT):X,C;

	ENDSETS
```



* DATA:输入数据，或利用@OLE函数从EXCEl中，与DATA名称同名的数据块读入数据

```
	DATA:
		E=60 55 51 43 41 52;
		D=35 37 22 32 41 32 43 38;
		C=6 2 6 7 4 2 9 5
			4 9 5 3 8 5 8 2
			5 2 1 9 7 4 3 3
			7 6 7 3 9 2 7 1
			2 3 9 5 7 2 6 5
			5 5 2 2 8 1 4 3;

	ENDDATA
```

* @FOR:约束条件

```
	@FOR(EIGHT(J):@SUM(SIX(I):X(I,J))=D(J));
	@FOR(SIX(I):@SUM(EIGHT(J):X(I,J))<=E(I));
```

* MIN/MAX:目标函数

```
	MIN=@SUM(SIXEIGHT(I,J):C(I,J)*X(I,J));
```

## 注意

例如设置索引时，想设置为所有索引的单数索引，利用逻辑运算符#ge#与#le#进行筛选

#ge# 若左边的运算数大于或等于右边的运算数，则为true，否则为false

#le# 若左边的运算数小于或等于右边的运算数，则为true，否则为false

## 完整示例程序

```
MODEL:
	SETS:
		SIX/S1..S6/:E;
		EIGHT/E1..E8/:D;
		SIXEIGHT(SIX,EIGHT):X,C;

	ENDSETS

	DATA:
		E=60 55 51 43 41 52;
		D=35 37 22 32 41 32 43 38;
		C=6 2 6 7 4 2 9 5
			4 9 5 3 8 5 8 2
			5 2 1 9 7 4 3 3
			7 6 7 3 9 2 7 1
			2 3 9 5 7 2 6 5
			5 5 2 2 8 1 4 3;

	ENDDATA

	MIN=@SUM(SIXEIGHT(I,J):C(I,J)*X(I,J));
	@FOR(EIGHT(J):@SUM(SIX(I):X(I,J))=D(J));
	@FOR(SIX(I):@SUM(EIGHT(J):X(I,J))<=E(I));

END
```

- ![img](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/1ad5ad6eddc451da3868246eb4fd5266d116329c)

```
var/1..6/:x,w;
link(var,var):k;
```
