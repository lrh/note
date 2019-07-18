
# 编码转换 utf8

```python
import chardet

# 其他编码转化成utf-8编码
def ConvertTo(filename, out_enc="UTF8"):
    try:
        # print("convert " + filename)
        with open(filename) as fcontent:
            content = fcontent.read()
            result = chardet.detect(content)  # 通过chardet.detect获取当前文件的编码格式串，返回类型为字典类型
            coding = result.get('encoding')  # 获取encoding的值[编码格式]
            if not coding:
                print("coding nil " + filename)
            elif coding != 'utf-8':  # 文件格式如果不是utf-8的时候，才进行转码
                print(str(coding) + " to utf-8 " + str(filename))
                from_coding = coding
                if from_coding == 'GB2312':
                    from_coding = 'gbk'
                    pass
                new_content = content.decode(from_coding).encode(out_enc)
                with open(filename, 'w') as f:
                    f.write(new_content)
                # print("done")
            else:
                print("other " + coding + " " + filename)
    except IOError:
        print("error")
```
