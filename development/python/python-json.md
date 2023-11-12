Python에서 JSON 포맷 데이터 다루기
===============================

### json.load vs json.loads
* `json.load()` : JSON 형태의 **파일 읽기**

json 파일 (현재 디렉토리에 위치)
```json
{
    "key1" : "value1",
    "key2" : "value2"
}
```
```python
import json

json_data_path = "./data.json"

with open(json_data_path, "r") as json_data:
    data = json.load(json_data)

print(data)


{'key1': 'value1', 'key2': 'value2'}
```

* `json.loads()` : JSON 형태의 **문자열 읽기**
```python
import json

json_data = '{"key1" : "value1", "key2" : "value2"}'

data = json.loads(json_data)

print(data)


{'key1': 'value1', 'key2': 'value2'}
```