# HTTP Lesson

## Introduction to HTTP

HTTP (HyperText Transfer Protocol) is a data transfer protocol used on the Internet, facilitating communication between clients and servers. It serves as the foundation for web data exchange, enabling users to access web pages, images, files, and other Internet resources.

## HTTP Methods

HTTP defines a set of request methods indicating the desired action for a resource. Below are examples of the most commonly used methods in both Python and Java.

### 1. GET

Used to request the content of a specified resource. The GET method is commonly used to retrieve data from a server.

**Python**

```python
import requests

response = requests.get('http://example.com')
print(response.text)
```

**Java**

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("http://example.com"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.body());
    }
}
```

### 2. POST

Used to send data for processing to a specified resource. The POST method is often used for submitting forms.

**Python**

```python
import requests

url = 'http://example.com'
myobj = {'key': 'value'}

x = requests.post(url, data=myobj)
print(x.text)
```

**Java**

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.http.HttpRequest.BodyPublishers;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("http://example.com"))
                .POST(BodyPublishers.ofString("key=value"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.body());
    }
}
```

### 3. PUT

Replaces all current representations of the target resource with the request data.

**Python**

```python
import requests

url = 'http://example.com/resource'
myobj = {'somekey': 'somevalue'}

x = requests.put(url, data=myobj)
print(x.text)
```

**Java**

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.http.HttpRequest.BodyPublishers;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("http://example.com/resource"))
                .PUT(BodyPublishers.ofString("somekey=somevalue"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.body());
    }
}
```

### 4. DELETE

Removes the specified resource.

**Python**

```python
import requests

url = 'http://example.com/delete'

response = requests.delete(url)
print(response.text)
```

**Java**

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("http://example.com/delete"))
                .DELETE()
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.statusCode());
    }
}
```

## HTTP Headers

HTTP headers allow the client and server to pass additional information with an HTTP request or response. Headers can include data about the content type, encoding, authentication, and more.

### Examples of Working with Headers:

**Python**

```python
import requests

url = 'http://example.com'

headers = {
    'User-Agent': 'My User Agent 1.0',
    'Accept': 'application/json'
}

response = requests.get(url, headers=headers)
print(response.text)
```

**Java**

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("http://example.com"))
                .header("User-Agent", "My User Agent 1.0")
                .header("Accept", "application/json")
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.body());
    }
}
```

## Basic Authentication

Basic Authentication is a method for an HTTP user agent to provide a user name and password when making a request.

### Examples:

**Python**

```python
import requests
from requests.auth import HTTPBasicAuth

response = requests.get('http://example.com', auth=HTTPBasicAuth('user', 'pass'))
print(response.text)
```

**Java**

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.Base64;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        String encoding = Base64.getEncoder().encodeToString(("user:pass").getBytes());
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("http://example.com"))
                .header("Authorization", "Basic " + encoding)
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.body());
    }
}
```

## Multipart Requests

Multipart requests are used to send files or data in multiple parts.

### Examples:

**Python** (using `requests` library)

```python
import requests
from requests_toolbelt.multipart.encoder import MultipartEncoder

multipart_data = MultipartEncoder(
    fields={'field0': 'value', 'field1': ('filename', open('file.txt', 'rb'), 'text/plain')}
)

response = requests.post('http://example.com/upload', data=multipart_data,
                         headers={'Content-Type': multipart_data.content_type})

print(response.text)
```

**Java** (using `java.net.http`)

Java's native HTTP client does not directly support multipart/form-data. You would typically use a third-party library like Apache HttpClient to construct