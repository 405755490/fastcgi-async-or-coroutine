## ����Ŀ��
�����Լ�����NGINX -> fastcgi -> ice����֮����ڵ�����ƿ����
## ѹ�ⷽ��
* �ҳ�nginx���ܼ���
* �ҳ�nginx + cgi���ܼ��ޡ��Ƚ�ͬ��cgi���첽cgi�Ĳ��졣
* �ҳ�nginx+cgi+ice���ܼ��ޡ��Ƚ�ͬ��cgi���첽cgi�Ĳ��졣

#### ����
�첽fastcgi��[Դ��](../mucgi "��ͣ��ʾ")  
ͬ��fastcgi��[Դ��](https://fastcgi-archives.github.io/ "��ͣ��ʾ")  

#### ѹ�ⷽ��
![չʾ](/doc/image/image001.png)  
 
##### ������״̬
    10��������ʵ���
    8��(Intel(R) Xeon(R) CPUE5504  @ 2.00GHz)
    ����1000Mbit
    Ӳ��7200ת
    �ڴ�32GB

## ѹ������
### 1.nginxѹ��
* �Ӵ�weighttp�������󣬿�����ƿ����CPU��
![չʾ](/doc/image/image002.png)  
![չʾ](/doc/image/image003.png)   

> Cpuʹ�ã�784
> �ﵽƽ����������96.5Ktps

### 2.NGINX->CGIѹ������
#### �����첽������CGI
* ʹ��nginxƿ��ʱ��weighttp������������nginx->cgi�첽ģ��ƿ��Ҳ��CPU��
![չʾ](/doc/image/image004.png)  
![չʾ](/doc/image/image005.png)   
    Cpuʹ�ã�770(370+400)
    �ﵽƽ����������71.3Ktps

#### ����ͬ������CGI
* ʹ��nginxƿ��ʱ��weighttp������������nginx->cgiͬ��ģ��ƿ������CPU��
![չʾ](/doc/image/image006.png)  
![չʾ](/doc/image/image007.png)  
    Cpuʹ�ã�672 (336+336)
    �ﵽƽ����������21.2Ktps

* ʹ��ͬ�Ȳ������Ӵ�ͬ��cgi���̸����ж�ƿ���Ƿ��ǵ���cgi�Ľ�����ƿ����
![չʾ](/doc/image/image008.png)  
![չʾ](/doc/image/image009.png)  
    Cpuʹ�ã�740 (353+390)
    �ﵽƽ����������27.2Ktps
>�������Ƶ���Ԥ�ڲ����ϡ� 

>nginx->cgiͬ��ģ��ƿ��������nginx��upstreamģ���cgi֮��ʹ�õ��Ƕ����ӣ���net.ipv4.tcp_tw_recycle = 0��ʱ��ѹ������з���time_wait״̬�Ķ˿ڴﵽ�ӽ���65536��������socket����Ԫ�飬��������ͨ������һ��fastcgi�����˿����Ż����ģ�͡�  
* ����һ��fastcgi�����˿���ѹ�⡣
![չʾ](/doc/image/image010.png)  
![չʾ](/doc/image/image011.png)  
![չʾ](/doc/image/image012.png)  
    Cpuʹ�ã�790
    �ﵽƽ����������28.2Ktps
__���Ż����Ӳ��Խ���Ͽ�����Դʹ�ÿ�����ȥ�ˣ���tps�����������ӡ�__

#### ѹ��NGINX ->CGI ->PROXY
##### �����첽������CGI
* ʹ��nginxƿ��ʱ��weighttp������������nginx->cgi->proxy�첽ģ��ƿ������Cpu��
![չʾ](/doc/image/image013.png)  
![չʾ](/doc/image/image014.png)  
    Cpuʹ�ã�550 (120+300+130)
    �ﵽƽ����������12Ktps
##### ����ͬ������CGI
![չʾ](/doc/image/image015.png)  
![չʾ](/doc/image/image016.png)  
    Cpuʹ�ã�670(360+190+120)
    �ﵽƽ����������10.8Ktps

### �Ż�NGINX +CGI +PROXYģ��
* NGINX +CGI + PROXYͬ��ģ�����ڶ��������ƻ���ɶԺ��proxy��ѹ�����㣬������ȫ���ӻ������ܡ�
* NGINX +CGI + PROXY�첽ģ���п��Ż��ռ䡣�����ƿ����ice�����̽����ʵ����ơ����Խ�nginx����������mcgi->����proxy�󡣻�����������ȫ���ӳ�����
![չʾ](/doc/image/image015.png)  
![չʾ](/doc/image/image016.png)  
    Cpuʹ�ã�788(177+418+193)
    �ﵽƽ����������19.6Ktps

## ����
![չʾ](/doc/image/image017.png)  

* ��̨���������浥��ѹ��nginx�ܵ��ﵽ96500tps.
* nginx->fastcgi����Դռ�ò�������£�`mucgi`ÿ�봦��71300��echo����,`libfcgi`ÿ�봦��21200��echo����.
* nginx->fastcgi->ice_proxy ��Դռ�ò�������£�`mucgi`ÿ�봦��10800��echo����,`libfcgi`ÿ�봦��19600��echo����.




