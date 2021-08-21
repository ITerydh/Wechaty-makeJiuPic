# [AI创造营]Wechaty实用小工具---九宫图爱心生成器~

## 背景

<center><font size="3" color="green">跟随抖音风~九宫图截图、截图、截图！</font></center>
<center><font size="2" color="red">手都截酸掉了吧！</font></center>
<center><font size="2" color="green">来吧~不需要你操作，我来！</font></center>
<center><font size="3" color="green">你只需要发送图片，结果自动生成</font></center>

## 效果图

![](https://ai-studio-static-online.cdn.bcebos.com/2c85a44692504fb9bb173ae9288aa375e1cf683f18bd485f9f2f8b7820f74bc4)

话不多说，肝着~

## 视频观赏

>视频地址：[https://www.bilibili.com/video/BV1Cf4y1P7Kc/](https://www.bilibili.com/video/BV1Cf4y1P7Kc/)

wechaty的安装不再讲解，请看上期：     
>[AI创造营]Wechaty实用小工具---证件照助手    
>[https://aistudio.baidu.com/aistudio/projectdetail/2253862](https://aistudio.baidu.com/aistudio/projectdetail/2253862)



## 第一步 环境准备

当你成功的运行起来docker，并通过二维码登录之后，Wechaty的环境就已经成功搭建了。

下面只需要导入部分库就可。


```python
import os
import asyncio
from wechaty import Wechaty, Message, FileBox

from PIL import Image
import time

os.environ['WECHATY_PUPPET_SERVICE_TOKEN'] = '换成你的token'
```

## 第二步 九宫图生成函数编写

左侧记得新建image和result文件夹



```python
def makeJiuPic(img_path):
    # 拿到图片路径，先把原图像重置大小
    img = Image.open(img_path)
    img = img.resize((304, 304), Image.ANTIALIAS)
    print("大小更改成功304")
    # 这张图也是最终的中心图，先进行存储
    img.save("result/5.png")
    # 再次拿到开始缩放为每张图的小图人物图100*100
    img = img.resize((100, 100), Image.ANTIALIAS)
    img = img.convert("RGBA")
    print("大小更改成功100")
    # 底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 底稿的粉红色小图100*100
    pink = Image.open("pink100x100.png")
    pink = pink.convert("RGBA")
    print("图片读取成功")
    # 准备好坐标值
    zuobiao = [(0,0),(102,0),(204,0),
               (0,102),(102,102),(204,102),
               (0,204),(102,204),(204,204)]

    print(zuobiao)

    # 初始化底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 生成第一张爱心图
    for i in range(9):
        if(i==0 or i==1 or i==2 or i==3 or i==4 or i==6):
            ground.paste(pink, zuobiao[i], mask=pink)
        else:
            ground.paste(img,zuobiao[i], mask=img)
    # 保存图片
    ground.save("result/1.png")

    # 初始化底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 生成第二张爱心图
    for i in range(9):
        if (i == 0 or i == 1 or i == 2 or i == 4 ):
            ground.paste(pink, zuobiao[i], mask=pink)
        else:
            ground.paste(img, zuobiao[i], mask=img)
    # 保存图片
    ground.save("result/2.png")

    # 初始化底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 生成第三张爱心图
    for i in range(9):
        if (i == 0 or i == 1 or i == 2 or i == 4 or i == 5 or i == 8):
            ground.paste(pink, zuobiao[i], mask=pink)
        else:
            ground.paste(img, zuobiao[i], mask=img)
    # 保存图片
    ground.save("result/3.png")

    # 初始化底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 生成第四张爱心图
    for i in range(9):
        if (i == 6):
            ground.paste(pink, zuobiao[i], mask=pink)
        else:
            ground.paste(img, zuobiao[i], mask=img)
    # 保存图片
    ground.save("result/4.png")

    # 初始化底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 生成第六张爱心图
    for i in range(9):
        if (i == 8):
            ground.paste(pink, zuobiao[i], mask=pink)
        else:
            ground.paste(img, zuobiao[i], mask=img)
    # 保存图片
    ground.save("result/6.png")

    # 初始化底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 生成第七张爱心图
    for i in range(9):
        if (i == 0 or i == 1 or i == 3 or i == 4 or i == 5 or i == 6 or i == 7 or i == 8):
            ground.paste(pink, zuobiao[i], mask=pink)
        else:
            ground.paste(img, zuobiao[i], mask=img)
    # 保存图片
    ground.save("result/7.png")

    # 初始化底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 生成第八张爱心图
    for i in range(9):
        if (i == 6 or i == 8):
            ground.paste(pink, zuobiao[i], mask=pink)
        else:
            ground.paste(img, zuobiao[i], mask=img)
    # 保存图片
    ground.save("result/8.png")

    # 初始化底稿的白底304x304
    ground = Image.open("white304x304.png")
    ground = ground.convert("RGBA")
    # 生成第九张爱心图
    for i in range(9):
        if (i == 1 or i == 2 or i == 3 or i == 4 or i == 5 or i == 6 or i == 7 or i == 8):
            ground.paste(pink, zuobiao[i], mask=pink)
        else:
            ground.paste(img, zuobiao[i], mask=img)
    # 保存图片
    ground.save("result/9.png")
```

## 第三步 主函数

项目要运行在本地环境

如果要在notebook中运行，需要更改asyncio


```python
class MyBot(Wechaty):
    async def on_message(self, msg: Message):
        talker = msg.talker()
        await talker.ready()
        if msg.type() == Message.Type.MESSAGE_TYPE_TEXT:
            if msg.text() == "ding":
                await talker.say('dong,发送一张图片获取九宫格爱心图片~')
            if msg.text() == "1":
                time.sleep(2)
                file_box = FileBox.from_file("result/1.png")
                await msg.say(file_box)
            if msg.text() == "2":
                time.sleep(2)
                file_box = FileBox.from_file("result/2.png")
                await msg.say(file_box)
            if msg.text() == "3":
                time.sleep(2)
                file_box = FileBox.from_file("result/3.png")
                await msg.say(file_box)
            if msg.text() == "4":
                time.sleep(2)
                file_box = FileBox.from_file("result/4.png")
                await msg.say(file_box)
            if msg.text() == "5":
                time.sleep(2)
                file_box = FileBox.from_file("result/5.png")
                await msg.say(file_box)
            if msg.text() == "6":
                time.sleep(2)
                file_box = FileBox.from_file("result/6.png")
                await msg.say(file_box)
            if msg.text() == "7":
                time.sleep(2)
                file_box = FileBox.from_file("result/7.png")
                await msg.say(file_box)
            if msg.text() == "8":
                time.sleep(2)
                file_box = FileBox.from_file("result/8.png")
                await msg.say(file_box)
            if msg.text() == "9":
                time.sleep(2)
                file_box = FileBox.from_file("result/9.png")
                await msg.say(file_box)


        elif msg.type() == Message.Type.MESSAGE_TYPE_IMAGE:
            await talker.say('已收到图片，生成图片ing...')
            # 将Message转换为FileBox
            img = await msg.to_file_box()
            # 获取图片名
            img_name = img.name
            # 图片保存的路径
            img_path = 'image/' + img_name
            # 将图片保存到本地文件
            await img.to_file(file_path=img_path)
            print("输入的图片路径：", img_path)
            makeJiuPic(img_path)
            # for pic in ["result/1.png", "result/2.png", "result/3.png","result/4.png", "result/5.png", "result/6.png","result/7.png", "result/8.png", "result/9.png"]:
            #     file_box = FileBox.from_file(pic)
            #     await msg.say(file_box)
            #     time.sleep(5)
            time.sleep(3)
            await talker.say("九张图片生成完毕!\n依次发送1-9获取九张图片")


async def main():
    bot = MyBot()
    await bot.start()


asyncio.run(main())
```

## 个人总结

>全网同名: iterhui

我在AI Studio上获得钻石等级，点亮10个徽章，来互关呀~

>[https://aistudio.baidu.com/aistudio/personalcenter/thirdview/643467](https://aistudio.baidu.com/aistudio/personalcenter/thirdview/643467)

