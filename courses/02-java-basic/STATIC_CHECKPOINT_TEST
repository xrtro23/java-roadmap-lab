# Java 기본편 진도 점검 - `static`까지

Java 기본편의 **자바 메모리 구조와 `static`** 섹션까지 학습한 뒤 이해도를 확인하는 문제입니다.

이 점검은 문법 암기보다 다음 내용을 자신의 코드와 말로 설명할 수 있는지 확인합니다.

- 클래스, 객체, 인스턴스
- 기본형과 참조형
- 객체지향 프로그래밍
- 생성자
- 패키지
- 접근 제어자와 캡슐화
- 자바 메모리 구조
- `static`

`final`, 상속, 다형성, 컬렉션은 사용하지 않습니다.

## 진행 규칙

- 권장 시간은 코드 작성 30분, 설명 10분입니다.
- 검색과 AI 도움 없이 먼저 해결합니다.
- 실행 전에 예상 결과와 이유를 작성합니다.
- 답을 확인한 뒤에는 틀린 이유를 자신의 말로 기록합니다.
- 정답 코드는 원본 저장소가 아니라 자신의 Fork 또는 개인 브랜치에 작성합니다.

---

## 문제 1. 코드 실행 결과 예측

다음 코드의 출력 결과를 작성하세요. 코드를 직접 실행하기 전에 먼저 답해야 합니다.

```java
class Member {
    String name;
    int score;
    static int count;

    Member(String name, int score) {
        this.name = name;
        this.score = score;
        count++;
    }
}

public class MemberTest {
    public static void main(String[] args) {
        Member member1 = new Member("민수", 10);
        Member member2 = member1;

        member2.name = "철수";
        member2.score += 5;

        Member member3 = new Member("영희", 20);

        System.out.println(member1.name);
        System.out.println(member1.score);
        System.out.println(member2.name);
        System.out.println(member3.name);
        System.out.println(Member.count);
    }
}
```

다음 질문에도 답하세요.

1. `member1`과 `member2`는 서로 다른 객체인가요?
2. `member2.name`을 변경했는데 `member1.name`도 바뀌는 이유는 무엇인가요?
3. `Member.count`는 무엇을 세고 있나요?
4. `count`에서 `static`을 제거하면 각 객체의 값은 어떻게 달라지나요?

---

## 문제 2. 메서드 호출과 참조형

다음 코드의 실행 결과를 예측하고 이유를 설명하세요.

```java
class Account {
    int balance;
}

public class AccountTest {
    public static void main(String[] args) {
        int money = 1000;

        Account account = new Account();
        account.balance = 1000;

        changeMoney(money);
        changeAccount(account);

        System.out.println(money);
        System.out.println(account.balance);
    }

    static void changeMoney(int value) {
        value = 2000;
    }

    static void changeAccount(Account target) {
        target.balance = 2000;
    }
}
```

다음 질문에도 답하세요.

1. `money`는 변하지 않는데 `account.balance`는 변하는 이유는 무엇인가요?
2. 메서드에는 객체 자체가 전달되나요, 객체를 가리키는 참조값이 전달되나요?
3. `account` 변수와 실제 `Account` 객체는 메모리상 같은 것인가요?

---

## 문제 3. 잘못 설계된 클래스 고치기

다음 클래스에는 여러 문제가 있습니다.

```java
public class BankAccount {
    public String owner;
    public int balance;

    public BankAccount() {
    }

    public void deposit(int amount) {
        balance += amount;
    }

    public void withdraw(int amount) {
        balance -= amount;
    }
}
```

다음 조건에 맞게 수정하세요.

- 계좌 소유자와 잔액은 외부에서 직접 변경할 수 없어야 합니다.
- 계좌를 만들 때 소유자 이름과 최초 입금액을 반드시 받아야 합니다.
- 소유자 이름이 비어 있으면 계좌를 만들 수 없어야 합니다.
- 최초 입금액은 음수가 될 수 없습니다.
- 입금액은 0보다 커야 합니다.
- 잔액보다 많은 금액을 출금할 수 없습니다.
- 현재 잔액은 외부에서 조회할 수 있어야 합니다.
- 잘못된 요청이 들어오면 오류 메시지를 출력하고 해당 작업을 중단하세요.

구현 후 다음 질문에 답하세요.

1. 필드를 `private`으로 만든 이유는 무엇인가요?
2. 기본 생성자를 사용하지 않은 이유는 무엇인가요?
3. `balance`의 setter를 만들지 않은 이유는 무엇인가요?
4. 검증 로직을 실행 클래스가 아니라 `BankAccount` 안에 둔 이유는 무엇인가요?

---

## 문제 4. 회원 출석 관리 프로그램

회원 등록과 출석 처리를 담당하는 작은 프로그램을 작성하세요.

### `Member`

회원 한 명의 정보를 표현합니다.

필드:

```text
회원 번호
이름
출석 횟수
```

요구사항:

- 모든 필드는 외부에서 직접 변경할 수 없어야 합니다.
- 객체를 생성할 때 이름을 반드시 받아야 합니다.
- 이름이 비어 있으면 회원을 생성할 수 없습니다.
- 회원 번호는 1부터 자동으로 증가해야 합니다.
- 회원 번호는 프로그램 전체에서 중복되면 안 됩니다.
- 출석 처리는 메서드를 통해서만 할 수 있습니다.
- 이름, 번호, 출석 횟수는 조회할 수 있어야 합니다.

### `MemberRegistry`

여러 회원을 관리합니다.

요구사항:

- 최대 5명까지 저장할 수 있습니다.
- 컬렉션 대신 `Member[]` 배열을 사용합니다.
- 회원을 등록하는 메서드가 있어야 합니다.
- 모든 회원 정보를 출력하는 메서드가 있어야 합니다.
- 등록된 회원 수를 알려주는 메서드가 있어야 합니다.
- 회원이 가득 찼다면 더 등록하지 않고 안내 메시지를 출력합니다.
- 내부 배열을 외부에 직접 반환하면 안 됩니다.

다음 실행 코드가 동작하도록 구현하세요.

```java
MemberRegistry registry1 = new MemberRegistry();
MemberRegistry registry2 = new MemberRegistry();

Member member1 = new Member("민수");
Member member2 = new Member("영희");
Member member3 = new Member("철수");

registry1.add(member1);
registry1.add(member2);
registry2.add(member3);

member1.attend();
member1.attend();
member3.attend();

registry1.printMembers();
registry2.printMembers();
```

실행 결과에서 다음 사실을 확인할 수 있어야 합니다.

- 각 저장소가 관리하는 회원 목록은 서로 다릅니다.
- 회원 번호는 저장소와 관계없이 중복되지 않습니다.
- 민수의 출석 횟수는 2회입니다.
- 철수의 출석 횟수는 1회입니다.

---

## 문제 5. `static` 판단하기

다음 항목을 `static`으로 만들어야 하는지 판단하고 이유를 적으세요.

1. 회원 한 명의 이름
2. 회원 한 명의 출석 횟수
3. 다음에 발급할 회원 번호
4. 프로그램에서 생성된 회원 전체의 수
5. 특정 회원의 정보를 출력하는 메서드
6. 두 숫자를 더해 결과만 반환하는 유틸리티 메서드

단순히 "공유하니까"라고 답하지 말고 다음 기준으로 설명하세요.

- 객체마다 값이 달라야 하나요?
- 모든 객체가 하나의 값을 공유해야 하나요?
- 메서드 실행에 특정 객체의 상태가 필요한가요?
- 객체를 만들지 않고 호출해도 자연스러운가요?

---

## 문제 6. 메모리 구조 설명하기

문제 4에서 작성한 프로그램을 기준으로 다음 항목이 어디에 존재하는지 설명하세요.

- `main()`의 지역 변수
- `Member member1` 변수
- `new Member("민수")`로 생성한 객체
- `Member`의 static 회원 번호 값
- 실행 중인 메서드의 지역 변수

설명에는 다음 용어를 모두 사용하세요.

```text
스택
힙
메서드 영역
참조값
```

정확한 JVM 내부 구현이 아니라 강의에서 학습한 개념 수준으로 설명하면 됩니다.

---

## 문제 7. 구두 설명

코드를 보지 않고 3분 안에 다음 질문에 답하세요.

1. 인스턴스 변수와 static 변수의 차이는 무엇인가요?
2. static 메서드가 인스턴스 변수를 바로 사용할 수 없는 이유는 무엇인가요?
3. 객체지향 프로그램에서 모든 메서드를 static으로 만들면 어떤 문제가 생기나요?

## 평가 기준

| 평가 항목 | 배점 |
|---|---:|
| 실행 결과와 참조 이해 | 20점 |
| 캡슐화와 생성자 설계 | 20점 |
| 프로그램 구현 | 30점 |
| `static` 판단과 설명 | 20점 |
| 메모리 구조 설명 | 10점 |

권장 판정 기준:

- **80점 이상:** 현재 범위를 이해한 상태로 `final` 섹션 진행
- **60~79점:** 다음 진도를 진행하면서 틀린 부분 복습
- **40~59점:** 참조형, 캡슐화, `static`을 다시 학습
- **40점 미만:** 예제 재실행보다 객체와 메모리 변화 과정을 손으로 추적하며 복습

프로그램의 실행 여부만으로 평가하지 않습니다. 어떤 필드가 인스턴스에 속하고 어떤 필드가 클래스에 속하는지, 그리고 필드를 감춘 이유를 자신의 말로 설명할 수 있는지가 핵심입니다.
