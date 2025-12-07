## Receiving the Request
```java
import okhttp3.OkHttpClient;  
import okhttp3.Request;  
import okhttp3.Response;  
  
public class OkHttpTest {  
    public static void main(String[] args) throws Exception {  
        OkHttpClient client = new OkHttpClient();  
  
        Request request = new Request.Builder()  
                .url("https://api.github.com") // public API  
                .build();  
  
        try (Response response = client.newCall(request).execute()) {  
            System.out.println("Status: " + response.code());  
            System.out.println("Body:");  
            System.out.println(response.body().string());  
        }    
    }  
}
```

### Steps
```java
OkHttpClient client = new OkHttpClient();  
```
Creates an HTTP client object, which handles network connections.
```java
Request request = new Request.Builder()  
        .url("https://api.github.com") // public API  
        .build();  
```
Builds an HTTP **GET** request targeting the URL `https://api.github.com`.
```java
try (Response response = client.newCall(request).execute()) {  
```
Sends the HTTP request synchronously.
```java
System.out.println("Status: " + response.code());  
```
Prints the HTTP status code.
```java
System.out.println("Body:");  
System.out.println(response.body().string());  
```
Reads and prints the response body as a `String`.
## Sending the Request
