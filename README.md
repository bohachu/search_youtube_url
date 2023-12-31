# search-youtube-url

這是一個 Python 套件，可以用來搜尋 YouTube 影片並取得其網址。

## 安裝

使用 pip 來安裝 search-youtube-url：

```bash
pip install search-youtube-url
```

## 使用方法

首先，你需要從 Google Cloud Platform 取得 YouTube Data API v3 的 API 金鑰，並設定為環境變數 `YOUTUBE_API_KEY`。

然後，你可以使用 `search_youtube_url` 函數來搜尋 YouTube 影片：

```python
from googleapiclient.discovery import build
import os
from dotenv import load_dotenv

def search_youtube_url(query):
    load_dotenv()
    api_key = os.getenv('YOUTUBE_API_KEY')
    youtube = build('youtube', 'v3', developerKey=api_key)
    request = youtube.search().list(
        part="snippet",
        maxResults=1,
        q=query
    )
    response = request.execute()
    if not response['items']:
        return "No video found"
    video_id = response['items'][0]['id']['videoId']
    video_url = f"https://www.youtube.com/watch?v={video_id}"
    return video_url

if __name__ == "__main__":
    query = "Could an orca give a TED Talk?"
    print(search_youtube_url(query))
```

這個函數會回傳搜尋結果中的第一個影片的網址。如果找不到影片，則會回傳 "No video found"。

## 開發

如果你想要參與開發，請先安裝開發所需的套件：

```bash
pip install -r requirements.txt
```
@end
