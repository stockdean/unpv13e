> UNIX网络编程 卷1：套接字联网API（第3版）源代码

* 函数
    - [sock_ntop](lib/sock_ntop.c)
    - [signal](lib/signal.c)
    - [Fgets](https://github.com/arkingc/unpv13e/blob/master/lib/wrapstdio.c#L24)
    - [dg_echo](lib/dg_echo.c)（UDP回射服务器服务端）
    - 套接字读写
        + [readn](lib/readn.c)
        + [writen](lib/writen.c)
        + [readline](test/readline1.c)
        + [readline](lib/readline.c)\(改进版\)

* 程序
    * [测试主机字节序](intro/byteorder.c)
    * [检查套接字选项是否支持并获取默认值](sockopt/checkopts.c)

<table>
<tr>
    <td rowspan="10" align="center"> <b>TCP回射服务器</b> </td>
    <td rowspan="2" align="center"> v1 </td>
    <td align="center"> <a href = "tcpcliserv/tcpcli01.c">客户端</a> </td>
    <td align="center"> <a href = "lib/str_cli.c">str_cli函数</a>(阻塞于标准输入时无法处理来自服务器子进程的FIN分节) </td>
</tr>
<tr>
    <td align="center"> <a href = "tcpcliserv/tcpserv01.c">服务器</a>(多进程) </td>
    <td align="center"> <a href = "https://github.com/arkingc/unpv13e/blob/master/znote/TCP%E5%9B%9E%E5%B0%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E9%97%AE%E9%A2%98.md#1%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%AD%A3%E5%B8%B8%E7%BB%88%E6%AD%A2">服务器会产生僵尸子进程</a> </td>
</tr>
<tr>
    <td rowspan="1" align="center"> v2 </td>
    <td align="center"> <a href = "tcpcliserv/tcpserv02.c">服务器</a>(多进程) </td>
    <td align="center"> <a href = "https://github.com/arkingc/unpv13e/blob/master/znote/TCP%E5%9B%9E%E5%B0%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E9%97%AE%E9%A2%98.md#11-%E4%BD%BF%E7%94%A8wait%E7%89%88sig_chld%E5%87%BD%E6%95%B0%E5%A4%84%E7%90%86%E5%AD%90%E8%BF%9B%E7%A8%8Bsigchld%E4%BF%A1%E5%8F%B7">处理服务器僵尸子进程，会中断服务器系统调用</a> </td>
</tr>
<tr>
    <td rowspan="1" align="center"> v3 </td>
    <td align="center"> <a href = "tcpcliserv/tcpserv03.c">服务器</a>(多进程) </td>
    <td align="center"> 处理服务器被中断的系统调用，无法同时处理多个SIGCHLD信号 </td>
</tr>
<tr>
    <td rowspan="2" align="center"> v4 </td>
    <td align="center"> <a href = "tcpcliserv/tcpcli04.c">客户端</a> </td>
    <td align="center"> <a href = "https://github.com/arkingc/unpv13e/blob/master/znote/TCP%E5%9B%9E%E5%B0%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E9%97%AE%E9%A2%98.md#12-%E4%BD%BF%E7%94%A8waitpid%E7%89%88sig_chld%E5%87%BD%E6%95%B0%E5%A4%84%E7%90%86%E5%AD%90%E8%BF%9B%E7%A8%8Bsigchld%E4%BF%A1%E5%8F%B7">正常终止时引起服务器5个子进程终止</a> </td>
</tr>
<tr>
    <td align="center"> <a href = "tcpcliserv/tcpserv04.c">服务器</a>(多进程) </td>
    <td align="center"> <a href = "https://github.com/arkingc/unpv13e/blob/master/znote/TCP%E5%9B%9E%E5%B0%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E9%97%AE%E9%A2%98.md#12-%E4%BD%BF%E7%94%A8waitpid%E7%89%88sig_chld%E5%87%BD%E6%95%B0%E5%A4%84%E7%90%86%E5%AD%90%E8%BF%9B%E7%A8%8Bsigchld%E4%BF%A1%E5%8F%B7">同时处理多个SIGCHLD信号</a> </td>
</tr>
<tr>
    <td rowspan="3" align="center"> select </td>
    <td align="center"> <a href = "select/tcpcli01.c">客户端</a> </td>
    <td align="center"> <a href = "select/strcliselect01.c">str_cli函数</a>(解决v1版的问题，但无法处理重定向、无法处理I/O缓冲) </td>
</tr>
<tr>
    <td align="center"> <a href = "select/tcpcli02.c">客户端</a> </td>
    <td align="center"> <a href = "select/strcliselect02.c">str_cli函数</a>(解决前一版的问题) </td>
</tr>
<tr>
    <td align="center"> <a href = "https://github.com/arkingc/unpv13e/blob/master/znote/select.md#%E4%BB%A3%E7%A0%81">服务器</a>(单进程) </td>
    <td align="center"> 重写v4版服务器，使用单进程减少了多进程的开销 </td>
</tr>
<tr>
    <td rowspan="1" align="center"> poll </td>
    <td align="center"> <a href = "tcpcliserv/tcpservpoll01.c">服务器</a>(单进程) </td>
    <td align="center"> 重写v4版服务器，使用单进程减少了多进程的开销 </td>
</tr>

<tr>
    <td align="center"> <b>总结</b> </td>
    <td colspan="3" align="center"> <b>v1-v4：正确处理服务器终止的子进程</b> </td>
</tr>
</table>

<table>
<tr>
    <td rowspan="7" align="center"> <b>UDP回射服务器</b> </td>
    <td rowspan="2" align="center"> v1 </td>
    <td align="center"> <a href = "udpcliserv/udpcli01.c">客户端</a> </td>
    <td align="center"> <a href = "lib/dg_cli.c">dg_cli函数</a>(v1)<br>问题一：任何进程可向客户端发数据，会与服务器的回射数据报混杂<br>问题二：客户数据报或服务器应答丢失会使客户永久阻塞于recvfrom<br>
    <a href = "https://github.com/arkingc/unpv13e/blob/master/znote/UDP%E5%9B%9E%E5%B0%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E9%97%AE%E9%A2%98.md#2%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%BF%9B%E7%A8%8B%E6%9C%AA%E8%BF%90%E8%A1%8C">问题三：服务器未启动会使客户端阻塞于recvfrom</a></td>
</tr>
<tr>
    <td align="center"> <a href = "udpcliserv/udpserv01.c">服务器</a>(单进程) </td>
    <td align="center"> <a href = "lib/dg_echo.c">dg_echo函数</a> </td>
</tr>
<tr>
    <td rowspan="1" align="center"> v2 </td>
    <td align="center"> <a href = "udpcliserv/udpcli02.c">客户端</a> </td>
    <td align="center"> <a href = "udpcliserv/dgcliaddr.c">dg_cli函数</a>(v2)<br> <a href = "https://github.com/arkingc/unpv13e/blob/master/znote/UDP%E5%9B%9E%E5%B0%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E9%97%AE%E9%A2%98.md#11-%E9%AA%8C%E8%AF%81%E6%94%B6%E5%88%B0%E7%9A%84%E6%95%B0%E6%8D%AE">处理问题一，验证接收到的响应。但无法处理服务器多宿(多个IP)的情况</a> </td>
</tr>
<tr>
    <td rowspan="1" align="center"> v3 </td>
    <td align="center"> <a href = "udpcliserv/udpcli04.c">客户端</a>(connect版) </td>
    <td align="center"> <a href = "udpcliserv/dgcliconnect.c">dg_cli函数</a>(v3)<br> </td>
</tr>
<tr>
    <td rowspan="2" align="center"> v4 </td>
    <td align="center"> <a href = "udpcliserv/udpcli06.c">客户端</a> </td>
    <td align="center"> <a href = "udpcliserv/dgcliloop1.c">dg_cli函数</a>(v4)：写2000个1400字节的UDP数据报给服务器<br>问题：UDP缺乏流量控制，服务器接收速率慢时，缓冲区被发送端淹没<br></td>
</tr>
<tr>
    <td align="center"> <a href = "udpcliserv/udpserv06.c">服务器</a>(单进程) </td>
    <td align="center"> <a href = "udpcliserv/dgecholoop1.c">dg_echo函数</a> </td>
</tr>
<tr>
    <td rowspan="1" align="center"> v5 </td>
    <td align="center"> <a href = "udpcliserv/udpserv07.c">服务器</a>(单进程) </td>
    <td align="center"> <a href = "udpcliserv/dgecholoop2.c">dg_echo函数</a>(增大接收缓冲区的大小)</td>
</tr>
<tr>
    <td align="center"> <b>总结</b> </td>
    <td colspan="3" align="center"> <b>v1：问题二、三的根本原因是UDP数据传输不可靠</b><br><b>v4-v5：UDP缺乏流量控制，服务器接收的数据报数目不定，依赖诸多因素</b>  </td>
</tr>
</table>

<br>

宏值与头文件表：

|常量|值|所在头文件|
|:--:|:--:|:--:|
|SERV_PORT|9877|unp.h|
|MAXLINE|4096|unp.h|

<br>

**可以调用sigaction函数来检查或修改与指定信号相关联的处理动作。传入“信号处理函数”，只要有信号发生，信号处理函数就会被调用，这种行为称为“捕获信号”**

```c
/*
 *  参数：
 *      signo：要检测或修改其具体动作的信号编号
 *      act：非空，则要修改其动作
 *      oact：非空，则经由oact返回该信号的上一个动作
 */
int sigaction(int signo,const struct sigaction *restrict act,
            struct sigaction *restrict oact);

struct sigaction {
    void (*sa_handler)(int);    //信号处理函数的地址，或SIG_IGN、SIG_DFL
    //在调用信号处理函数之前，信号集要加到进程的信号屏蔽字中。
    //仅当从信号处理函数返回时再将进程的信号屏蔽字恢复为原先值。
    //这样，在调用信号处理函数时就能阻塞某些信号。在信号处理程序被调用时，
    //操作系统建立的新信号屏蔽字包括正被传递的信号。因此保证了在处理一个
    //给定的信号时，如果这种信号再次发生，那么它会被阻塞到对前一信号的处理
    //结束为止。如果一个信号在被阻塞期间产生了一次或多次，那么该信号被解
    //阻塞之后通常只递交一次，也就是说UNIX信号默认是不排队的
    sigset_t sa_mask;           //阻塞额外的信号
    int sa_flags;               //信号标志
    void (*sa_sigaction)(int,siginfo_t *,void *);
}

//信号处理函数，传入信号值
void handler(int signo);    //可以将信号值设为SIG_IGN来忽略它；设为SIG_DFL来启用默认处置
```

* **忽略信号**：将handler的参数设为SIG_IGN来忽略对某个信号的处置
* **启用信号的默认处置**：将handler的参数设为SIG_DFL来启动信号的默认处置
    - 默认处置通常是收到信号后终止进程
    - SIGCHLD和SIGURG(带外数据到达时发送)的默认处置是忽略信号

| 信号 | 描述 |
|:--:|:--:|
|SIGCHLD|子进程终止时给父进程发送的信号，如果父进程没有捕获代码，则这个信号被忽略|
|SIGTERM|关机时，init进程向系统中进程发出的信号，提示进程即将关机，进程可以捕获然后执行一些处理|
|SIGKILL(不能捕获)|杀掉进程|
|SIGSTOP(不能捕获)|停止进程|

| 信号标志 | 描述 |
|:--:|:--:|
|SA_RESTART|如果设置，由相应信号中断的系统调用将由内核自动重启（但是好像某些实现即使支持这个标志，也不一定会重启，所以不能过分依赖这个标志）|

<br>

Linux环境下开发经常会碰到很多错误(设置errno)，常见错误：

| 错误 | 描述 |
|:--:|:--:|
|EAGAIN|通常发生在非阻塞I/O中，如果数据未准备好，I/O操作会返回这个错误，提示再试一次|
|EINTR|表示系统调用被一个捕获的信号中断，发生该错误可以继续读写套接字|