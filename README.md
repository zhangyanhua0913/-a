以下是整理后的 `README.md` 文档内容：

---

# 接口文档

本接口支持提取本地音视频文件及抖音主页所有视频的文案，同时支持单链接提取文案，支持短视频链接解析，主页视频解析等。覆盖二十多个常见平台。所有提取的文案均经过格式化处理，采用最新的大语言模型，准确率极高，无论是国内外语言，还是国内各地方言，均可高效处理。接口响应速度快，定价合理，使用便捷，支持高并发调用，可广泛应用于各类场景。我们还提供了丰富的程序模板，助您快速打造专属产品。

---

## 密钥 Key 渠道   

客服微信：baihuaabd
  --- 购买渠道：http://shop.92k.fun/  （访问时不要挂梯子）

---

## 接口列表

### 1. **主页视频链接提取接口**

#### 接口地址
```
POST https://api2.92k.fun/fetchs-videos_zhuye
```

#### 功能描述
返回的视频结果顺序是从前往后，最新的就是第一个。根据用户提供的主页链接，提取指定数量的视频链接。每次请求最少消耗 10 个积分。积分消耗规则如下：
- 请求 1-20 个视频，消耗 10 个积分。
- 请求 21-30 个视频，消耗 20 个积分。
- 以此类推。

#### 请求参数
| 参数名            | 类型   | 必填 | 描述                          |
|-------------------|--------|------|-------------------------------|
| `extract_count`   | int    | 是   | 需要提取的视频数量个数。      |
| `device_identifier` | string | 是   | 密钥 Key。                    |
| `home_link`       | string | 是   | 用户主页链接（仅支持抖音，后续支持快手、小红书等）。 |

#### 请求示例
```json
{
  "extract_count": 5,
  "device_identifier": "sk-xfafemcaksjdfsldfkifealsadfegadfasdfdkfeo",
  "home_link": "https://www.douyin.com/user/MS4wLjABAAAANHP1mMBt21lgn7ThBHII4rxlzsFb6OwVKuNPeSrw_uqXA4sSYV1J1A_SyaSPZ9lp?from_tab_name=main&vid=7436569894923095307"
}
```

#### 返回参数
| 参数名            | 类型   | 描述                          |
|-------------------|--------|-------------------------------|
| `nickname`        | string | 博主昵称。                    |
| `remaining_points`| int    | 剩余积分。                    |
| `xiaohao`         | int    | 本次请求消耗的积分。          |
| `num`             | int    | 实际提取的视频数量。          |
| `videos`          | list   | 提取的视频链接列表，包含标题和视频链接。 |

#### 返回示例
```json
{
  "nickname": "抖音用户",
  "remaining_points": 90,
  "xiaohao": 10,
  "num": 5,
  "videos": [
    {
      "title": "视频标题1",
      "videoSrc": "https://www.douyin.com/video/123456789"
    },
    {
      "title": "视频标题2",
      "videoSrc": "https://www.douyin.com/video/987654321"
    }
  ]
}
```

---

### 2. **主页视频链接提取并转文案接口**

#### 接口地址
```
POST https://api2.92k.fun/fetchs-videos_zhuye_wa
```

#### 功能描述
根据用户提供的主页链接，提取指定数量的视频链接，并对每个视频进行音频转文案处理。积分消耗规则如下：
- 主页解析视频按照区间计算规则（请求 1-20 个视频消耗 10 个积分，请求 21-30 个视频消耗 20 个积分）。
- 每个视频转文案按视频时长消耗积分，每分钟扣 1 个积分。

**示例**：提取主页下 15 个视频，每个视频都是 1 分钟，共计消耗积分：`10 + 15 = 25` 积分。

#### 请求参数
| 参数名            | 类型   | 必填 | 描述                          |
|-------------------|--------|------|-------------------------------|
| `extract_count`   | int    | 是   | 需要提取的视频数量个数。如果全部提取，输入一个较大的数字（如 1000）。 |
| `device_identifier` | string | 是   | 密钥 Key。                    |
| `home_link`       | string | 是   | 用户主页链接（抖音、快手、小红书等）。 |

#### 请求示例
```json
{
  "extract_count": 3,
  "device_identifier": "sk-dfefeiskdfsldkfjeialdfjeldfeifaodfkdfje",
  "home_link": "https://www.douyin.com/user/MS4wLjABAAAANHP1mMBt21lgn7ThBHII4rxlzsFb6OwVKuNPeSrw_uqXA4sSYV1J1A_SyaSPZ9lp?from_tab_name=main&vid=7436569894923095307"
}
```

#### 返回参数
| 参数名            | 类型   | 描述                          |
|-------------------|--------|-------------------------------|
| `nickname`        | string | 博主昵称。                    |
| `remaining_points`| int    | 剩余积分。                    |
| `num`             | int    | 实际提取的视频数量。          |
| `total`           | int    | 总视频数量。                  |
| `processed`       | int    | 成功转文案的视频数量。        |
| `videos`          | list   | 视频列表，包含标题、视频链接、文案内容等。 |

#### 返回示例
```json
{
  "video_links": {
    "nickname": "博主昵称",
    "remaining_points": 80,
    "num": 10,
    "total": 10,
    "processed": 10,
    "videos": [
      {
        "sequence_number": 1,
        "title": "视频标题",
        "videoSrc": "无水印视频链接",
        "text_content": "原始文本",
        "srt_content": "SRT字幕格式文本",
        "formatted_text": "格式化后的文本",
        "duration_minutes": 2,
        "status": "success"
      }
    ]
  }
}
```

---

### 3. **单视频链接解析接口**

#### 接口地址
```
POST https://api2.92k.fun/watermarke/parses_DZP
```

#### 功能描述
解析单个视频链接，返回视频标题、视频链接、封面链接、图集信息等。每次请求消耗 1 个积分。

#### 请求参数
| 参数名            | 类型   | 必填 | 描述                          |
|-------------------|--------|------|-------------------------------|
| `link`            | string | 是   | 需要解析的视频链接。          |
| `device_identifier` | string | 是   | 密钥 Key。                    |

#### 请求示例
```json
{
  "link": "https://www.douyin.com/video/123456789",
  "device_identifier": "sk-dfeildfeifejfieflakdjfeioflkdfjoeiflaskdfjaldlfe"
}
```

#### 返回参数
| 参数名            | 类型   | 描述                          |
|-------------------|--------|-------------------------------|
| `title`           | string | 视频标题。                    |
| `videoSrc`        | string | 视频链接。                    |
| `imageAtlas`      | list   | 图集信息（如果有）。          |
| `imageSrc`        | string | 视频封面链接。                |
| `remaining_points`| int    | 剩余积分。                    |

#### 返回示例
```json
{
  "title": "视频标题",
  "videoSrc": "https://www.douyin.com/video/123456789",
  "imageAtlas": [
    {
      "imageSrc": "https://www.douyin.com/image/123456789"
    }
  ],
  "imageSrc": "https://www.douyin.com/cover/123456789",
  "remaining_points": 99
}
```

---

### 4. **单视频链接解析并转文案接口**

#### 接口地址
```
POST https://api2.92k.fun/watermarke/parses_DZP_wa
```

#### 功能描述
解析单个视频链接，并返回视频标题、视频链接、封面链接、图集信息以及文案内容。转文案按视频时长消耗积分，每分钟扣 1 个积分（不足 1 分钟按 1 分钟计算）。

#### 请求参数
| 参数名            | 类型   | 必填 | 描述                          |
|-------------------|--------|------|-------------------------------|
| `link`            | string | 是   | 需要解析的视频链接。          |
| `device_identifier` | string | 是   | 密钥 Key。                    |

#### 请求示例
```json
{
  "link": "https://www.douyin.com/video/123456789",
  "device_identifier": "sk-dffjijfekfjiufefkasjfiejflaskjfeiofaksdfjiefjasfd"
}
```

#### 返回参数
| 参数名            | 类型   | 描述                          |
|-------------------|--------|-------------------------------|
| `title`           | string | 视频标题。                    |
| `videoSrc`        | string | 视频链接。                    |
| `imageAtlas`      | list   | 图集信息（如果有）。          |
| `imageSrc`        | string | 视频封面链接。                |
| `remaining_points`| int    | 剩余积分。                    |
| `text_content`    | string | 文案内容（纯文本格式）。      |
| `srt_content`     | string | 文案内容（SRT 格式）。        |
| `formatted_text`  | string | 文案内容（格式化文本）。      |
| `duration_minutes`| int    | 视频时长（分钟）。            |

#### 返回示例
```json
{
  "title": "视频标题",
  "videoSrc": "https://www.douyin.com/video/123456789",
  "imageAtlas": [
    {
      "imageSrc": "https://www.douyin.com/image/123456789"
    }
  ],
  "imageSrc": "https://www.douyin.com/cover/123456789",
  "remaining_points": 98,
  "text_content": "这是视频的文案内容...",
  "srt_content": "1\n00:00:00,000 --> 00:00:10,000\n这是视频的文案内容...",
  "formatted_text": "这是视频的文案内容...",
  "duration_minutes": 2
}
```

---

## 注意事项

1. **积分消耗**：
   - 每个接口调用都会消耗积分，具体消耗值见接口描述。
   - 积分不足时，接口会返回错误信息。

2. **错误处理**：
   - 如果请求失败，接口会返回 HTTP 状态码和错误信息，例如：
     ```json
     {
       "detail": "积分不足：您的积分已用完"
     }
     ```

3. **请求频率**：
   - 请合理控制请求频率，避免频繁调用导致积分快速消耗。

4. **超时设置**：
   - 建议设置较长的超时时间（如 `timeout=50000`），以确保长时间任务不会因超时中断。

5. **常见错误码**：
   - `400`：积分不足。
   - `406`：密钥 Key 无效。
   - `407`：密钥 Key 有误。
   - `500`：服务器内部错误。

---

## 请求示例代码

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

以下是继续的内容：

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

## 常见问题

### 1. **积分消耗规则**
- 主页解析视频按区间消耗积分：
  - 1-20 个视频：10 积分。
  - 21-30 个视频：20 积分。
  - 以此类推。
- 转文案按视频时长消耗积分：
  - 每分钟消耗 1 积分（不足 1 分钟按 1 分钟计算）。

### 2. **超时设置**
- 建议设置较长的超时时间（如 `timeout=50000`），以确保长时间任务不会因超时中断。

### 3. **错误码说明**
- `400`：积分不足。
- `406`：密钥 Key 无效。
- `407`：密钥 Key 有误。
- `500`：服务器内部错误。

### 4. **注意事项**
- 所有接口都需要传入密钥 Key。
- 积分不足时将无法使用服务。
- 建议在调用接口前先检查剩余积分。
- 批量解析接口建议控制提取数量，避免积分消耗过快。

---

## 总结

以上是四个接口的详细文档及请求示例代码，开发者可以根据需求选择合适的接口进行调用。如果有任何问题，请联系客服获取支持。

---

希望这份 `README.md` 文档对您有所帮助！如果有其他需求，请随时告知。
