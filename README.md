# collection_of_OCR_APIs
各种 OCR 接口收集，百度OCR


---

## 百度 OCR 在线版

不需要注册百度 OCR 应用，可以直接在线使用，网址：https://ai.baidu.com/tech/ocr/general

可以应对普通需求，图片大小有限制，而且微博长图基本上毛都识别不出来。

- type_ 值可以选择不同 OCR 版本；
- 在线图片：image_url 值传入图片链接；
- 本地图片：image 值传入图片 base64 码；
- 不带 cookie 访问 20 次，就会被禁用一段时间；
带上 cookie 大约每 10 秒可以访问 20 次。在浏览器找一下 cookie 值。

```python
import requests, json

# 图片链接
image_url = 'https://ai.bdstatic.com/file/25C60B51D36E40C4AF579CD439429448'

# 高精度版
type_ = 'https://aip.baidubce.com/rest/2.0/ocr/v1/accurate_basic'
# 高精度含位置版
# type_ = 'https://aip.baidubce.com/rest/2.0/ocr/v1/accurate'
# 标准版
# type_ = 'https://aip.baidubce.com/rest/2.0/ocr/v1/general_basic'
# 标准含位置版
# type_ = 'https://aip.baidubce.com/rest/2.0/ocr/v1/general'

data = {
    'image': '',
    'image_url' : image_url,
    'type' : type_,
    'detect_direction': 'false'
}

# 本地图片需要转成 base64 码，传入'image'值中
# import base64
# with open("C:\\Users\\wonai\\Desktop\\1.jpg","rb") as f:
#     base64_data = base64.b64encode(f.read())
# data = {
#     'image': base64_data,
#     'image_url' : '',
#     'type' : type_,
#     'detect_direction': 'false'
# }

headers = {
    'user-agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36',
    'cookie': '浏览器找一下 cookie'
}

baidu_api_url = 'https://ai.baidu.com/aidemo'
resp = requests.post(baidu_api_url, headers = headers, data = data)
rt = json.loads(resp.text)
print(rt)

```
