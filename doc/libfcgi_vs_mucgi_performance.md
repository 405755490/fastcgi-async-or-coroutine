## ����Ŀ��
�����Լ�����NGINX -> fastcgi -> ice����֮����ڵ�����ƿ����
## ѹ�ⷽ��
* �ҳ�nginx���ܼ���
* �ҳ�nginx -> fastcgi���ܼ��ޡ��Ƚ�ͬ��cgi���첽cgi�Ĳ��졣
* �ҳ�nginx -> fastcgi -> ice���ܼ��ޡ��Ƚ�ͬ��cgi���첽cgi�Ĳ��졣

#### ����
�첽fastcgi��[Դ��](../mucgi "��ͣ��ʾ")  
ͬ��fastcgi��[Դ��](https://fastcgi-archives.github.io/ "��ͣ��ʾ")  

#### ѹ�ⷽ��
![չʾ](/doc/image/image001.png)  
 
#### ������״̬
    10��������ʵ���
    8��(Intel(R) Xeon(R) CPUE5504  @ 2.00GHz)
    ����1000Mbit
    Ӳ��7200ת
    �ڴ�32GB

## ѹ������
### 1. nginxѹ��
![չʾ](/doc/image/image002.png)  
![չʾ](/doc/image/image003.png)   
    CPUʹ�ã�784  
    �ﵽƽ����������96.5Ktps  
> CPU��Դ������꣬����nginx����ƿ����CPU
---
### 2. NGINX->CGIѹ������
#### a. �����첽fastcgi
![չʾ](/doc/image/image004.png)  
![չʾ](/doc/image/image005.png)  
    CPUʹ�ã�770(370+400)  
    �ﵽƽ����������71.3Ktps  
> CPU��Դ������꣬����nginx->cgi�첽ģ��ƿ��Ҳ��CPU
#### b. ����ͬ��fastcgi
* i.ʹ��nginxƿ��ʱ��weighttp������
![չʾ](/doc/image/image006.png)  
![չʾ](/doc/image/image007.png)  
    CPUʹ�ã�672 (336+336)  
    �ﵽƽ����������21.2Ktps  
> CPU��Դ��ʣ��,����ƿ������CPU
* ii.�Ӵ󲢷���
![չʾ](/doc/image/image008.png)  
![չʾ](/doc/image/image009.png)  
    CPUʹ�ã�740 (353+390)  
    �ﵽƽ����������27.2Ktps  
> �Ӵ󲢷���������������ߵ���Ԥ�ڲ����ϡ� 

>nginx->cgiͬ��ģ��ƿ��������nginx��upstreamģ���cgi֮��ʹ�õ��Ƕ����ӣ���net.ipv4.tcp_tw_recycle = 0��ʱ��ѹ������з���time_wait״̬�Ķ˿ڴﵽ�ӽ���65536��������socket����Ԫ�飬��������ͨ������һ��fastcgi�����˿����Ż����ģ�͡�  
* iii.����һ��fastcgi�����˿�
![չʾ](/doc/image/image010.png)  
![չʾ](/doc/image/image011.png)  
![չʾ](/doc/image/image012.png)  
    CPUʹ�ã�790  
    �ﵽƽ����������28.8Ktps  
> ����һ��fastcgi�����˿���ѹ�⣬�Ӳ��Խ���Ͽ�����Դʹ�ÿ�����ȥ�ˣ���tps�����������ӡ�
---
### 3. NGINX->CGI->PROXYѹ������
* a. �����첽CGI  
![չʾ](/doc/image/image013.png)  
![չʾ](/doc/image/image014.png)  
    CPUʹ�ã�550 (120+300+130)  
    �ﵽƽ����������12Ktps  
>  CPU��Դ��ʣ��,����ƿ������CPU
* b. ����ͬ��CGI  
![չʾ](/doc/image/image015.png)  
![չʾ](/doc/image/image016.png)  
    CPUʹ�ã�670(360+190+120)  
    �ﵽƽ����������10.8Ktps  
>  CPU��Դ��ʣ��,����ƿ������CPU
---
### 4.�Ż�NGINX +CGI +PROXYģ��
__NGINX + MUCGI + PROXY�첽ģ���п��Ż��ռ䡣�����ƿ����ice�����̽����ʵ����ơ����Խ�nginx����������mcgi->����proxy�󡣻�����������ȫ���ӳ�����__
  
![չʾ](/doc/image/image017.png)  
![չʾ](/doc/image/image018.png)  
    CPUʹ�ã�788(177+418+193)  
    �ﵽƽ����������19.6Ktps  
> CPU��Դ������꣬����ƿ��Ҳ��CPU.
## ����  
* ��̨���������浥��ѹ��nginx�ܵ��ﵽ96500tps.  
* nginx->fastcgi����Դռ�ò�������£�`mucgi`ÿ�봦��71300��echo����,`libfcgi`ÿ�봦��21200��echo����.  
* nginx->fastcgi->ice_proxy ��Դռ�ò�������£�`mucgi`ÿ�봦��10800��echo����,`libfcgi`ÿ�봦��19600��echo����.  

![չʾ](/doc/image/image019.png)  



