# paper_auto_backup
论文自动备份软件

# 在软件安装前需要安装 win10toast

```shell
pip3 install win10toast
```

# 代码内容

```python
import time
import os
import shutil
from win10toast import ToastNotifier

message = ToastNotifier()

## 软件启动时，立即进行一次备份
shutil.copy("main.md",".\\PaperAutoBackup\\{}.md".format(time.strftime("%Y-%m-%d-%H-%M-%S",time.localtime())))
os.remove("main-LastBackup.md")
shutil.copy("main.md","main-LastBackup.md")

## 打开论文软件
os.system("start main.md")

print("程序启动完成！")

while True:
    
    ## 倒计时部分

    # 倒计时 5 分钟后第一次提示
    time.sleep(10)
    message.show_toast("论文自动备份程序",
                   "10秒后自动备份，请及时按ctrl+S备份程序",
                   duration=4)
    time.sleep(10)
    shutil.copy("main.md",".\\PaperAutoBackup\\{}.md".format(time.strftime("%Y-%m-%d-%H-%M-%S",time.localtime())))
    os.remove("main-LastBackup.md")
    shutil.copy("main.md","main-LastBackup.md")
    message.show_toast("论文自动备份程序",
                   "备份完成，备份时间{}".format(time.strftime("%Y-%m-%d-%H-%M-%S",time.localtime())),
                   duration=4)
    print("论文备份完成，备份时间{}".format(str(time.time())))

```
