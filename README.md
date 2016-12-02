# yiqixieAPI
yiqixieAPIDocument
YIQIXIE-OPEN-API sample code
https://coding.net/u/yiqixie/p/yiqixie-open-API/git
接入一起写进行开发，可以按照下面目录提示操作：
申请API
User Provisioning API
创建用户
删除用户
获取用户列表
获取用户信息
更改用户信息
Token API
获取refresh token(or long lived token)
获取oauth access token(or short lived token)
Document API
创建文档
创建表格
创建演示
创建文件夹
更新文档/共享设置
获取文档属性
复制文档
复制表格
IFRAMEING API
文档嵌入链接
表格嵌入链接
演示嵌入链接
Doc/Docx Upload&Writeback API
文档导入
表格导入
文档导出
表格导出









申请API
注：只有企业号才可以申请API，企业版申请操作点击Link。
        一起写按APP进行开发管理，每一个APP对应一个具有开发功能的企业号，具有一组api_key/secret_key。开发者API调用依靠时，一起写通过api_key和secret_key进行识别和鉴权。
       使用一起写进行开发，开发者需要为每个APP创建一个一起写企业账号。
       企业号默认不具备开发功能，切换为企业号后，通过右上角头像下的“帐户信息”进入企业号管理，申请成为开发者。
         提交申请，并经由一起写管理员后台审批通过后，开发者可以在此页面获得api_key和secret_key。开发者申请时提交的邮箱同时也会收到包含api_key与secret_key。

一起写开放平台遵循Two Legged OAuth2协议标准, 将来会支持three legged oauth标准.



User Provisioning API
创建用户
路径：https://yiqixie.com/e/api/user/create
参数说明：
参数
是否必须
说明
api_key
是
应用的唯一标识
secret_key
是
分配的唯一密钥
local_id
是
第三方用户的唯一id，不可更改
需要开发者自己维护的本地用户id
email
是
第三方用户的唯一邮箱，可更新
display_name
是
用户昵称，可更新
profile_url
是
用户头像的url，可更新
请求示例：
https://yiqixie.com/e/api/user/create?api_key=k6rqo598kdugh2ni52e9eef3v303e8lnmit18vvh&secret_key=trtsf78i78rgqfdc4jrs0vsfmhvnbg2ipuluisk1&local_id=1234567&email=jcai@yiqixie.com&display_name=abc&profile_url=<encoded profile url>
成功返回示例：
{
"STATUS": "SUCCESS",
"user_id": "6832699324062886516",
"home_id": "fcAArpwGinCiNvdd0J8M_b8Ud"
}
参数说明：
参数
说明
STATUS
操作是否成功
user_id
用户在一起写的唯一标识
home_id
用户在一起写的目录id
出错返回示例：
{"ERRMSG":"incorrect api_key or secret_key","STATUS":"ERROR"}
{"ERRMSG":"user already created in YIQIXIE","STATUS":"ERROR"}

删除用户
路径：https://yiqixie.com/e/api/user/delete
参数说明：
参数
是否必须
说明
api_key
是
应用的唯一标识
secret_key
是
分配的唯一密钥
user_id
是
创建用户时返回获得的一起写的用户id
请求示例：
https://yiqixie.com/e/api/user/delete?api_key=k6rqo598kdugh2ni52e9eef3v303e8lnmit18vvh&secret_key=trtsf78i78rgqfdc4jrs0vsfmhvnbg2ipuluisk1&user_id=4469992750700262646
成功返回示例：
{"STATUS":"SUCCESS"}
出错返回示例：
{"ERRMSG":"incorrect api_key or secret_key","STATUS":"ERROR"}
{"ERRMSG":"INVALID USER","STATUS":"ERROR"}
{"ERRMSG":"user not existed in YIQIXIE","STATUS":"ERROR"}
获取用户列表
路径：https://yiqixie.com/e/api/user/list
参数说明：
参数
是否必须
说明
api_key
是
应用的唯一标识
secret_key
是
分配的唯一密钥
format
否
0为精简格式，仅返回user_id。
1为详细格式，返回每个用户的user_id，local_id以及用户状态。
默认为0。
注：用户状态目前仅分两种，1为普通用户，5为管理员。
请求示例：
https://yiqixie.com/e/api/user/list?api_key=k6rqo598kdugh2ni52e9eef3v303e8lnmit18vvh&secret_key=trtsf78i78rgqfdc4jrs0vsfmhvnbg2ipuluisk1&format=1
成功返回示例：
format=0：
{
  "STATUS": "SUCCESS",
  "USER_LIST": "[7189418288467811014, 2229093736705383188]"
}
format=1：
{
  "STATUS": "SUCCESS",
  "USER_LIST": "[{local_id=null, user_id=7189418288467811014, user_state=5, home_id=fcAAH3gmwhG9aso5cyFUGf1zp}, {local_id=1, user_id=2229093736705383188, user_state=1, home_id=fcACizkW7rm5I04PjvE4rtvtC}]"
}
出错返回示例：
{"STATUS":"ERROR","ERRMSG":"INVALID FORMAT"}
{"STATUS":"ERROR","ERRMSG":"MISSING PARAMETER"}
{"STATUS":"ERROR","ERRMSG":"INVALID USER"}
获取用户信息
路径：https://yiqixie.com/e/api/user/get
参数说明：
参数
是否必须
说明
api_key
是
应用的唯一标识
secret_key
是
分配的唯一密钥
local_id
是
第三方用户的唯一id
请求示例：
http://yiqixie.com/e/api/user/get?api_key=kjd0pm6q0v0p179bg1r16p3end9m00h4gha6cp8h&secret_key=c8pruime6tl06r5l2ffj7sbe9c8mpn03bkkm2882&local_id=1
成功返回示例：
{
  "STATUS": "SUCCESS",
  "user_id": "6832699324062886516",
  "home_id": "fcAArpwGinCiNvdd0J8M_b8Ud"
}
出错返回示例：
{"STATUS":"ERROR","ERRMSG":"INVALID FORMAT"}
{"STATUS": "ERROR","ERRMSG": "incorrect api_key or secret_key"}
{"STATUS": "ERROR", "ERRMSG": "User NOT Existing"}
更改用户信息
路径：https://yiqixie.com/e/api/user/update
参数说明：
参数
是否必须
说明
api_key
是
应用的唯一标识
secret_key
是
分配的唯一密钥
user_id
是
开发者创建用户返回获得的一起写的用户id
email
否
若包含，则为更新项
display_name
否
若包含，则为更新项
profile_url
否
若包含，则为更新项
请求示例：
https://yiqixie.com/e/api/user/update?api_key=k6rqo598kdugh2ni52e9eef3v303e8lnmit18vvh&secret_key=trtsf78i78rgqfdc4jrs0vsfmhvnbg2ipuluisk1&user_id=4469992750700262646&email=c@yiqixie.com
成功返回示例：
{"STATUS":"SUCCESS"}
出错返回示例：
{"ERRMSG":"incorrect api_key or secret_key","STATUS":"ERROR"}
{"ERRMSG":"INVALID USER","STATUS":"ERROR"}
{"ERRMSG":"user not existed in YIQIXIE","STATUS":"ERROR"}
Token API
获取refresh token(or long lived token)
路径：https://yiqixie.com/e/api/getrefreshtoken
参数说明： 
参数
是否必须
说明
api_key
是
应用的唯一标识
secret_key
是
分配的唯一密钥
user_id
是
开发者创建用户返回获得的一起写的用户id
注：请求成功返回long_token, long_token等效于oauth2协议中的refresh token，有效期可以视为无限长，开发者应当保存在自己的数据库里面，在任何时候都不应该把这个token传到前台逻辑。
请求示例：
https://yiqixie.com/e/api/getrefreshtoken?api_key=k6rqo598kdugh2ni52e9eef3v303e8lnmit18vvh&secret_key=trtsf78i78rgqfdc4jrs0vsfmhvnbg2ipuluisk1&user_id=4469992750700262646
成功返回示例：
{
  "STATUS": "SUCCESS",
  "long_token": "RTxsrrt_meWmtsV4O-bWQKNdPgOwDaMWO7M_oJEE_35JPxghGk6FHsJf8ExIjNcQFTuNl4A9Iyr8iB1gxT5qr2dlPlEtXQ_N-X7vvtfKu-6fGFFGaTw4TFykdWapJwQMQF_MmUXg8DG23XNYtaagnyKv7cixIKP68EM-AN6YlH12b-fa0Ax88yiPNoDzCDxRyGQyLqBoLb-A0UhBMMe3ow"
}


出错返回示例：
{"ERRMSG":"INVALID USER","STATUS":"ERROR"}
{"ERRMSG":"user already created in YIQIXIE","STATUS":"ERROR"}
获取oauth access token(or short lived token)
路径：https://yiqixie.com/e/api/refresh
参数说明：
参数
是否必须
说明
api_key
是
应用的唯一标识
secret_key
是
分配的唯一密钥
long_token
是
长期有效令牌
注：请求成功返回short_token, short lived token有效期为两个小时，开发者可以把该token嵌入到前端逻辑，或者放到用户可见的url里面，而不用担心泄露问题。
请求示例：
https://yiqixie.com/e/api/refresh?api_key=k6rqo598kdugh2ni52e9eef3v303e8lnmit18vvh&secret_key=trtsf78i78rgqfdc4jrs0vsfmhvnbg2ipuluisk1&long_token=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0erxkg0J0jRzVaO7omavIxwF3w2d3d33-crlGgWAs6YLy4VQ8nkeTOxWrbSlTXZqDAMFLrsrYOuZzAxRs2ZAwLgqm_TWJoAMYlbpC4WjHQjlxaVUI81JsHCIf_6-odLFYRRkeFohyJ82UeNNFKJKAj3g
成功返回示例：
{
  "STATUS": "SUCCESS",
  "short_token": "RTxsrrt_meWmtsV4O-bWQKNdPgOwDaMWO7M_oJEE_35JPxghGk6FHsJf8ExIjNcQerf4x0zong-5QInTNo2GX-vGFPqU5n5aP70ai5xu5V8n9e0BwnS29DPV2WwaKKZESO8V_gqy68f7yhtay2ZI-Bk-I035pS1jTWzDtomkG-fFDEfBquKIJHvAddABNX1oHcnbRHn6mt5ZFLQmjH4Slw"
}
错误返回示例：
{"ERRMSG":"TOKEN EXPIRE","STATUS":"ERROR"}
{"ERRMSG":"incorrect long_token","STATUS":"ERROR"}
{"ERRMSG":"user already created in YIQIXIE","STATUS":"ERROR"}
Document API
创建文档
路径：https://yiqixie.com/d/newapi?id=<user's home id>&initial_link_status=<1 or 2 or 3>&API-SESSION-TOKEN=<short lived token>
参数说明：
参数
是否必须
说明
id
是
创建用户返回的home_id
initial_title
否
初始文档名
initial_link_status
否
1 disable；2 readonly；3 readwrite
API-SESSION-TOKEN
是
获取oauth access token返回的short_token
请求示例：
https://yiqixie.com/d/newapi?id=fafjas34ujbnja23jjnb&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
成功返回示例：
{
  "key": "fcAA8ibD8kepx34eVWjLMhEH1",
  "cid": "fcAA8ibD8kepx34eVWjLMhEH1"
}

参数
说明
key
文档key
cid
文档创建者的用户id
错误返回示例：
{
  "STATUS": "INVALID_TOKEN",
  "ERRMSG": "INVALID_TOKEN"
}



创建表格
路径：https://yiqixie.com/s/newapi?id=<user's home id>&API-SESSION-TOKEN=<short lived token>
参数说明：
参数
是否必须
说明
id
是
创建用户返回的home_id
initial_title
否
初始表格名
initial_link_status
否
1 disable；2 readonly；3 readwrite
API-SESSION-TOKEN
是
获取oauth access token返回的short_token
请求示例：
https://yiqixie.com/s/newapi?id=fafjas34ujbnja23jjnb&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
成功返回示例：
{
  "key": "fcAB6iJAEKZdaLZaB5Ushheai",
  "cid": "fcAB6iJAEKZdaLZaB5Ushheai"
}

参数
说明
key
文档key
cid
表格创建者的用户id
创建演示
路径：https://yiqixie.com/p/newapi?id=<user's home id>&API-SESSION-TOKEN=<short lived token>
参数说明：
参数
是否必须
说明
id
是
创建用户返回的home_id
initial_title
否
初始演示名
initial_link_status
否
1 disable；2 readonly；3 readwrite
API-SESSION-TOKEN
是
获取oauth access token返回的short_token
请求示例：
https://yiqixie.com/p/newapi?id=fafjas34ujbnja23jjnb&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
成功返回示例：
{
  "key": "fcACF-2qnxiKoOVuoiXFEzpk4",
  "cid": "fcACF-2qnxiKoOVuoiXFEzpk4"
}

参数
说明
key
文档key
cid
演示创建者的用户id

创建文件夹
路径：https://yiqixie.com/d/newfolderapi/<key>?initial_link_status=<1 or 3>&folderName=<personal defined folder name>&API-SESSION-TOKEN=<short lived token>
参数说明：
参数
是否必须
说明
key
是
创建新文件夹所在的父文件夹id。若没有创建过文件夹，则为创建用户时返回的home_id
initial_link_status(integer)
否
1 disable；3 readwrite
folderName
否
用户可以创建时自定义文件夹名称
API-SESSION-TOKEN
是
获取oauth access token返回的short_token
请求示例：
https://yiqixie.com/d/newfolderapi/fafjas34ujbnja23jjnb?initial_link_status=1&folderName=apicreatefolder&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
成功返回示例：
{
  "FolderID": "fcAAdmq18FfYMtDGd5f8U--Wn"
}

参数
说明
FolderID
文件夹的id

更新文档/共享设置
路径：https://yiqixie.com/e/api/setmetadata/<key>，其中<key>为创建文档时返回的key。
参数说明：
注：下面的参数一次只能更新一个，不支持同时更改
参数
是否必须
说明
title(string)
否
设置后覆盖原来文档名
link_status(integer)
否
1:disable, 2:readonly, 3:readwrite
add_collaborators
否
文档新增协作者的user_id；可以批量提交user_id，之间用逗号（,）分隔。
delete_collaborators
否
文档删除协作者的user_id。可以批量提交user_id，之间用逗号（,）分隔。文档的创建者不可以被删除。
API-SESSION-TOKEN
是
获取oauth access token返回的short_token
请求示例：
https://yiqixie.com/e/api/setmetadata/fcABgtk86sqA1pgBH7FpWXHQ9?link_status=1&add_collaborators=6453970655730691257,3276686331386743911&delete_collaborators=7202220532224394872&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
成功返回示例：
{"STATUS":"SUCCESS"}
错误返回示例：
{"STATUS":"ERROR","ERRMSG":"MISSING PARAMETER"}
{"STATUS":"ERROR","ERRMSG":"INVALID LINKSTATUS"}
{"STATUS":"ERROR","ERRMSG":"INVALID USER ID: XXXXXXXXXX"}
{"STATUS":"ERROR","ERRMSG":"TRYING DELETING OWNER"}
获取文档属性
路径：https://yiqixie.com/e/api/getmetadata/<key>，其中<key>为创建文档时返回的key。
参数说明：
参数
是否必须
说明
attribute
是
link_status：文档链接的共享属性
collaborators：协作者列表
title：文档名称
all：以上全部
last_modified_time: 上次修改时间(返回毫秒)
API-SESSION-TOKEN
是
获取oauth access token返回的short_token
请求示例：
https://yiqixie.com/e/api/getmetadata/fcABgtk86sqA1pgBH7FpWXHQ9?attribute=title&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
成功返回示例：
{
"STATUS":"SUCCESS",
"ATTRIBUTE":"{COLLABORATORS=[{collaborator_id=1971067395383836682, role=OWNER}, {collaborator_id=2893885422173044447, role=COLLABORATOR}, {collaborator_id=690490035570182790, role=COLLABORATOR}], TITLE=公共文件夹, LINK_STATUS=2}"
}

参数
说明
COLLABORATORS
协作者列表
collaborator_id
协作者id
 role
角色：文档所有者(OWNER)，还是协作者
TITLE
文档名
LINK_STATUS
文档共享状态：1.关闭共享；2.只读权限 ；3.编辑权限 
错误返回示例：
{"STATUS":"ERROR","ERRMSG":"MISSING PARAMETER"}
{"STATUS":"ERROR","ERRMSG":"INVALID ATTRIBUTE"}

复制文档
请求方式：只支持post
路径：https://yiqixie.com/d/copy/<source doucument id>?pid=<container's id>&title=<initial title>&API-SESSION-TOKEN=<short lived token>
参数说明：
参数
是否必须
说明
source document id
是
被复制的文档id
container's id
是
必须是文件夹，复制出来的文档讲放在该文件夹下，调用者保证拥有读写权限
title
否
复制出来的文档名
API-SESSION-TOKEN
是
获取oauth access token返回的short_token
返回：成功复制文档返回副本的id：
{
  "id": "fcAB8MZSWGPJamAPKvIl81I7p"
}
复制表格
请求方式：只支持post
路径：https://yiqixie.com/s/copy/<source doucument id>?pid=<container's id>&title=<initial title>
参数说明：
参数
是否必须
说明
source document id
是
被复制的表格id
container's id
是
必须是文件夹，复制出来的文档讲放在该文件夹下，调用者保证拥有读写权限
title
否
复制出来的表格名
API-SESSION-TOKEN
是
获取oauth access token返回的short_token
返回：成功复制表格返回副本的id
{
  "id": "fcADlEyYWKZFZATb2Y4WIl6re"
}

IFRAMEING API
文档嵌入链接
构建规则：https://yiqixie.com/d/home/<key>?rt=embedded&API-SESSION-TOKEN=<short_token>
参数说明：
参数
是否必须
说明
key
是
创建文档时返回的文档key，作为url路径的一部分
API-SESSION-TOKEN
是
获取oauth access token返回的short_token，作为url请求参数
链接示例：
https://yiqixie.com/d/home/fcABgtk86sqA1pgBH7FpWXHQ9?rt=embedded&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
链接构建成功示例：


表格嵌入链接
构建规则：https://yiqixie.com/s/home/<key>?rt=embedded&API-SESSION-TOKEN=<short_token>
参数说明：
参数
是否必须
说明
key
是
创建文档时返回的文档key，作为url路径的一部分
API-SESSION-TOKEN
是
获取oauth access token返回的short_token，作为url请求参数
链接示例：
https://yiqixie.com/s/home/fcABgtk86sqA1pgBH7FpWXHQ9?rt=embedded&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
链接构建成功示例：


演示嵌入链接
构建规则：https://yiqixie.com/p/home/<key>?rt=embedded&API-SESSION-TOKEN=<short_token>
参数说明：
参数
是否必须
说明
key
是
创建文档时返回的文档key，作为url路径的一部分
API-SESSION-TOKEN
是
获取oauth access token返回的short_token，作为url请求参数
链接示例：
https://yiqixie.com/p/home/fcABgtk86sqA1pgBH7FpWXHQ9?rt=embedded&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
链接构建成功示例：

Doc/Docx Upload&Writeback API 
Converting a doc/docx document to yiqixie, edit them, and export to doc/docx format.

文档导入
路径：https://yiqixie.com/d/import/upload/<home_id>?format=docx&API-SESSION-TOKEN=<short lived token>
文件导入方式：
导入的文件在post的body中以form-data形式发送，发送的key:value分别为"Filedata"和待导入文件。
参数说明：
参数
是否必须
说明
home_id
是
用户的桌面id，创建用户时返回
format
是
文档导入格式，目前支持doc|docx
成功返回示例：
{
  "sessionStatus": {
	"state": "FINALIZED",
	"status": "SUCCESS",
	"additionalData": {
  	"docId": "fcACDn_JwIrEmHrUk5ZVxhg0B"
	}
  }
}
表格导入
路径：https://yiqixie.com/s/import/upload/<home_id>?format=xlsx&API-SESSION-TOKEN=<short lived token>
文件导入方式：
导入的文件在post的body中以form-data形式发送，发送的key:value分别为"Filedata"和待导入文件。
参数说明：
参数
是否必须
说明
home_id
是
用户的桌面id，创建用户时返回
format
是
表格导入格式，目前支持xlsx

成功返回示例：
{
  "sessionStatus": {
	"state": "FINALIZED",
	"status": "SUCCESS",
	"additionalData": {
  	"xlsxId": "fcACDn_JwIrEmHrUk5ZVxhg0B"
	}
  }
}
文档导出
路径：https://yiqixie.com/d/export/<key>?format=docx&API-SESSION-TOKEN=<short lived token>
参数说明：
参数
是否必须
说明
key
是
创建文档时返回的文档key，作为url路径的一部分
format
是
文档导出格式，目前支持docx|doc|pdf|html
API-SESSION-TOKEN
是
获取oauth access token返回的short_token，作为url请求参数

请求示例：
https://yiqixie.com/d/export/fcABgtk86sqA1pgBH7FpWXHQ9?format=html&API-SESSION-TOKEN=UUx0A1q93N11yOx8cBw_8_-HsKaC5DjXC1vP8j36GkMcRmttT74rS6PFljAHsK0eaiawThxZ6iwkuMn3heTheSfManUc00FKdYaQrITvPNCNeLtvE7TllkLdVfqNRGV0EolIIRqXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ
返回：成功返回相应格式文档。

表格导出
路径：https://yiqixie.com/s/export/<key>?format=xlsx&API-SESSION-TOKEN=<short lived token>
参数说明：
参数
是否必须
说明
key
是
创建表格时返回的key，作为url路径的一部分
format
是
文档导出格式，目前只支持xlsx
API-SESSION-TOKEN
是
获取oauth access token返回的short_token，作为url请求参数
请求示例：
https://yiqixie.com/s/export/fcABqKJVkNQRFwoTLNEBl50s6?format=html&API-SESSION-TOKEN=RTxsrrt_meWmtsV4O-bWQKNdPgOwDaMWO7M_oJEE_35JPxghGk6FHsJf8ExIjNcQ6pI0fKN0DpXR22R9xgH9devGFPqU5n5aP70ai5xu5V8n9e0BwnS29DPV2WwaKKZEqogw70MIud4GfZkEStQZ3ztkuHZS0GpPhjwrV0Wmg2f7Q7rObz6285IWgL_K1C6sxk8sjfsQ6vI_a7TOXqepkAXMIdPU9hZ30X9PMFU8W6Ri8yC7W3BmdAqIqd4xix6LVAhLf3kd25HLbjNeI9l0nqYiAj1zQrTzUGLRQ

返回：成功返回相应格式文档。

URL前缀的改动
/merlot --> /e
/vodka --> /d
/tequila --> /s
/show --> /p
