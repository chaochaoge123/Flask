# 1. flask实例
```
from flask import Flask
app=Fladk(__name__)
@app.route('/')
def hello_world():
    return 'Hello World!'
```

### 2.返回方式
- return "hello"  返回字符串
- jsonify    返回json格式
- render_template 返回模板
- redirect  重定向
- send_file 打开文件并返回

### 3. request
```
@app.route('/login',methods= ('POST','GET'))
def reque():
    print(request .method )
    if request .method =='POST':
        print(request .values,type(request .values ))
        print(request .values .to_dict()) # 前台数据字典形式
        urluser_name=request.args.get('username')
        username=request .form.get('username')
        password=request .form.get('password')
        print(request .path)
        
        #上传文件，保存
        print(request.files, type(request.files))
        f=request .files['my']
        f.save(f.filename)

        if username=='yin' and password =='gg':
            session['user']=username
            return redirect('/file')
    return render_template('tset.html')
--------------------------------------
方法和属性：
1、方法
args   url地址当中的参数
form   POST请求体中的FormData中的数据
values  获取所有参数(url,formdata)
request.data   
request.json content-type:application/json 将数据序列化字典中
request.files 获取Formdata中的文件
2、属性
method 请求方式
url 完整地址
host 前半段儿 http://111.111.111.111:5000/
path 后半段儿 /login
```
### 4. 模板语言(jinja2)
```
{{  }}  非逻辑代码
{%  %}	逻辑代码
```
### 5. 路由
```
@app.route('/log',methods= ("POST","GET"),endpoint= 'mylog')
# endpoint= 'mylog' 反向解析
# redirect_to= '/log'  重定向
# defaults= {'nid':10}  默认参数
# strict_slashes=True  严格url格式
def hello():
     return 'Hello World!'

# /index/<int:nid> 动态路由
@app.route('/index/<int:nid>', endpoint='myindex', )
def index(nid):
    print(nid)
    return url_for(endpoint='myundex', nid=nid)  # 返回url后半部分
```
### 6. flask配置
- 参考地址
`https://www.cnblogs.com/DragonFire/p/9260299.html`
- 实例化配置`app = Flask(__name__)`
```
常用配置：
static_folder = 'static',  # 静态文件目录的路径 默认当前项目中的static目录
static_url_path = None,  # 静态文件目录的url路径 默认不写是与static_folder同名,远程静态文件时复用
template_folder = 'templates'  # template模板目录, 默认当前项目中的 templates 目录
static_host: 指定远程的IP，访问远程的资源
```
- 对象配置`app.run()`
```
'SECRET_KEY': None,  # 之前遇到过,在启用Session的时候,一定要有它
'SESSION_COOKIE_NAME': 'session',  # 在cookies中存放session加密字符串的名字
'JSONIFY_MIMETYPE': 'application/json'
----------------------------------
配置文件：
class FlaskConfigDebug(object):
	DEBUG = True
	SECRET_KEY = "DragonFire"

在视图文件导入：
app.config.from_object(FlaskConfigDebug)  导入配置文件
```











