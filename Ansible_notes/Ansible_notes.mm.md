# ansible 安装使用笔记

---

## 安装
```bash
# apt 安装方法
apt install ansible
# apt安装的默认配置文件位置
ansible 2.9.16
  配置文件位置：config file = /etc/ansible/ansible.cfg
  配置模块位置：configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python 模块位置： = /usr/lib/python3/dist-packages/ansible
  ansible 可执行程序位置： executable location = /usr/bin/ansible
```

## ansible 命令应用基础：
```bash
    语法：ansible <host-pattern> [-f forks] [-m module_name] [-a args]
    -f forks: 启动的并发线程数
    -m module_name: 要使用的模块
    -a args: 模块特有参数

    常见模块:
    command: 命令模块，默认模块，用于在远程执行命令：
        ansible all -a 'date'
    
    cron: 
        state:
            present: 安装
            absent: 移除
        # ansible web -m cron -a 'minute="*/10" job="/bin/echo hello " name="test cron job" state=absent'
    user:
        name=: 指明创建的用户名字
        # ansible web -m user -a 'name=mysql uid=306 system=yes group=mysql'
    group：
        group: 创建组
        # ansible web -m group -a ' name=mysql gid=306 system=yes'
    copy: 
        copy： 复制文件
                                src=源文件路径  dest=目标路径            owner=用户 mode=权限
        ansible all -m copy -a 'src=/etc/fstab dest=/tmp/fstab.ansible owner=root mode=640'
                                content=： 取代src=，表示直接用此处指定的信息生成为目标文件的内容：
        ansible all -m copy -a 'content="Hello Ansible\nHi MageEdu" dest=/tmp/test.ansible'
    file:
        file: 设定文件属性
                                                          mode=权限  path=指定文件路径，可以使用name或者dest来替换：
        # ansible all -m file -a 'owner=user1 group=user1 mode=644  path=/tmp/fstab.ansible'
        link:模式 创建连接文件
        # ansible all -m file -a 'path=/tmp/fstan.link src=/tmp/fstab.ansible state=link'
```
