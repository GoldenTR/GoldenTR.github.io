# matlab数字图像处理

[TOC]



## 基础

### 概念

空域

![image-20230714181700901](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230714181700901.png)

频域

![image-20230714181753381](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230714181753381.png)

图像的矩阵表示

![image-20230714181723763](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230714181723763.png)

二值图像

![image-20230714182218414](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230714182218414.png)

灰度图像

![image-20230714182205287](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230714182205287.png)

RGB图像

![image-20230714182151068](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230714182151068.png)

索引图像

![image-20230714182131596](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230714182131596.png)

## 空间滤波-线性空间滤波

### 拉普拉斯滤波器

#### 基本公式

![image-20230713162731197](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230713162731197.png)

![image-20230713162808958](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230713162808958.png)

#### 基本思想：

当邻域的中心像素灰度低于它所在邻域内的其他像素的平均灰度时，此中心像素的灰度应该进一步降低；

当高于时进一步提高中心像素的灰度，从而实现图像锐化处理。
在算法实现过程中，通过对邻域中心像素的四方向或八方向求梯度，并将梯度和相加来判断中心像素灰度与邻域内其他像素灰度的关系，并用梯度运算的结果对像素灰度进行调整。

#### 效果：

当邻域内像素灰度相同时，模板的卷积运算结果为0；

当中心像素灰度高于邻域内其他像素的平均灰度时，模板的卷积运算结果为正数；

当中心像素的灰度低于邻域内其他像素的平均灰度时，模板的卷积的负数。

对卷积运算的结果用适当的衰弱因子处理并加在原中心像素上，就可以实现图像的锐化处理。

#### 代码示例：

* 使用fspecial函数生成拉普拉斯算子
* 使用imfilter函数计算出![image-20230713163205695](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230713163205695.png)

```
>> I=imread('test.jpg');
>> I=rgb2gray(I);
>> f=fspecial('laplacian',0);
>> g=I-imfilter(I,f);
>> subplot(121),imshow(I),subplot(122),imshow(g)

f=imread('test.jpg'); %读取原图像
h1=fspecial('laplacian',0); %拉普拉斯滤波器，等价于拉普拉斯算子掩模中参数为0
g1=f-imfilter(f,h1); %中心为-4，c=-1,即从原图像中减去拉普拉斯算子处理的结果
h2=[1 1 1; 1 -8 1; 1 1 1]; %式（13.4）的滤波器
g2=f-imfilter(f,h2); %中心为-8，c=-1
subplot(1,3,1),imshow(f) %显示原图像
subplot(1,3,2),imshow(g1) %显示滤波器(13.3)修复的图像
subplot(1,3,3),imshow(g2) %显示滤波器(13.4)修复的图像
```

## 空间滤波-非线性空间滤波器

#### 重要函数

```
g=ordfilt2(f, order, domain)
```

使用邻域的一组排序元素中的第order个元素来替代f中的每个元素，而该邻域由domain中的非零元素指定

##### 邻域

#### 最小滤波器

##### 含义：

指一组排序元素中的第一个样本值，即称为第0个百分位

##### matlab函数：

```
g=ordfilt2(f, 1, ones(m,n))
```

#### 中值滤波器

##### 含义：

对应第50个百分位

##### matlab函数：

```
g=ordfilt2(f, median(1:m * n), ones(m,n))
```

或

```
g=medfilter2(f, [m,n]) %函数在m x n的邻域内计算中值，默认为3 x 3
```

##### 代码示例：

```
I=rgb2gray(I);
I1=rgb2gray(I1);
g=medfilt2(I1);
subplot(131),imshow(I),subplot(132),imshow(I1),subplot(133),imshow(g)
```

## 频域变换-傅里叶变换

#### 意义：

把图像从空间域转换到频域，在频域可以更快速有效地处理图像

#### matlab函数：

**这里使用二维离散傅里叶变换（DFT）**

```
fff2()		%matlab快速傅里叶变换
iff2()		%matlab傅里叶逆变换，注意此时返回的数据类型为复数型，若要用inshow显示则需要转换为uint8型数据
```



#### 代码示例：

构造一阶巴特沃兹低通滤波器

```
cm=imread('cameraman.tif');
[n,m]=size(cm);		%计算图像的维数
cf=fft2(cm);		%进行傅里叶变换
cf=fftshift(cf);	%进行中心变换，把频率函数图的中心点变换为0
u=[-floor(m/2):floor((m-1)/2)];		%水平频率，对应矩阵行数
v=[-floor(n/2):floor((n-1)/2)];		%垂直频率，对应矩阵列数
[uu,vv]=meshgrid(u,v);				%频域平面上的网格节点
b1=1./(1+(sqrt(uu.^2+vv.^2)/15).^2);	%构造一阶巴特沃兹低通滤波器
cf1=b1.*cf;								%逐点相乘，进行低通滤波
cm1=real(ifft2(cf1));					%进行傅里叶逆变换，并取实部
%特别注意：ifft2返回的是复数类型的数据，包含实部和虚部，而imshow函数接收的是uint8型数据，故必须进行数据转换
```

fftshift()作用如下：

使用fftshift()前

![fouriertransformsexample_02_zh_CN](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/fouriertransformsexample_02_zh_CN.png)

使用fftshift()后

![fouriertransformsexample_03_zh_CN](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/fouriertransformsexample_03_zh_CN.png)

## 频域变换-离散余弦变换(DCT)？

### 意义：

把图像从空间域转换到频域，在频域可以更快速有效地处理图像，并且较好地利用了人类视觉系统的特点

### 代码示例：

DCT变换基函数

```
T=dctmtx(8);	%8x8的DCT变换矩阵
colormap('gray');	%设置颜色映射矩阵
for m=1:8
	for n=1:8
		subplot(8,8,(m-1)*8+n);
		Y=zeros(8);			%8x8函数中只有一个元素为1，其余元素都为0
		Y(m,n)=1;			%8x8函数中只有一个元素为1，其余元素都为0
		X=T'*Y*T;			%作逆DCT变换
		imagesc(X);			%显示图像
		axis square			%画图区域为矩形
		axis off			%不显示轴线和标号
	end
end
```

DCT变换灰度图像压缩

```
I=imread('cameraman.tif');		
I=im2double(I);		%把数据转为double类型
T=dctmtx(8);		%T为8x8的DCT变换矩阵
%定义正DCT变换的匿名函数，block_struct是matlab内置的结构变量
dct=@(block_struct) T*block_struct.data*T';
B=blockproc(I,[8,8],dct);	%作正DCT变换
mask=[1 1 1 1 0 0 0 0
	 1 1 1 0 0 0 0 0
	 1 1 0 0 0 0 0 0
	 1 0 0 0 0 0 0 0
	 0 0 0 0 0 0 0 0
	 0 0 0 0 0 0 0 0
	 0 0 0 0 0 0 0 0
	 0 0 0 0 0 0 0 0];	%给出掩膜矩阵
%提取低频系数
B2=blockproc(B,[8,8],@(block_struct)mask.*block_struct.data);
%定义DCT逆变换的匿名函数
invdct=@(block_struct) T'*block_struct.data*T;
I2=blockproc(B2,[8 8],invdct);	%作逆DCT变换
subplot(1,2,1),imshow(I);
subplot(1,2,2),imshow(I2);
```

DCT变换彩色图像压缩

```
I=imread("D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\tu7_1.bmp");
I_double=double(I);     %dct2只可接收double型，把图像数据转化为double
for k=1:3
    I_dct(:,:,k)=dct2(I_double(:,:,k));     %使用dct2进行变换
end
I_dct(abs(I_dct)<0.1)=0;    %把dct系数小于0.1的设为0
for k=1:3
    I_idct(:,:,k)=idct2(I_dct(:,:,k));  %dct逆变换
end
I_idct=uint8(I_idct);   %imshow接收uint8型数据
subplot(121),imshow(I)
subplot(122),imshow(I_idct)
```

```
在DCT变换中，掩膜矩阵和限制DCT系数大小是两种不同的压缩方法，它们可以应用于灰度图像和彩色图像。

对于灰度图像，使用掩膜矩阵（也称为量化表）是一种常见的压缩方法。掩膜矩阵中的数值决定了DCT系数的量化步长，通过量化DCT系数，可以减少图像中高频细节的数量，从而实现压缩。掩膜矩阵中的数值可以根据图像的特性和压缩需求进行调整，以达到不同的压缩效果和质量级别。

对于彩色图像，通常不使用掩膜矩阵来压缩颜色通道。这是因为彩色图像的颜色信息通常与图像的细节信息密切相关，直接对颜色通道进行量化可能会导致颜色失真。因此，在彩色图像压缩中，常见的做法是限制DCT系数的大小，以减少高频细节并控制压缩比。通过限制DCT系数的大小，可以在一定程度上保留图像的颜色信息，减少颜色失真的风险。
```

```
对彩色图像和灰度图像应用相同的DCT系数限制（将小于0.1的系数设为0）会有一些不同的影响。

对于彩色图像：

颜色信息丢失：DCT系数小于0.1的部分将被设为0，这可能导致一些颜色细节的丢失。彩色图像的颜色信息分布在各个通道中，因此对DCT系数进行限制可能会影响到颜色的饱和度和准确性。
平滑效果：限制DCT系数会导致高频细节的丢失，使得图像变得更加平滑。这可能会导致一些细节的模糊和边缘的变得更加柔和。
对于灰度图像：

细节丢失：DCT系数小于0.1的部分将被设为0，这可能导致一些细节的丢失。灰度图像的细节信息主要体现在低频部分的DCT系数中，限制系数可能会导致图像的细节变得模糊。
平滑效果：限制DCT系数会使图像变得更加平滑，去除一些高频细节。这可能导致图像整体的平滑效果增强。
```

## 图像保真度和质量

### 客观保真度准则

PSNR峰值信噪比

均方根误差
$$
e_{rms}
$$
越小，

峰值信噪比PSNR越大，处理的图像质量越好

### matlab函数：

```
psnr(A,ref) %A为需要判定的图像，ref为参照图像
```

### 注意：

使用DCT压缩后的图像PSNR值为inf即无穷大

## 水印防伪-基于矩阵奇异值分解

### 矩阵的奇异值分解(SVD)与矩阵的能量

图像的主要能量集中在矩阵的数值较大的奇异值上

### matlab函数：

```
S = svd(A) 以降序顺序返回矩阵 A 的奇异值。

[U,S,V] = svd(A) 执行矩阵 A 的奇异值分解，因此 A = U*S*V'。
```

### 代码示例：

图像的奇异值分解

```
I=imread("D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\Lena.bmp");
I_double=double(I);		%uint8型无法进行svd奇异值分解，转为double型
[u,s,v]=svd(I_double);	
s=diag(s);				%提出对角矩阵的对角线元素，得到一个向量
smax=max(s)				%最大奇异值
smin=min(s)				%最小奇异值
s1=s;
s1(21:end);				%保留前20个大的奇异值，其他奇异值置0
s1=diag(s1);			%把向量变为对角矩阵
g=u * s1 * v';			%计算压缩之后的图像矩阵
g=uint8(g);				%转换为原数据类型uint8进行显示
subplot(121),imshow(I)
subplot(122),imshow(g)
figure,plot(s,'.','color','k')		%画出奇异值对应的点
```

### 噪声对矩阵奇异值的影响

* Weyl定理证明了矩阵奇异值分解的稳定性
  * 当图像被施加小的扰动时（有噪声），图像矩阵的奇异值的变化不会超过扰动矩阵的最大奇异值
  * 因此基于矩阵奇异值分解的数字水印算法具有很好的稳定性，能有效抵御噪声对水印信息的干扰

**应用于水印嵌入：**

基于矩阵奇异值分解的数字水印算法正是想要嵌入的水印信息嵌入到图像矩阵的奇异值中，如果在嵌入水印的过程中选择一个嵌入强度因子来控制水印信息嵌入的强度，那么当嵌入强度因子足够小时，图像在视觉上不会产生明显的变化

## 水印防伪-基于矩阵奇异值分解的水印嵌入

基于矩阵奇异值分解的数字水印算法正是想要嵌入的水印信息嵌入到图像矩阵的奇异值中，如果在嵌入水印的过程中选择一个嵌入强度因子来控制水印信息嵌入的强度，那么当嵌入强度因子足够小时，图像在视觉上不会产生明显的变化

### 示例代码：

SVD水印嵌入

```
I=imread("D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\tu9_1.bmp");
W=imread("D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\tu9_2.bmp");
[m1,m2,m3]=size(W);			%获取水印文件大小、维数
I0=I([1:m1],[1:m2],:);		%在载体图片左上角取水印图片大小相同的小块
% I0=I(:,:,:);				%错误！应取对应于水印图片大小的小块
I0=double(I0);				%svd矩阵奇异值分解需要使用double属性的数值
W=double(W);				%svd矩阵奇异值分解需要使用double属性的数值				
a=0.05;						%设置嵌入强度因子
for i=1:3
    [U1{i},S1{i},V1{i}]=svd(I0(:,:,i));		%用细胞数组来储存图像矩阵不同维度下的奇异值
    I1(:,:,i)=S1{i}+a * W(:,:,i);			%嵌入水印后的图像矩阵=奇异值+嵌入强度因子*水印图像矩阵
    [U2{i},S2{i},V2{i}]=svd(I1(:,:,i));		%求嵌入水印后的图像矩阵的奇异值
    I2(:,:,i)=U1{i}*S2{i}*V1{i}';			%计算处理后的图像矩阵
end
IW=I;									%图像初始化
IW([1:m1],[1:m2],:)=I2;					%把处理后的图像置入原图像的左上角
% IW(:,:,:)=I2;							%错误！嵌入的大小应该恰好为水印图片大小
IW=uint8(IW);							%使图像矩阵数据格式与imshow的uint8型匹配
W=uint8(W);
subplot(131),imshow(I)
subplot(132),imshow(W)
subplot(133),imshow(IW)
```

SVD水印提取

```
I=imread("D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\tu9_1.bmp");
W=imread("D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\tu9_2.bmp");
[m1,m2,m3]=size(W);			%获取水印文件大小、维数
I0=I([1:m1],[1:m2],:);		%在载体图片左上角取水印图片大小相同的小块
% I0=I(:,:,:);				%错误！应取对应于水印图片大小的小块
I0=double(I0);				%svd矩阵奇异值分解需要使用double属性的数值
W=double(W);				%svd矩阵奇异值分解需要使用double属性的数值				
a=0.05;						%设置嵌入强度因子
for i=1:3
    [U1{i},S1{i},V1{i}]=svd(I0(:,:,i));		%用细胞数组来储存图像矩阵不同维度下的奇异值
    I1(:,:,i)=S1{i}+a * W(:,:,i);			%嵌入水印后的图像矩阵=奇异值+嵌入强度因子*水印图像矩阵
    [U2{i},S2{i},V2{i}]=svd(I1(:,:,i));		%求嵌入水印后的图像矩阵的奇异值
    I2(:,:,i)=U1{i}*S2{i}*V1{i}';			%计算处理后的图像矩阵
end
IW=I;									%图像初始化
IW([1:m1],[1:m2],:)=I2;					%把处理后的图像置入原图像的左上角
% IW(:,:,:)=I2;							%错误！嵌入的大小应该恰好为水印图片大小
IW=uint8(IW);							%使图像矩阵数据格式与imshow的uint8型匹配
W=uint8(W);
subplot(131),imshow(I)
subplot(132),imshow(W)
subplot(133),imshow(IW)
%提取水印
IWstar=imnoise(IW,'gaussian',0,0.01);   %通过引入高斯噪声增强水印图像的鲁棒性
I2star=IWstar([1:m1],[1:m2],:);         %在引入噪声后的图像左上角裁剪出水印
I2star=double(I2star);                  %svd处理需要double型数据
for i=1:3
    [U3{i},S2star{i},V3{i}]=svd(I2star(:,:,i));
    I1star(:,:,i)=U2{i}*S2star{i}*V2{i}';       %使用嵌入水印后的图像奇异值，计算水印图像的共轭转置
    Wstar(:,:,i)=(I1star(:,:,i)-S1{i})/a;       %(水印图像的共轭转置矩阵-原图像的奇异值)/嵌入强度因子=水印图像的共轭转置
end
for i=1:3
    Wstar(:,:,i)=medfilt2(Wstar(:,:,i));        %对水印图像进行中值滤波
end
Wstar=uint8(Wstar);
figure,subplot(121),imshow(IWstar)
subplot(122),imshow(Wstar)
```

```
在基于SVD（奇异值分解）方法嵌入的水印技术中，嵌入水印会对图像的奇异值进行修改。当提取水印时，需要从修改后的奇异值中恢复出水印信息。然而，奇异值的恢复过程会受到噪声的影响。

为了提高水印的鲁棒性（鲁棒性是指水印对于一些常见攻击和失真具有较好的保护能力），在提取水印时引入高斯噪声可以使得水印更加鲁棒。高斯噪声的引入可以增加水印的抗干扰能力，降低由于奇异值恢复过程中的噪声引起的误差。通过在嵌入和提取过程中引入高斯噪声，可以增加水印的可靠性和提高水印的正确提取率。

引入高斯噪声的目的是为了增加系统的抗攻击和失真能力，提高水印的可靠性和鲁棒性。
```



## 水印防伪-基于DCT变换的水印算法?

## 图像加密-Henon混沌序列打乱图像矩阵行序与列序

### 简述：

![image-20230714162759157](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/image-20230714162759157.png)

### 代码示例：

加密：

```
% 生成 Henon 混沌序列
n = 256; % 序列长度
x = zeros(n, 1);
y = zeros(n, 1);
x(1) = 0.1;
y(1) = 0.1;
a = 1.4;
b = 0.3;
for i = 2:n
    x(i) = 1 - a * x(i-1)^2 + y(i-1);
    y(i) = b * x(i-1);
end

% 加载图像并获取图像矩阵
img = imread("D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\tu9_1.bmp");
img = rgb2gray(img); % 转换为灰度图像
img_rows = size(img, 1);
img_cols = size(img, 2);

% 打乱行序列
row_indices = 1:img_rows;
row_indices_shuffled = row_indices(randperm(img_rows));

% 打乱列序列
col_indices = 1:img_cols;
col_indices_shuffled = col_indices(randperm(img_cols));

% 创建打乱后的图像矩阵
img_shuffled = img(row_indices_shuffled, col_indices_shuffled);

% 显示原始图像和打乱后的图像
subplot(1, 2, 1);
imshow(img);
title('原始图像');

subplot(1, 2, 2);
imshow(img_shuffled);
title('打乱后的图像');
```

解密：

```
% 生成 Henon 混沌序列
n = 256; % 序列长度
x = zeros(n, 1);
y = zeros(n, 1);
x(1) = 0.1;
y(1) = 0.1;
a = 1.4;
b = 0.3;
for i = 2:n
    x(i) = 1 - a * x(i-1)^2 + y(i-1);
    y(i) = b * x(i-1);
end

% 加载打乱后的图像和打乱后的行列索引
%img_shuffled = imread('shuffled_image.jpg');
%row_indices_shuffled = load('row_indices.txt');
%col_indices_shuffled = load('col_indices.txt');

% 恢复原始的行列索引
row_indices = zeros(n, 1);
col_indices = zeros(n, 1);
for i = 1:n
    row_indices(row_indices_shuffled(i)) = i;
    col_indices(col_indices_shuffled(i)) = i;
end

% 恢复原始图像
img_recovered = img_shuffled(row_indices, col_indices);

% 显示恢复后的图像
imshow(img_recovered);
title('恢复后的图像');
```

## 图像隐藏-基于空域LSB的图像隐藏算法

### 简述：

* 对于uint8数据类型的灰度图像矩阵，灰度级别从0-255，共256个灰度级别
* 256个灰度级别对应8位二进制数，即可按从高到低分为8个位平面
* 且人眼对低位平面不敏感，则对被加密图片的灰度级别的低位进行处理

### 代码示例：

Henon混沌序列加密+LSB图像隐藏

```
clc, clear
secret=imread('D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\tu11_1.bmp'); ws1=size(secret);    %读入保密图像，并计算维数
base=imread('D:\D.文档\matlab_file\数学建模算法与应用（第3版）源程序\程序及数据\13第13章  数字图像处理\tu11_2.bmp'); ws2=size(base);   %读入载体图像，并计算维数
resize_base=imresize(base,ws1(1:2));              %把载体图像变换成与保密图像同样大小

%首先利用henon序列对加密图像secret进行加密，但是只对行序列进行打乱
key=-0.400001;                                    %给出密钥，即混沌序列的初始值
L=max(ws1); x(1)=key; y(1)=key; a=1.4; b=0.3;
% L=max(ws1(1)); x(1)=key; y(1)=key; a=1.4; b=0.3;         

for i=1:L-1                                       %生成两个混沌序列,此时生成的是最大的维度的数值对应的方阵
     x(i+1)=1-a*x(i)^2+y(i); y(i+1)=b*x(i);
end
x(ws1(1)+1:end)=[];                               %删除x后面一部分元素，使之与图片的正常大小对应
[sx,ind1]=sort(x); [sy,ind2]=sort(y);             %对混沌序列按照从小到大排序
en_secret(ind1,ind2,:)=secret;                    %打乱保密图像的行序和列序，生成加密图像矩阵en_secret
imshow(en_secret)                                 %显示保密图像加密后得到的图像

resize_base2=bitand(resize_base,240);             %载体图像与11110000(（二进制）=240(十进制）)逐位与运算
en_secret2=bitand(en_secret,240);                 %加密图像与11110000逐位与运算
en_secret2=en_secret2/16;                         %加密图像高4位移到低4位
mix=bitor(resize_base2,en_secret2);               %把加密图像嵌入载体图像的低4位，构造合成图像
mix2=bitand(mix,15)*16;                           %这里15（十进制）=00001111,提取加密图像的高4位，
mix3=mix2(ind1,ind2,:);                           %对加密图像进行解密
figure, subplot(1,2,1), imshow(mix3)              %显示提取的并解密以后的原图像
subplot(1,2,2),imshow(mix)                        %显示嵌入加密图像的合成图像
```

