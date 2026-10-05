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

* 실제 진행 시간 : 코드 작성 1시간 40분, 설명 40분 진행
** 검증은 IntelliJ RUN, Chat GPT 로만 진행힘. (서술형 답변은 제외)
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

예상결과)
철수
15
철수
영희
2

검증) IntelliJ 검증 → 동일

다음 질문에도 답하세요.

1. `member1`과 `member2`는 서로 다른 객체인가요?
→ 같은 객체다
2. `member2.name`을 변경했는데 `member1.name`도 바뀌는 이유는 무엇인가요?
→ 둘은 같은 객체 변수가 다르더라도 같은 주소값을 가지고 있어서 해당 객체에 접근해서 값을 변경하는 것이기 때문에 값이 변한다. 변수에 값을 저장 하는것이 아닌, 주소값을 가지고 참조해서 해당 데이터에 접근하는 것이기 떄문에 동일 주소를 가지고 있어 값이 변하게 된다.
3. `Member.count`는 무엇을 세고 있나요?
→ 인스턴스를 생성하지 않고 Member에 직접 호출하는 static으로 쓰여있어, 현재 클래스에 선언된 멤버의 개수를 세고 있다.
4. `count`에서 `static`을 제거하면 각 객체의 값은 어떻게 달라지나요?
→ 현재 Member.count로 선언되고 있어서 객체의 값이 변하지 않고, 컴파일 오류가 난다.
개체의 변수로 바꾸면 member1.count로 print 출력을 할텐데, 이럴경우 객체를 직접 실행을 하는거라 0으로 초기화 된 상태에서 count++을 진행하는 것이므로 1밖에 나오지 않는다.
---

검증) Chat GPT 활용.
오류) 2번 내용 설명에서 주소와 참조를 모두 사용을 했으나 참조 단어 사용이 더 정확하다.
3번 내용의 경우, 생성자 안에서 count 값을 증가 시키는 건데, 해당 내용이 없다. 설명도 틀림.
member2의 경우 생성자로 생성된 것도 아니여서 포함하지 않음
추가공부필요) 여기서 static의 역할을 자세히 설명하자.

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

예상결과)
1000
2000

검증) IntelliJ 검증 → 동일

다음 질문에도 답하세요.

1. `money`는 변하지 않는데 `account.balance`는 변하는 이유는 무엇인가요?
→ account는 인스턴스를 생성하고 public 이라 값을 변경할수 있다. 그래서 balance의 경우 1000으로 값을 지정해 주었기에 1000으로 변경이 되고 메서드가 실행되어 
changeMoney 메서드의 경우 매개변수를 넘겼지만 return 이 없고 void이기 때문에 값이 변하지 않고, 실행 순서인, 초기값 그대로 값이 유지된다.
* 메서드에 static 에 대한 설명이 부족해보여서 추가로 찾아서 개념을 확실하게 알아야 할듯.
2. 메서드에는 객체 자체가 전달되나요, 객체를 가리키는 참조값이 전달되나요?
→ 메서드의 경우 참조값이 전달된다.
3. `account` 변수와 실제 `Account` 객체는 메모리상 같은 것인가요?
→ account 변수는 객체 생성을 한 정보를 담는 것으로 참조값을 가지고 있고, Account 객체 자체는 해당 클래스 정보이기에 다른 정보이다.
---

검증) Chat GPT 활용.
오류) 1번 코드에 public이 없다. 설명 틀림, void return 이랑 관계가 없음.
기본형과 참조형의 차이로 설명을 했어야 함.
3번 내용의 account 변수는 실제 Account 객체를 가리키는 참조값을 저장하는 변수이고, new Account()로 생성된 객체는 메모리에 실제로 생성된 Account 인스턴스이므로 서로 다르다.

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
→ owner, balance : private로 캡슐화 (객체 접근해서 입/출금 메서드로 변경하는것은 가능함)
- 계좌를 만들 때 소유자 이름과 최초 입금액을 반드시 받아야 합니다.
→  생성자 변수 추가,기본생성자 사용X (검증 로직 추가 X)
- 소유자 이름이 비어 있으면 계좌를 만들 수 없어야 합니다.
→ 생성자의 매개변수를 무조건 넘기기
- 최초 입금액은 음수가 될 수 없습니다.
→ 입금액 판별 메서드에서 로직 추가, 최초 판단 기준은 금액 0인것으로는 불가능하니, 입출금 체크하는 변수 선언
- 입금액은 0보다 커야 합니다.
→ 입금액 판별 메서드에서 로직 추가 
- 잔액보다 많은 금액을 출금할 수 없습니다.
→ 잔액 비교 메서드 로직 추가 
- 현재 잔액은 외부에서 조회할 수 있어야 합니다.
→ 잔액 조회하는 메서드 새로 생성 (public) 
- 잘못된 요청이 들어오면 오류 메시지를 출력하고 해당 작업을 중단하세요.
→ 오류 메시지 print 출력, return 구현

구현 후 다음 질문에 답하세요.

1. 필드를 `private`으로 만든 이유는 무엇인가요?
→ 두 필드 모두 외부에서 직접 변경할 수 없어야 하기 때문에, 캡슐화(제약)으로 외부에서 접근 안되도록 변경을 하였음.
2. 기본 생성자를 사용하지 않은 이유는 무엇인가요?
→ 계좌를 만들 떄 반드시 소유자 이름과 최초 입금액을 반드시 받아야 하기 떄문에, 기본 생성자를 생성하는게 아닌, 소유자 이름과 최초 입금액을 반드시 받아야 되서 기본 생성자를 생성하지 않음.
3. `balance`의 setter를 만들지 않은 이유는 무엇인가요?
→ 일단 강의 들을때 코드 작성 기준으로는 setter를 사용하지 않았음. 계좌 소유자와 잔액은 외부에서 직접 변경할 수 없는 변수다.
변수를 private로 하더라도, public 메서드로 setter 를 하는 구현할 수 있지만 여기서는 직접적으로 값을 세팅해주는 변경이 안되기에 못만든다.
4. 검증 로직을 실행 클래스가 아니라 `BankAccount` 안에 둔 이유는 무엇인가요?
→ BankAccount의 멤버 변수인 소유자와 잔액의 경우 외부에서 직접 변경할수 없어야 하기에, private로 사용하였다.
그리고 최조 입금액 조건이라던지, 출금 제약이란지 메서드 실행중에 판별하는 여러 조건들이 있어 내부에 두었음.

---
> BankAccount
```java
package checkTest;

public class BankAccount {
    private String owner;
    private int balance;
    private int cashCnt;

    public BankAccount(String owner, int amount) {
        if(owner.isEmpty()) {
            System.out.println("계좌를 만들 때 소유자 이름은 반드시 받아야 합니다.");
            return;
        }
        this.owner = owner;

        checkAmount(amount);
        deposit(amount);
    }

    public void deposit(int amount) {
        String msg = checkAmount(amount);
        if(!msg.equals("Success")) return;
        balance += amount;
        cashCnt++;
    }

    public void withdraw(int amount) {
        String msg = checkAmount(amount);
        if(!msg.equals("Success")) return;
        msg = checkWithDrawBalance(amount);
        if(!msg.equals("Success")) return;
        balance -= amount;
        cashCnt++;
    }

    public String checkAmount(int amount) {
        String msg = "Success";
        if (amount <= 0) {
            msg = "입금액은 0보다 커야 합니다.";
            if(cashCnt == 0 && amount < 0) msg = "최초 입금액은 음수가 될 수 없습니다.";
        }
        if(!msg.equals("Success")) System.out.println(msg);
        return msg;
    }

    public String checkWithDrawBalance(int amount) {
        String msg = "Success";
        if(balance-amount < 0) {
            msg = "잔액보다 많은 금액을 출금할 수 없습니다.";
            System.out.println(msg);
        }
        return msg;
    }

    public void showBalance() {
        System.out.println("현재 잔액은 : " + balance + "원입니다.");
    }

}
```

> BankAccountTest
```java
package checkTest;

public class BankAccountTest {
    public static void main(String[] args) {
        BankAccount bankAccount1 = new BankAccount("시루떡",20000);
        BankAccount bankAccount2 = new BankAccount("RANI",10000);

        bankAccount1.deposit(10000);
        bankAccount1.withdraw(30000);
        bankAccount1.showBalance();

        bankAccount2.deposit(10000);
        bankAccount2.withdraw(30000);
        bankAccount2.showBalance();

    }

}
```

예상결과)
현재 잔액은 : 0원입니다.
잔액보다 많은 금액을 출금할 수 없습니다.
현재 잔액은 : 20000원입니다.

검증) IntelliJ 검증 → 실패 : RUN 실행 2번 추가 더 진행하여 수정사항 반영 (생성자, 객체, 메서드 오류 수정 메서드 오류 수정)
- this.owner = owner;  코드 및 메서드 기능 수정 보완

검증) Chat GPT
1) 생성자 로직 추가
public BankAccount(String owner, int amount) {
    if(owner == null || owner.isEmpty()) {
        System.out.println("소유자 이름은 비어 있을 수 없습니다.");
        return;
    }
    this.owner = owner;
    deposit(amount);
}

2) 출금액은 0보다 커야 합니다 라는 로직 추가하라는 데.. 굳이 안넣어도 될거 같아 PASS
3) 테스트 코드 오타 : bankAccount1.showBalance(); 중복 실행

개인검증 추가) 다른 기능들 검증하는것 더 추가했었어야 했는데 생각을 못하였음.
기능은 동작한것 확인함.

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

> BankAccount
```java
-- code
```

예상결과) 실행 전 보이는 IntelliJ 빨간줄 오류 확인 등으로 작업하다 이상해서, 더 내려보니 실행 결과문이 정해져 있는것도 보여서..
틀리게 하고 있는것 발견도 하고 해서 아예 다른 코드인 것을 인지하여 넘어감.

검증) IntelliJ 검증 → 실패
틀렸지만 현재 코드 기준 메서드에서 static 메서드를 써야 오류가 안나는데 해당 개념 추가 공부가 필요함.

> Member (코드 변경 후)
```java
package checkTest;

public class Member {

    private String name;
    private int memberNo;
    private int attendCnt;
    private static int sNo = 1;

    public Member(String name) {
        if(!name.isEmpty()) {
            this.name = name;
            this.memberNo = sNo;
            sNo++;
        }
    }

    public void attend() {
        attendCnt++;
    }

    public void showMemberInfo() {
        //System.out.println("이름 : " + name + ", 번호 : " + memberNo + ", 출석 횟수 : " + attendCnt);
        System.out.println("[회원 번호:" + memberNo + "] " + name + "의 출석 횟수는 " + attendCnt + "회입니다.");
    }



}
```

> MemberRegistry (코드 변경 후)
```java
package checkTest;

class MemberRegistry {

    int limitCnt=5;
    private Member[] members = new Member[limitCnt];

    public void add(Member member) {
        if(curCnt() >= limitCnt) {
            System.out.println("최대 5명까지 저장할 수 있습니다. (등록 불가)");
            return;
        }
        members[curCnt()] = member;
    }

    public void printMembers() {
        for(int k=0; k<curCnt(); k++) {
            Member member = members[k];
            member.showMemberInfo();
        }
    }

    public int curCnt() {
        int cnt = 0;
        for(Member member : members) {
            if(member != null) cnt++;
        }
        return cnt;
    }

}
```

## 문제 5. `static` 판단하기

다음 항목을 `static`으로 만들어야 하는지 판단하고 이유를 적으세요.
* static 판단 여부 : O , X 로 기입함.

1. 회원 한 명의 이름
→ X / 회원 객체가 이미 독립적인 이름으로 필요가 없음. static으로 관리하는 가장 큰 이유는 new XXXX() 형태의 객체를 생성하지 않고 직접 관리하며 그 클래스 마다 공유하는 것이라고 보면 된다.
2. 회원 한 명의 출석 횟수
→ X / 위에 설명과 동일함.
3. 다음에 발급할 회원 번호
→ O / 회원 번호는 중복이 되면 안되기에 공통적으로 관리를 하는게 좋다. 객체마다 값이 달라야 하며, 모든 객체의 하나의 값을 공유해야 하는건 아니지만 자동으로 세팅을 해준다던지. 점검 로직을 한다던지 하면 모든 객체에서 하나의 값을 공유하는게 좋다. 객체 상태는 크게 영향은 있다. (제약조건이 있는 경우에만)
4. 프로그램에서 생성된 회원 전체의 수
→ X / 예제 4번과 달리 전체 회원 목록을 하나만 관리를 한다 하더라도, 하나만 객체 생성을 해서도 확인이 가능함. 의미가 없음.
5. 특정 회원의 정보를 출력하는 메서드
→ O / 메서드를 실행할때 계속 객체를 생성을 하는것은 의미가 없기 때문에, static 메서드로 생성하고, 객체 생성없이 메서드를 사용하여 값을 가져오면 된다. 
6. 두 숫자를 더해 결과만 반환하는 유틸리티 메서드
→ O / 위에 설명과 동일하다. 객체를 생성을 하지 않고 메서드 실행만 하면 된다.

단순히 "공유하니까"라고 답하지 말고 다음 기준으로 설명하세요.
* 중복되는 내용은 아래에 기입함.

- 객체마다 값이 달라야 하나요? → 객체마다 값이 달라야 한다면 인스턴스를 생성해서 별도로 관리를 해야하므로 static을 사용하면 안된다.
- 모든 객체가 하나의 값을 공유해야 하나요? → 모든 객체가 하나 값을 공유하는 건 위험한 일이다. 목적에 맞게 사용을 해야 정확한 데이터를 확인 할수 있다. 동일하게 사용 불가
- 메서드 실행에 특정 객체의 상태가 필요한가요? → 특정 조건일때만 실행하는 것이 아닌 이상에는, 특별히 객체 생성이 필요하지 않다. 상황에 따라 다르다.
- 객체를 만들지 않고 호출해도 자연스러운가요? → 오히려 부자연스러운것은 단순 메서드 기능을 쓰는데 계속 객체를 만드는 것

---

## 문제 6. 메모리 구조 설명하기

문제 4에서 작성한 프로그램을 기준으로 다음 항목이 어디에 존재하는지 설명하세요.

* 기본 개념 설명
자바 메모리 구조는 3가지로 구성되어 있으며 메서드 영역, 스택 영역, 힙 영역이 있다.
1) 메서드 영역의 경우 클래스에 대한 모든 정보를 보관하며
2) 스택 영역은 메서드 실행시 하나씩 쌓이는 영역이다. 후입선출과 선입선출 구조가 있는데 스택은 후입선출로 먼저 들어왔다고 먼저 빠지는 게 아니라 마지막 부분이 끝나고 사라지고 하는 것을 반복해서 한다고 보면 되고, 선입선출은 말 그대로 먼저 들어온 것 먼저 나가는 것이다. 큐 자료라고 들었는데 자세히는 모름.
3) 힙 영역은 인스턴스 생성 영역이며, 더 이상 참조할 수 없는 상태가 될 경우 가비지 컬렉션이 제거해서 값을 더이상 참조할수 없다.

- `main()`의 지역 변수 변수의 경우 → 클래스 정보므로 메서드 영역이다
- `Member member1` 변수 → Member member1 = new Member() 로 member1 변수 자체는 인스턴스를 생성은 했지만 객체 자체가 아닌, 참조값을 가지고 있는 변수이기 때문에 동일하게 메서드 영역이다.
- `new Member("민수")`로 생성한 객체 → 객체 생성 영역은 힙 영역이다. 위에 참조값을 가지는 변수와는 달리 생성된 객체에 접근해서 데이터 조회,수정 하는 것 가능하다.
- `Member`의 static 회원 번호 값 → static int memberNo 형태로 변수로 관리하기 때문에 메서드 영역이다.
- 실행 중인 메서드의 지역 변수 → 실행중인 상태는 아직 자바 실행 단계이기 때문에 메서드가 끝나기 전까지는 스택 영역에 있다. 스택 영역은 실제 프로그램이 실행되는 영역이 때문에 계속 스택이 쌓이거나, 쌓여진 스택의 메서드를 처리하고 사라지는 기능을 수행한다.

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
→ 인스턴스 변수는 객체 생성시 생성되는 변수인데 new 객체명() 이런식으로 객체 생성을 했을때마다 새롭게 관리가 가능하다.
static 의 경우 객체를 생성하지 않고 사용하기 위해 사용되며, 객체 사용없이 처음 정의된 상태를 유지하기 때문에 서로 다른 목적을 가지고 있다.
인스턴스는 기존의 값을 유지하는게 아닌 새로 생성하고, 사용을 하지 않으면 힙 영역에서 사라지는 특징을 가지지만 static은 클래스 영역

2. static 메서드가 인스턴스 변수를 바로 사용할 수 없는 이유는 무엇인가요?
→ 인스턴스 변수나 메서드에 접근하려면 참조값을 알아야 하는데 static 메서드에서는 참조값을 알수 있는 방법이 없다.

3. 객체지향 프로그램에서 모든 메서드를 static으로 만들면 어떤 문제가 생기나요?
→ 객체지향의 경우 대상에 초점을 맞춘건데, 모든 메서드를 static으로 만들면 대상에 초점을 맞출수 없다.

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
