以下是按照 `README.md` 格式整理的文档内容：

---

# 接口请求示例代码

本接口支持提取本地音视频文件及抖音主页所有视频的文案，同时支持单链接提取文案，覆盖二十多个常见平台。所有提取的文案均经过格式化处理，采用最新的大语言模型，准确率极高，无论是国内外语言，还是国内各地方言，均可高效处理。接口响应速度快，定价合理，使用便捷，支持高并发调用，可广泛应用于各类场景。我们还提供了丰富的程序模板，助您快速打造专属产品。

---

## 接口请求示例

### 1. **`/fetchs-videos_zhuye` 请求示例**

#### 使用 `requests` 库（同步请求）
```python
import requests

url = "https://api2.92k.fun/fetchs-videos_zhuye"
payload = {
    "extract_count": 5,
    "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo",
    "home_link": "https://www.douyin.com/user/MS4wLjABAAAANHP1mMBt21lgn7ThBHII4rxlzsFb6OwVKuNPeSrw_uqXA4sSYV1J1A_SyaSPZ9lp?from_tab_name=main&vid=7436569894923095307"
}

print("主页提取文案需要时间，请耐心等待...")
try:
    response = requests.post(url, json=payload, timeout=50000)  # 设置超时时间为 50000 秒
    if response.status_code == 200:
        print("请求成功！")
        print(response.json())
    else:
        print(f"请求失败，状态码：{response.status_code}")
        print(response.json())
except requests.Timeout:
    print("请求超时，请检查网络连接或稍后重试。")
except Exception as e:
    print(f"请求发生错误：{e}")
```

#### 使用 `httpx` 库（异步请求）
```python
import httpx
import asyncio

async def fetch_videos():
    url = "https://api2.92k.fun/fetchs-videos_zhuye"
    payload = {
        "extract_count": 5,
        "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo",
        "home_link": "https://www.douyin.com/user/MS4wLjABAAAANHP1mMBt21lgn7ThBHII4rxlzsFb6OwVKuNPeSrw_uqXA4sSYV1J1A_SyaSPZ9lp?from_tab_name=main&vid=7436569894923095307"
    }

    print("主页提取文案需要时间，请耐心等待...")
    try:
        async with httpx.AsyncClient(timeout=50000) as client:  # 设置超时时间为 50000 秒
            response = await client.post(url, json=payload)
            if response.status_code == 200:
                print("请求成功！")
                print(response.json())
            else:
                print(f"请求失败，状态码：{response.status_code}")
                print(response.json())
    except httpx.Timeout:
        print("请求超时，请检查网络连接或稍后重试。")
    except Exception as e:
        print(f"请求发生错误：{e}")

asyncio.run(fetch_videos())
```

---

### 2. **`/fetchs-videos_zhuye_wa` 请求示例**

#### 使用 `requests` 库（同步请求）
```python
import requests

url = "https://api2.92k.fun/fetchs-videos_zhuye_wa"
payload = {
    "extract_count": 3,
    "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo",
    "home_link": "https://www.douyin.com/user/MS4wLjABAAAANHP1mMBt21lgn7ThBHII4rxlzsFb6OwVKuNPeSrw_uqXA4sSYV1J1A_SyaSPZ9lp?from_tab_name=main&vid=7436569894923095307"
}

print("主页提取文案需要时间，请耐心等待...")
try:
    response = requests.post(url, json=payload, timeout=50000)  # 设置超时时间为 50000 秒
    if response.status_code == 200:
        print("请求成功！")
        print(response.json())
    else:
        print(f"请求失败，状态码：{response.status_code}")
        print(response.json())
except requests.Timeout:
    print("请求超时，请检查网络连接或稍后重试。")
except Exception as e:
    print(f"请求发生错误：{e}")
```

#### 使用 `httpx` 库（异步请求）
```python
import httpx
import asyncio

async def fetch_videos_with_captions():
    url = "https://api2.92k.fun/fetchs-videos_zhuye_wa"
    payload = {
        "extract_count": 3,
        "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo",
        "home_link": "https://www.douyin.com/user/MS4wLjABAAAANHP1mMBt21lgn7ThBHII4rxlzsFb6OwVKuNPeSrw_uqXA4sSYV1J1A_SyaSPZ9lp?from_tab_name=main&vid=7436569894923095307"
    }

    print("主页提取文案需要时间，请耐心等待...")
    try:
        async with httpx.AsyncClient(timeout=50000) as client:  # 设置超时时间为 50000 秒
            response = await client.post(url, json=payload)
            if response.status_code == 200:
                print("请求成功！")
                print(response.json())
            else:
                print(f"请求失败，状态码：{response.status_code}")
                print(response.json())
    except httpx.Timeout:
        print("请求超时，请检查网络连接或稍后重试。")
    except Exception as e:
        print(f"请求发生错误：{e}")

asyncio.run(fetch_videos_with_captions())
```

---

### 3. **`/watermarke/parses_DZP` 请求示例**

#### 使用 `requests` 库（同步请求）
```python
import requests

url = "https://api2.92k.fun/watermarke/parses_DZP"
payload = {
    "link": "https://www.douyin.com/video/123456789",
    "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo"
}

print("主页提取文案需要时间，请耐心等待...")
try:
    response = requests.post(url, json=payload, timeout=50000)  # 设置超时时间为 50000 秒
    if response.status_code == 200:
        print("请求成功！")
        print(response.json())
    else:
        print(f"请求失败，状态码：{response.status_code}")
        print(response.json())
except requests.Timeout:
    print("请求超时，请检查网络连接或稍后重试。")
except Exception as e:
    print(f"请求发生错误：{e}")
```

#### 使用 `httpx` 库（异步请求）
```python
import httpx
import asyncio

async def parse_video():
    url = "https://api2.92k.fun/watermarke/parses_DZP"
    payload = {
        "link": "https://www.douyin.com/video/123456789",
        "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo"
    }

    print("主页提取文案需要时间，请耐心等待...")
    try:
        async with httpx.AsyncClient(timeout=50000) as client:  # 设置超时时间为 50000 秒
            response = await client.post(url, json=payload)
            if response.status_code == 200:
                print("请求成功！")
                print(response.json())
            else:
                print(f"请求失败，状态码：{response.status_code}")
                print(response.json())
    except httpx.Timeout:
        print("请求超时，请检查网络连接或稍后重试。")
    except Exception as e:
        print(f"请求发生错误：{e}")

asyncio.run(parse_video())
```

---

### 4. **`/watermarke/parses_DZP_wa` 请求示例**

#### 使用 `requests` 库（同步请求）
```python
import requests

url = "https://api2.92k.fun/watermarke/parses_DZP_wa"
payload = {
    "link": "https://www.douyin.com/video/123456789",
    "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo"
}

print("主页提取文案需要时间，请耐心等待...")
try:
    response = requests.post(url, json=payload, timeout=50000)  # 设置超时时间为 50000 秒
    if response.status_code == 200:
        print("请求成功！")
        print(response.json())
    else:
        print(f"请求失败，状态码：{response.status_code}")
        print(response.json())
except requests.Timeout:
    print("请求超时，请检查网络连接或稍后重试。")
except Exception as e:
    print(f"请求发生错误：{e}")
```

#### 使用 `httpx` 库（异步请求）
```python
import httpx
import asyncio

async def parse_video_with_captions():
    url = "https://api2.92k.fun/watermarke/parses_DZP_wa"
    payload = {
        "link": "https://www.douyin.com/video/123456789",
        "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo"
    }

    print("主页提取文案需要时间，请耐心等待...")
    try:
        async with httpx.AsyncClient(timeout=50000) as client:  # 设置超时时间为 50000 秒
            response = await client.post(url, json=payload)
            if response.status_code == 200:
                print("请求成功！")
                print(response.json())
            else:
                print(f"请求失败，状态码：{response.status_code}")
                print(response.json())
    except httpx.Timeout:
        print("请求超时，请检查网络连接或稍后重试。")
    except Exception as e:
        print(f"请求发生错误：{e}")

asyncio.run(parse_video_with_captions())
```

---

## 关键点说明

1. **超时设置**：
   - `timeout=50000` 表示请求的超时时间为 50000 秒（约 13.9 小时），确保长时间任务不会因超时中断。
   - 如果任务完成时间较短，可以适当减少超时时间。

2. **用户提示**：
   - 在请求开始前，打印提示信息 `"主页提取文案需要时间，请耐心等待..."`，提醒用户任务可能需要较长时间。

3. **错误处理**：
   - 捕获 `Timeout` 异常，提示用户检查网络连接或稍后重试。
   - 捕获其他异常，打印错误信息以便调试。

---

以上是更新后的代码示例，开发者可以直接使用或根据需求进一步调整。

--- 

希望这份 `README.md` 文档对您有所帮助！如果有其他需求，请随时告知。
