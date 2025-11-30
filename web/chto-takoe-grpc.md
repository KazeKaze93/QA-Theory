# Что такое gRPC?

**gRPC** — это современный фреймворк удалённого вызова процедур (Remote Procedure Call, RPC), разработанный Google. Он позволяет сервисам обмениваться данными быстро и эффективно, особенно в распределённых системах и микросервисной архитектуре.

***

### Основные особенности gRPC

1. **Использует HTTP/2**
   * Поддержка мультиплексирования (несколько запросов по одному соединению).
   * Потоковая передача данных (server streaming, client streaming, bidirectional streaming).
   * Сжатие заголовков.
2. **Формат сообщений — Protocol Buffers (Protobuf)**
   * Более компактный и быстрый по сравнению с JSON и XML.
   * Строго типизированный контракт между клиентом и сервером.
3. **Кросс-языковая поддержка**
   * gRPC имеет генераторы кода для многих языков: Python, Java, Go, C#, C++, Node.js и др.
4. **Типы взаимодействия**
   * **Unary** — обычный запрос-ответ (как HTTP).
   * **Server streaming** — один запрос, много ответов.
   * **Client streaming** — много запросов, один ответ.
   * **Bidirectional streaming** — оба потока могут обмениваться сообщениями параллельно.

***

### Преимущества

* Высокая производительность (Protobuf + HTTP/2).
* Строгие контракты (минимум ошибок в формате данных).
* Поддержка стриминга.
* Хорошо подходит для микросервисов.

***

### Недостатки

* Менее удобен для работы в браузере (по сравнению с REST, нужен gRPC-Web).
* Сложнее отлаживать (сообщения в Protobuf не читаемые человеком без декодирования).
* Требует строгого описания схемы (IDL-файлы `.proto`).

***

### Для QA важно

* Проверка соответствия сообщений контракту (`.proto`).
* Тестирование разных типов вызовов (unary, streaming).
* Проверка обработки ошибок и кодов состояния (gRPC использует свои статус-коды, отличные от HTTP).
* Нагрузочное тестирование (особенно при стриминге).



В **gRPC** запросы описываются в виде контрактов на языке **Protocol Buffers (Protobuf)**, а затем на их основе генерируется код для клиента и сервера.

***

### Пример `.proto` файла

```proto
syntax = "proto3";

service UserService {
  // Обычный запрос (unary)
  rpc GetUser (UserRequest) returns (UserResponse);

  // Поток от сервера (server streaming)
  rpc ListUsers (Empty) returns (stream UserResponse);

  // Поток от клиента (client streaming)
  rpc UploadUsers (stream UserRequest) returns (UploadStatus);

  // Двунаправленный поток (bidirectional streaming)
  rpc Chat (stream ChatMessage) returns (stream ChatMessage);
}

// Сообщения
message UserRequest {
  int32 id = 1;
}

message UserResponse {
  int32 id = 1;
  string name = 2;
  string email = 3;
}

message UploadStatus {
  bool success = 1;
}

message ChatMessage {
  string user = 1;
  string text = 2;
}

message Empty {}
```

***

### Виды запросов

1.  **Unary (один запрос — один ответ)**\
    Клиент:

    ```python
    response = stub.GetUser(UserRequest(id=1))
    print(response.name, response.email)
    ```
2.  **Server streaming (один запрос — много ответов)**\
    Клиент:

    ```python
    for user in stub.ListUsers(Empty()):
        print(user.name)
    ```
3.  **Client streaming (много запросов — один ответ)**\
    Клиент:

    ```python
    def request_generator():
        yield UserRequest(id=1)
        yield UserRequest(id=2)
        yield UserRequest(id=3)

    response = stub.UploadUsers(request_generator())
    print(response.success)
    ```
4.  **Bidirectional streaming (обмен сообщениями в обе стороны)**\
    Клиент:

    ```python
    def chat_generator():
        yield ChatMessage(user="Alice", text="Привет")
        yield ChatMessage(user="Bob", text="Как дела?")

    for message in stub.Chat(chat_generator()):
        print(f"{message.user}: {message.text}")
    ```

***

Таким образом, gRPC поддерживает не только стандартную схему «запрос–ответ», но и полноценный **стриминг в обе стороны**, что делает его мощным инструментом для real-time приложений.
