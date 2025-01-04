博客地址 http://zhuzimiko.com/
# BetterDirsearchDictionary
优化后的更好的Dirsearch字典
#### 来源
今天在做buuctf的`[BJDCTF2020]EasySearch`，开始扫目录但是什么都没有扫到。看wp发现第一步是扫目录扫描到了`index.php.swp`文件。疑惑于自己为什么扫不到。于是看了看自己dirsearch的字典（用的dirsearch默认的），发现里面是有`index.php.swp`的
![](http://www.zhuzimiko.com/Study/368bd832-39de-41ac-b446-3e129856b65e.png)
那么为啥扫描不到呢？为了方便测试，我把字典做了修改，仅包含`index.php.swp`进行扫描，抓包发现，返回结果是404，而在题目环境中直接访问，返回的是302
![](http://www.zhuzimiko.com/Study/3984fab8-c4f2-4ed6-8e5a-26ce38401bb3.png)
![](http://www.zhuzimiko.com/Study/80adfb90-c39f-4ca9-99b3-27fffacf1486.png)
对比发现，是`dirsearch`的字典中多了一个`.`至于为什么，我也不是很清楚，于是我打算在字典中加入所有删除了`.`开头的字典内容。（保留有`.`的），便于提高扫描准确度
```py
# 打开输入文件进行读取
input_file = "cnm"  # 替换为你的文件名
output_file = "output.txt"  # 输出文件名
# 读取文件并处理每一行
with open(input_file, "r", encoding="utf-8") as infile:
    lines = infile.readlines()
# 删除每行开头的.并写入新文件
with open(output_file, "w", encoding="utf-8") as outfile:
    for line in lines:
        outfile.write(line.lstrip("."))
print(f"处理完成！修改后的文件已保存为 {output_file}")
```
