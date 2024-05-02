# visusal vm을 centOs에서 실행하는 방법

## 1.	visualvm 설치한 후 bin 안에 있는 exe 파일을 실행한다.

https://visualvm.github.io/download.html

```
위 사이트에서 os 에 맞는 visualvm을 다운 받은 후
아래 파일을 실행한다.
```
![image](https://github.com/auspicious0/init_visualvm/assets/108572025/3975af16-5055-4859-bd05-f3f22a4874a8)


2.	아래 자바 코드를 vi 편집기를 통해 작성한다.
 ![image](https://github.com/auspicious0/init_visualvm/assets/108572025/71388466-8cec-4f6d-b9a8-139fe18e512f)
```
public class MonitorDemo {
    public static void main(String[] args) {
        while (true) {
            System.out.println("Monitoring...");
            try {
                Thread.sleep(1000); // 1초마다 모니터링
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```
3.	아래와 같이 실행한다.

```
javac MonitorDemo.java

jar cfe MonitorDemo.jar MonitorDemo MonitorDemo.class

java -Dcom.sun.management.jmxremote=true\     
-Dcom.sun.management.jmxremote.local.only=false\
-Dcom.sun.management.jmxremote.port=1099\
-Dcom.sun.management.jmxremote.ssl=false\      
-Dcom.sun.management.jmxremote.authenticate=false\
-Djava.rmi.server.hostname=192.168.1.93\     
-Dcom.sun.management.jmxremote.rmi.port=1099\      
-jar MonitorDemo.jar
 ```
![image](https://github.com/auspicious0/init_visualvm/assets/108572025/f243459f-214e-4284-ad60-dcf3f3f79696)

4.	실행한 visualvm 파일에서 연결한다.

```
"File" 메뉴에서 "Add JMX Connection"을 선택합니다.
연결할 호스트와 포트를 입력합니다. 위의 코드에서는 1099 포트에서 JMX 연결을 허용합니다.
연결이 성공하면 프로세스 목록에 Java 프로그램이 표시됩니다. 해당 프로그램을 선택하여 세부 정보를 확인할 수 있습니다.
```
![image](https://github.com/auspicious0/init_visualvm/assets/108572025/8c3effd9-d8bd-45ab-8cd4-369837d74c7a)

