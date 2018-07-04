# Building a very simple SOAP microservice in JAVA

I build the service on windows,
and demonstrate it from a simple C# console application
and all this in about 5 minutes.

## Video Tutorial
[![Building a very simple SOAP microservice in JAVA](https://img.youtube.com/vi/qcI6Gq6DhdU/0.jpg)](https://www.youtube.com/watch?v=qcI6Gq6DhdU)

[Building a very simple SOAP microservice in JAVA](https://www.youtube.com/watch?v=qcI6Gq6DhdU)

1. Create two folders using the cmd prompt 

```
mkdir SeansSimpleSOAP
mkdir build
```

2. Create text file in the SeansSimpleSOAP folder with the following code and name it **Hello.java**

```java
package SeansSimpleSOAP;

import javax.jws.WebService;

@WebService()
public class Hello {
  public void Hello() {}

  public String sayHello(String name) {
    System.out.println("new message from " + name);
    return "Hello " + name + ".";
  }
}
```

3. Create a second text file in the SeansSimpleSOAP folder with the following code and name it **Server.java**

```java
package SeansSimpleSOAP;
import javax.xml.ws.Endpoint;

public class Server {

    static String address = "http://127.0.0.1:8080/Service";
	
    protected Server() throws Exception {
        System.out.println("Starting Server");
        Object implementor = new Hello();
        Endpoint.publish(address, implementor);
    }

    public static void main(String args[]) throws Exception {
        new Server();
        System.out.println("Service listening at " + address);        
    }
}
```

4. build it,

`javac -d build SeansSimpleSOAP/*.java`

5. then finally run it. 

`java -cp build SeansSimpleSOAP.Server`

6. Browse the WSDL using your internet browser

`http://127.0.0.1:8080/Service?wsdl`



