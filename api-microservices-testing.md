# 🌐 API & Microservices Testing

## 📌 Introduction

API and microservices testing ensures the reliability, functionality, and security of application programming interfaces. Unlike UI testing, API testing validates backend logic, data integrity, and communication between services. This guide covers:

- API testing strategies using **REST Assured, Postman, and SoapUI**
- **Contract testing and service virtualization**
- **Mocking and stubbing techniques** for effective API testing

---

## 🔹 API Testing Strategies

### ✅ Best Practices for API Testing

1. **Validate Response Codes** – Ensure correct HTTP status codes.
2. **Check Response Structure & Data** – Use JSON Schema validation.
3. **Test Edge Cases** – Handle invalid inputs, large payloads, etc.
4. **Verify Authentication & Authorization** – Test OAuth, API keys, JWT.
5. **Simulate Real-World Scenarios** – Ensure APIs work in different environments.

### 🛠 API Testing Tools & Frameworks

| Tool             | Features                                   |
| ---------------- | ------------------------------------------ |
| **Postman**      | GUI-based API testing, automated workflows |
| **REST Assured** | Java-based API testing framework           |
| **SoapUI**       | API testing for REST & SOAP services       |
| **Karate**       | BDD-style API testing with JSON support    |

### 🏗 Example: API Test Using REST Assured (Java)

```java
import io.restassured.RestAssured;
import io.restassured.response.Response;
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

public class APITest {
    public static void main(String[] args) {
        RestAssured.baseURI = "https://api.example.com";
        given().header("Authorization", "Bearer token")
            .when().get("/users")
            .then().statusCode(200)
            .body("size()", greaterThan(0));
    }
}
```

---

## 🔹 Contract Testing & Service Virtualization

Contract testing validates that APIs adhere to agreed specifications, preventing integration issues in microservices.

### ✅ Benefits of Contract Testing

- Detects breaking changes early.
- Ensures consumer-provider compatibility.
- Reduces dependency on real services.

### 🏗 Example: Contract Testing Using Pact (Node.js)

```javascript
const { Pact } = require("@pact-foundation/pact");

const provider = new Pact({
  consumer: "UserApp",
  provider: "UserService",
  port: 8081,
});

provider.setup().then(() => {
  provider.addInteraction({
    state: "User exists",
    uponReceiving: "a request for user data",
    withRequest: { method: "GET", path: "/users/1" },
    willRespondWith: { status: 200, body: { id: 1, name: "John Doe" } },
  });
});
```

### 🛠 Service Virtualization Tools

| Tool           | Features                       |
| -------------- | ------------------------------ |
| **WireMock**   | Mock API responses for testing |
| **Mountebank** | Simulate APIs and services     |
| **MockServer** | Create and test API mocks      |

---

## 🔹 Mocking & Stubbing Techniques for API Testing

Mocking and stubbing simulate API responses without relying on real services, improving test reliability and execution speed.

### ✅ When to Use Mocking & Stubbing

- **During Development** – APIs may not be fully implemented yet.
- **For Load Testing** – Simulate high request volumes.
- **To Isolate Components** – Test a service independently.

### 🏗 Example: Mocking API Responses in Postman

1. Go to **Postman > Mock Servers**.
2. Create a new mock server and define responses.
3. Use the mock URL in tests.

### 🏗 Example: Mocking API Using WireMock (Java)

```java
import static com.github.tomakehurst.wiremock.client.WireMock.*;

configureFor("localhost", 8080);
stubFor(get(urlEqualTo("/users/1"))
    .willReturn(aResponse()
        .withHeader("Content-Type", "application/json")
        .withBody("{ \"id\": 1, \"name\": \"John Doe\" }")));
```

### 🛠 Mocking & Stubbing Tools

| Tool           | Features                              |
| -------------- | ------------------------------------- |
| **WireMock**   | Stubs API responses for testing       |
| **Mountebank** | Multi-protocol service virtualization |
| **MockServer** | Create HTTP and HTTPS mocks           |

---

## 🎯 Conclusion

API and microservices testing is essential for ensuring robust and scalable applications. By leveraging **contract testing, service virtualization, and API mocking**, teams can create stable, efficient, and reliable test automation frameworks.

### 🔹 Key Takeaways:

✅ Use API testing frameworks like **REST Assured, Postman, and SoapUI**.
✅ Implement **contract testing** with **Pact** to validate API agreements.
✅ Utilize **service virtualization** to reduce dependency on live services.
✅ Leverage **mocking and stubbing** for fast, independent API testing.

By integrating these strategies, teams can build **resilient API test automation pipelines** that support scalable and high-performance applications. 🚀
