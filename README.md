# SimExp_Cracker

一个简洁的[科大奥锐](http://www.ustcori.com/Default.aspx)的虚拟仿真实验上传 / 解密的Python脚本

仅用于研究算法，任何个人不应该使用此脚本进行包括但不限于`篡改自己或他人成绩；对网站进行大量数据写入；对网站进行木马注入`等一切违规违法行为

任何因违反上述准则而产生的纠纷或经济利益损失，一切责任由使用者承担

**使用此脚本默认您已同意上面的内容**

## Installation

run the command below:

```sh
git clone https://github.com/Nova-Noir/SimExp_Cracker.git
cd SimExp_Cracker
```

# Usage

After Cloning, you should first edit `pwn.py`, change the value of `URL` at the `Line 15` to your own `SimExp_URL`

> Note: no '/' needed at the end of the URL

## Encrypt

`SimExp Cracker` can encrypt your own `*.xml` file into the API-recognizable`Content` using `Experiment.encrypt`.

It takes a byte-like value as its argument

```python
with open('path_to_the_xml_file.xml', 'rb') as f:
    c = f.read()
    content = Experiment.encrypt(c)
    print(content)
```

## Decrypt

`SimExp Cracker` can decrypt the `Content` using `Experiment.decrypt`

In order to get the `Content`, you need first capture the package posted to `/ServiceAPI/UpdateRecord`

To do so, while the Packet Capture Software is running, you could click `submit` button (recommended) or click `close` button and then find the data in your Packet Capture Software.

You can also get`UserID`、 `LabID`、`RecordID`、`FileName` and `LabName` in this package, which would be useful when you upload.

```python
encrypted_content = 'encrypted_content_here'
with open('path_to_decrypted_xml.xml', 'w') as f:
    f.write(Experiment.decrypt(encrypted_content))
```

## Upload

`SimExp Cracker` can upload the file to the server using `Experiment.upload`

```python
r = Experiment('UserID', LabID, 'LabName', RecordID, 'FileName')
c = Experiment.encrypt(content)
r.upload(c)
```

## Content
`SimExp Cracker` can get your experiments content using `Experiment.gen_content`

```python
with open('Content.html', 'w') as f:
        cookie = {
            "ASP.NET_SessionId": "%YOUR_COOKIE_HERE%"
        }
        # Method 1
        f.write(Experiment.get_content(r"Upload\\LabDate\\%LABNAME%\\%FILE_NAME%.xml",
                                       # make sure the url string has tag r, otherwise you gotta use "\\\\" instead.
                                       cookie))

        # Method 2
        r = Experiment('UserID', LabID, 'LabName', RecordID, 'FileName')
        f.write(r.gen_content(cookie))
```

# How it works?

I'll write a full blog on [my own blog](https://novanoir.moe/).

