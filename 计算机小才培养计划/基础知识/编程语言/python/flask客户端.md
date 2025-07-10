## 网络请求：

### 格式

如果您希望继续使用 `GET` 请求，那么您应该从查询参数中获取数据，而不是尝试从请求体中获取。
```python
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/api', methods=['GET'])
def api():
    # 从查询参数中获取数据
    message = request.args.get('message', '')
    data = work(message)
    print(data)
    # 处理数据...
    # 返回响应
    #返回数据的格式
    return jsonify({
        'status': 'success',
        'message': data
    })
```

在这个例子中，`request.args.get('message', '')` 用于从查询参数中安全地获取 `message` 参数的值，如果参数不存在，则返回空字符串。