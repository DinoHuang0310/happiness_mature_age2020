# newenergyforum2020
 
 ### Follow the rules when you git
  1. feat: 新功能 (feature)
  2. fix: 修補bug
  3. doc: 文件 (documentation)
  4. style: 樣式 (不影響程式碼運行之異動)
  5. refactor: 重構 (未新增功能或修補bug之程式碼異動)
  6. test: 增加測試
  7. chore: 構建過程或輔助工具之異動


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run-script build
```
## data format
```
{
    "about": "引言(html)",
    "spotlight": [
        {
            "val": 數值,
            "unit": "單位",
            "description": "描述"
        }
    ],
    "speakers": [
        {
            "image": "圖檔url",
            "position": "抬頭",
            "name": "姓名",
            "experience": [ // 選填
                {
                    "title": "標題",
                    "subtitle": "小標",
                    "list": ["清單"]
                }
            ],
            "description": ["描述"] // 選填
        }
    ],
    "formState": {
        "active": Boolean(是否開放報名),
        "successMessage": "報名成功alert訊息",
        "closeMessage": "關閉報名的公告(html)",
        "alert": ["報名須知"]
    },
    "exhibitor": [
        {
            "title": "標題",
            "description": "描述"
        }
    ],
    "slider": [
        {
            "title": "標題",
            "url": "url",
            "image": "圖檔url"
        }
    ],
    "agencys": [
        {
            "title": "標題",
            "list": [{
                    "title": "圖檔alt",
                    "image": "圖檔url",
                    "url": "url(選填)"
                }
            ]
        }
    ]
}
```