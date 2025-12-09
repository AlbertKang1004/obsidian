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
```java
import okhttp3.*;

public class OkHttpPostExample {
    public static void main(String[] args) throws Exception {
        OkHttpClient client = new OkHttpClient();

        MediaType JSON = MediaType.parse("application/json; charset=utf-8");

        String json = """
            {
              "username": "albert",
              "score": 10
            }
            """;

        RequestBody body = RequestBody.create(json, JSON);

        Request request = new Request.Builder()
                .url("https://example.com/api")
                .post(body)
                .build();

        try (Response response = client.newCall(request).execute()) {
            System.out.println("Status: " + response.code());
            System.out.println(response.body().string());
        }
    }
}
```
### Step
```java
MediaType JSON = MediaType.parse("application/json; charset=utf-8");
```
Defines the content type of the data you will send
```java
String json = """
{
  "username": "albert",
  "score": 10
}
""";
```
Creates a **JSON string payload**.
```java
RequestBody body = RequestBody.create(json, JSON);
```
Wraps the JSON string into a `RequestBody` so it can be sent.
```java
Request request = new Request.Builder()
        .url("https://example.com/api")
        .post(body)
        .build();
```
Builds a POST request to the given URL and attaches the JSON body.