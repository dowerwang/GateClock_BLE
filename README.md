# GateClock_BLE

## 2018_3_3
    1.加入了【开门界面】【关门界面】【管理员模式界面锤子小图标】
    2.调整了旧 UI 的部分文字显示位置，让显示更加美观

# 2018_3_4
    1.重写了【管理员认证界面】，更加符合直觉
    2.修复了【Key_Cap】函数的显示bug
    3.unlock_interface 函数中的时间可以显示为动态的  这个功能先不加入


    【BUG1】：录入普通用户的时候，密码只能有6位，但是在开始界面输入密码的时候，竟然可以显示8位的密码。要去问老司机
    【Q1】：整个工程的密码只有6位，8位纯属虚晃别人，虚码功能需要使用这个信息，也就是真实的密码只有6位这个信息

# 2018_3_5
    1.修复了【验证失败】界面的显示位置，让显示居中，显得更加自然
    2.需要加入【密码虚码】功能，现在已经有了前半段虚码的功能，需要再加入后半段虚码的功能
    3.未来可能还需要加入【蓝牙】的功能，需要预留函数接口，也就是需要预留出有关用户指令的函数。例如：手机发到单片机0x00，单片机需要知道手机发出这个指令的意思，并且实时的做出反应。

# 2018_3_6
    1.还需要加入【历史记录功能】


    flash 存储
    本系统一共支持120个用户
    在原版工程中，所有的用户在flash中是同等对待的，管理员和普通用户没有分开。
    将管理员个普通用户分开能更好的管理，但是同样，在管理员用户不满的情况下，会浪费一点点的 flash 空间。

    【0x0800 C000】：开始存储用户结构体的地址为   【第49页】
    【0x0800 F800】：最后存储用户结构体的地址为   【第63页】
    上面两个地址的差值为【3800】，十进制为14336，14336/(63-49)=1024
    【0x0800 FC00】：保存所有用户的个数
    【0x0800 FC02】：保存管理员的个数
    【0x0800 FC04】：保存家人用户的个数
    【0x0800 FC06】：保存保姆用户的个数
    【0x0800 FC08】：音频 flag
    【0x0800 FD00】：
    【0x0800 FC10】：存放关键字【0xAA55】，每次用户重置，则重置这个关键字，用于标识是否是第一次使用


    【0x0800 FD04】：我想把开锁记录存储在这个位置。这个还得问一下老司机，检查一下是不是可行。
    用户编号在一个用户数据样本中的第三个【XX】，可以直接调用flash中的每个用户的第34个数据就是那个用户的 ID 了。
    然后有了用户的 ID ，当然还需要那个用户开门时候的时间，所以还需要把当时的时间数据写入到 flash 里面，时间所占多少字节需要清楚。
    【写ID方案】：ID 一共有两个字节。可以这么写 Test_Write(UNLOCK_NOTES_ADDR, my_user1.number);
    【写日期方案】：日期一共8个字节。可以这么写：
        u16 hourmin = calendar.hour
        Test_Write(UNLOCK_NOTES_ADDR, my_user1.number);

# 2018_3_12  Ok return... success>>>
    1.需要加入历史记录功能，写日期c以及就加入 ID 的功能已经能够实现，现在需要写成函数。
    2.今天下午有课，今天一整天就写这一个函数了。

# 2018_3_13
    1.给指纹开锁写了 历史记录 计入的功能

# 2018_3_14
    1.【历史记录】功能彻底完工
    2.需要修补密码阴码功能
    3.虚码完全体诞生！

# 2018_3_20
    1.加入【保姆时段】功能
    2.需要修改【声音】功能

# 2018_3_22
    1.添加了声音库

# 2018_3_23
    1.今天去问老司机，蓝牙的东西能不能焊上就能用，最好今天把蓝牙给调通
    2.已经把所有声音都挑选好
    蓝牙通信部分先把【信息录入】【信息删除】做好就行，详细的就是通过蓝牙发送数据

# 2018_3_27
    1.今天需要把数据包的格式以及内容都过一遍，然后写一个按键控制发送数据包的程序，发送的数据包先选择【录入射频卡】这个功能

# 2018_3_28
    1.发送包头部分完工。需要加入发送数据包功能，发送数据包之前可能还需要进行编码

# 2018_3_29
    1.今天需要写三位用户编号进行ascii转码程序（已完成）

# 2018_3_30
    1.今天需要写BLE收发，射频卡采集（已完成）

# 2018_3_31
    1.今天需要写射频卡的录入功能（已完成射频卡录入功能）

# 2018_4_1
    1.今天需要写射频卡的删除功能（已完成射频卡删除功能）

# 2018_4_2
    1.今天需要写指纹头的检测功能，能够检测到指纹头就可以（已完成指纹的录入和删除，超额完成任务）

# 2018_4_3
    1.今天需写密码录入功能（已完成）（超额完成密码删除功能）

# 2018_4_4
    1.今天了解一下指纹头的内部细节，方便之后的调试以及Debug，顺带相当于休息一下。
    写完了指纹解锁和射频卡解锁，超额完任务！！！

# 2018_4_7
    1.已完成密码解锁功能。
    2.还差界面显示，时间段密码解锁，低功耗没有写。

# 2018_4_9
    1.已经完成了低功耗部分，今天把密码输入界面人性化就行了。（界面优化已完成）

# 2018_4_14
    1.今天把密码加密整合进去
