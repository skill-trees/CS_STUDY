# 자바 직렬화(Serialization)

변수들은 각자 메모리 주소공간을 가진다. 변수가 모든 컴퓨터에서 동일한 주소값을 가지는것은 아니다. 왜냐면 걱 OS 마다 가상 메모리 주소 공간이 다르기 때문이다. 따라서, 다른 OS에서도 변수에 동일하게 접근하고 싶을 때 주소값이 아닌 Byte 형태의 직렬화 된 객체를 만들어야한다.

- 자바 직렬화란 자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 데이터 변환하는 기술과 바이트로 변환된 데이터를 다시 객체로 변환하는 기술(역직렬화)을 아울러서 말합니다.
- 시스템 적으로는 JVM(Java Virtual Machine)의 메모리에 상주(heap 또는 stack) 되어 있는 객체 데이터를 바이트 형태로 변환하는 기술과 직렬화된 바이트 형태의 데이터를 객체로 변환해서 JVM으로 상주시키는 형태를 말합니다.

## 직렬화 방법

자바 직렬화를 하기 위해서 type이 primitive type(기본형 타입)이거나 java.io.Serializable 인터페이스를 상속 받아야 합니다.

```java
@Entity
@AllArgsConstructor
@toString
public class Post implements Serializable {
private static final long serialVersionUID = 1L;
    
private String title;
private String content;
```

`serialVersionUID`를 만들어준다.

```java
Post post = new Post("제목", "내용");
byte[] serializedPost;
try (ByteArrayOutputStream baos = new ByteArrayOutputStream()) {
    try (ObjectOutputStream oos = new ObjectOutputStream(baos)) {
        oos.writeObject(post);

        serializedPost = baos.toByteArray();
    }
}
```

`ObjectOutputStream`으로 직렬화를 진행한다. Byte로 변환된 값을 저장하면 된다.

### **역직렬화 예시**

```java
try (ByteArrayInputStream bais = new ByteArrayInputStream(serializedPost)) {
    try (ObjectInputStream ois = new ObjectInputStream(bais)) {

        Object objectPost = ois.readObject();
        Post post = (Post) objectPost;
    }
}
```

`ObjectInputStream`로 역직렬화를 진행한다. Byte의 값을 다시 객체로 저장하는 과정이다.

### 주의해야 할 사항

1. 구조 변경

위의 코드에서 `serialVersionUID`를 직접 설정했었다. 사실 선언하지 않아도, 자동으로 해시값이 할당된다.

직접 설정한 이유는 기존의 클래스 멤버 변수가 변경되면 `serialVersionUID`가 달라지는데, 역직렬화 시 달라진 넘버로 Exception이 발생될 수 있다.

따라서 직접 `serialVersionUID`을 관리해야 클래스의 변수가 변경되어도 직렬화에 문제가 발생하지 않게 된다.

→ 위와 같은 특성 때문에 자바 직렬화를 자주 변경되는 클래스의 객체에 사용하는 것을 지양해야합니다.

1. 용량

자바 직렬화 시에는 기본적으로 타입에 대한 정보 등 클래스에 대한 메타정보가 포함되어 있기 때문에 상대적으로 다른 포맷(JSON, CSV)에 비해 용량이 큽니다.

## 직렬화 상황

### 서블릿 세션(Servlet Session)

서블릿 기반의 WAS(톰캣, 웹로직) 들은 대부분 세션의 자바 직렬화를 지원하고 있습니다. 단순히 메모리 위에서 운용하는 세션이 아닌(서버 재시작 시 초기화) 클러스터링 환경에서 세션 공유를 위해 파일로 저장하거나 DB에 저장할 때 세션 객체를 자바 직렬화를 사용하여 저장할 수 있습니다.

### 캐시(Cache)

실시간으로 반복적으로 DB에서 조회하는 데이터가 아니라면, 리소스 절약을 위해 주로 캐시(메모리 DB) 라이브러리 시스템(Ehcache, Redis ...) 에 데이터를 저장해 놓고 사용하게 되는데, 이 때 데이터를 자바 직렬화하여 저장할 수 있습니다.

### 자바 RMI(Remote Method Invocation)

사실 자바 직렬화는 자바 RMI에서 많이 사용했다고 합니다. (지금은 잘 사용하지 않는..)

RMI(Remote Method Invocation)은 쉽게 말하면 원격 시스템(외부 시스템)에서 원격에 있는 시스템 메서드를 로컬 시스템의 메서드인 것처럼 호출하는 것을 말하는데, 메서드의 파라미터로 객체를 전달할 때, 그 객체를 자동으로 직렬화시켜 전달합니다.

그렇기에 파라미터로 전달되는 데이터는 serializable 인터페이스를 구현해야합니다.

데이터를 전달받은 원격 시스템에서는 직렬화 된 데이터를 역직렬화하여 사용하게 됩니다.