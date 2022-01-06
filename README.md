---
title: "Unity CSharp Coding Standard"
date: 2022-01-06
---

## 머리말

### 기본 원칙

1. 가독성을 최우선으로 삼는다. (대부분의 경우 코드는 그 자체가 문서의 역할을 해야 함) 
2. 본 코딩표준을 따라 잘 짜여진 기존의 코드에서 배운다.


### 참조문서

이 코딩 표준은 아래의 코딩 표준에서 영감을 얻었음.
아래 코딩 표준의 내용을 거의 그대로 사용하였으며,
개인적인 목적에 의해 일부 되었음.
* [C# Coding Standards](https://docs.popekim.com/en/coding-standards/csharp) ([SPDX-License-Identifier: MIT](https://github.com/popekim/dev-docs-ko/blob/main/LICENSE))
* [leotgo/unity-coding-standards](https://github.com/leotgo/unity-coding-standards)

## I. 메인 코딩 표준

1. 클래스와 구조체의 이름은 파스칼 표기법을 따른다.

   ```cs
   class PlayerManager;
   struct PlayerData;
   ```

2. 지역 변수 그리고 함수의 매개 변수의 이름은 카멜 표기법을 따른다.

   ```cs
   public void SomeMethod (int someParameter) {
       int someNumber;
       int id;
   }
   ```

3. 메서드 이름은 기본적으로 동사(명령형)+명사(목적어)의 형태로 짓는다.

   ```cs
   public uint GetAge ()
   {
       // 함수 구현부...
   }
   ```

4. 단, 단순히 부울(boolean) 상태를 반환하는 메서드의 동사 부분은 최대한 `Is`, `Can`, `Has`, `Should`를 사용하되 그러는 것이 부자연스러울 경우에는 상태를 나타내는 다른 3인칭 단수형 동사를 사용한다.

   ```cs
   public bool IsAlive (Person person);
   public bool HasChild (Person person);
   public bool CanAccept (Person person);
   public bool ShouldDelete (Person person);
   public bool Exists (Person person);
   ```

5. 아래에 제시된 예를 제외하곤 모든 메서드의 이름은 파스칼 표기법을 따른다.

   ```cs
   public uint GetAge () {
       // 함수 구현부...
   }
   ```

6. public 메서드가 아닌 경우 카멜 표기법을 따른다. Visual Studio를 사용 시에는 별도의 스타일 규칙을 추가해야 할 수도 있음. ([자세한 설명](https://stackoverflow.com/questions/40856186/naming-rule-violation))

   ```cs
   private uint getAge () {
       // 함수 구현부...
   }
   ```

7. 상수의 이름은 모두 대문자로 하되 밑줄로 각 단어를 분리한다.

   ```cs
   const int SOME_CONSTANT = 1;
   ```

8. 상수로 사용하는 개체형 변수에는 `static readonly`를 사용한다.

   ```cs
   public static readonly MY_CONST_OBJECT = new MyConstClass ();
   ```

9. `static readonly` 변수는 모두 대문자로 하되 밑줄로 각 단어를 분리한다.

10. 초기화 후 값이 변하지 않는 변수는 `readonly`로 선언한다.

    ```cs
    public class Account {
        private readonly string mPassword;
    
        public Account (string password) {
            mPassword = password;
        }
    }
    ```

11. 네임스페이스의 이름은 파스칼 표기법을 따른다.

    ```cs
    namespace System.Graphics
    ```

12. 부울(boolean) 변수는 최대한 `is`, `can`, `has`, `should`를 사용하되 그러는 것이 부자연스러울 경우에는 상태를 나타내는 다른 3인칭 단수형 동사를 사용한다.

    ```cs
    bool isFired;                // 지역변수
    private bool m_isFired;       // private 멤버변수
    ```

13. 부울 프로퍼티는 앞에 `Is`, `Has`, `Can`, `Should` 중에 하나를 붙인다.

    ```cs
    public bool IsFired { get; private set; }
    public bool HasChild { get; private set; }
    public bool CanModal { get; private set; }
    public bool ShouldRedirect { get; private set; }
    ```

14. 인터페이스를 선언할 때는 앞에 `I`를 붙인다.

    ```cs
    interface ISomeInterface;
    ```

15. `private` 멤버 변수명은 앞에 `m_`을 붙이고 카멜 표기법을 따른다

    ```cs
    public class Employee
    {
        public int DepartmentID { get; set; }
        private int m_age;
    }
    ```

16. 값을 반환하는 함수의 이름은 무엇을 반환하는지 알 수 있게 짓는다.

    ```cs
    public uint GetAge();
    ```

19. 단순히 반복문에 사용되는 변수가 아닌 경우엔 `i`, `e` 같은 변수명 대신 `index`, `employee` 처럼 변수에 저장되는 데이터를 한 눈에 알아볼 수 있는 변수명을 사용한다.

20. 뒤에 추가적인 단어가 오지 않는 경우 줄임말은 모두 대문자로 표기한다.

    ```cs
    public int OrderID { get; private set; }
    public int HttpCode { get; private set; }
    ```

21. getter와 setter 대신 프로퍼티를 사용한다.

    **틀린 방식:**

    ```cs
    public class Employee
    {
        private string mName;
        public string GetName();
        public string SetName(string name);
    }
    ```

    **올바른 방식:**

    ```cs
    public class Employee
    {
        public string Name { get; set; }
    }
    ```

22. 지역 변수를 선언할 때는 그 지역 변수를 사용하는 코드와 동일한 줄에 선언하는 것을 원칙으로 한다.

23. `double`이 반드시 필요한 경우가 아닌 이상 부동 소수점 값에 `f`를 붙여준다

    ```cs
    float f = 0.5F;
    ```

24. `switch` 문에 언제나 `default:` 케이스를 넣는다.

    ```cs
    switch (number)
    {
        case 0:
            ... 
            break;
        default:
            break;
    }
    ```

25. `switch` 문에서 `default:` 케이스가 절대 실행될 일이 없는 경우, `default:` 안에 `Debug.LogError()` 또는 `Debug.Assert(false)` 란 코드를 추가한다.

    ```cs
    switch (type)
    {
        case 1:
            ... 
            break;
        default:
            Debug.LogError("unknown type");
            break;
    }
    ```

26. 재귀 함수는 이름 뒤에 `Recursive`를 붙인다.

    ```cs
    public void FibonacciRecursive();
    ```

27. 클래스 안에서 멤버 변수와 메서드의 등장 순서는 다음을 따른다.

    1. public 멤버변수/프로퍼티
    2. internal 멤버변수/프로퍼티
    3. protected 멤버변수/프로퍼티
    4. private 멤버변수
        * 단, 프로퍼티와 대응하는 private 멤버변수는 프로퍼티 바로 위에 적음
        * 단, 단일 멤버메서드에서 사용되는 private 멤버변수를 해당 priavte 멤버메서드 바로 위에 적는 경우에는 예외를 허용
    5. 생성자
    6. public 메서드
    7. Internal 메서드
    8. protected 메서드
    9. private 메서드

28. 대부분의 경우 함수 오버로딩을 피한다.

    **올바른 방식:**

    ```cs
    public Anim GetAnimByIndex(int index);
    public Anim GetAnimByName(string name);
    ```

    **틀린 방식:**

    ```cs
    public Anim GetAnim(int index);
    public Anim GetAnim(string name);
    ```

29. 클래스는 각각 독립된 소스 파일에 있어야 한다. 단, 작은 클래스 몇 개를 한 파일 안에 같이 넣어두는 것이 상식적일 경우 예외를 허용한다.

30. 파일 이름은 대소문자까지 포함해서 반드시 클래스 이름과 일치해야 한다.

    ```cs
    public class PlayerAnimation 
    {
    }
    ```
    
    ```
    PlayerAnimation.cs
    ```

31. 여러 파일이 하나의 클래스를 이룰 때(즉, partial 클래스), 파일 이름은 클래스 이름으로 시작하고, 그 뒤에 마침표와 세부 항목 이름을 붙인다.

    ```cs
    public partial class Human;
    ```

    ```
    Human.Head.cs
    Human.Body.cs
    Human.Arm.cs
    ```

32. 특정 조건이 반드시 충족되어야 한다고 가정(assertion)하고 짠 코드 모든 곳에 `assert`를 사용한다. `assert`는 복구 불가능한 조건이다.(예: 대부분의 함수는 다음과 같은 `assert`를 가질 수도... `Debug.Assert`(매개변수의 null 값 검사) )

33. 비트 플래그 열거형은 이름 뒤에 `Flags`를 붙인다.

    ```cs
    public enum VisibilityFlags
    {
    }
    ```

34. 디폴트 매개 변수 대신 함수 오버로딩을 선호한다.

35. 디폴트 매개 변수를 사용하는 경우, `null`이나 `false`, `0` 같이 비트 패턴이 0인 값을 사용한다.

36. 변수 가리기(variable shadowing)는 허용되지 않는다. 외부 변수가 동일한 이름을 사용중이라면 내부 변수에는 다른 이름을 사용한다.

    ```cs
    public class SomeClass
    {
        public int Count { get; set; }
        public void Func(int count)
        {
            for (int count = 0; count != 10; ++count)
            {
                // count를 사용
            }
        }
    }
    ```

37. 언제나 `System.Collections`에 들어있는 컨테이너 대신에 `System.Collections.Generic`에 들어있는 컨테이너를 사용한다. 순수 배열을 사용하는 것도 괜찮다.

38. `var` 키워드를 사용하지 않으려 노력한다. 단, 대입문의 우항에서 데이터형이 명확하게 드러나는 경우, 또는 데이터형이 중요하지 않은 경우에는 예외를 허용한다. `IEnumerable`에 `var`를 사용하거나 우항의 `new` 키워드를 통해 어떤 개체가 생성되는지 알 수 있는 등이 허용되는 경우의 좋은 예이다.

    ```cs
    var text = "string obviously";
    var age = 28;
    var employee = new Employee();
    
    string accountNumber = GetAccountNumber();
    ```

39. 싱글턴 패턴 대신에 정적(`static`) 클래스를 선호한다.

40. `async void` 대신에 `async Task`를 사용한다. `async void`가 허용되는 유일한 곳은 이벤트 핸들러이다.

41. 외부로부터 들어오는 데이터의 유효성은 외부/내부 경계가 바뀌는 곳에서 검증(validate)하고 문제가 있을 경우 내부 함수로 전달하기 전에 반환해 버린다. 이는 경계를 넘어 내부로 들어온 모든 데이터는 유효하다고 가정한다는 뜻이다.

42. 따라서 내부 함수에서 예외(익셉션)를 던지지 않으려 노력한다. 예외는 경계에서만 처리하는 것을 원칙으로 한다.

43. 위 규칙의 예외: `enum` 형을 `switch` 문에서 처리할 때 실수로 처리 안 한 `enum` 값을 찾기 위해 `default:` 케이스에서 예외를 던지는 것은 허용.

    ```cs
    switch (accountType)
    {
        case AccountType.Personal:
            return something;
        case AccountType.Business:
            return somethingElse;
        default:
            throw new ArgumentOutOfRangeException(nameof(AccountType));
    }
    ```

44. 함수의 매개변수로 `null`을 허용하지 않는 것을 추구한다. 특히 `public` 함수일 경우 더욱 그러하다.

45. `null` 매개변수를 사용할 경우 변수명 뒤에 `OrNull`를 붙인다

    ```cs
    public Anim GetAnim(string nameOrNull)
    {
    }
    ```

46. 함수에서 `null`을 반환하지 않는 것을 추구한다. 특히 `public` 함수일 경우 더욱 그러하다. 그러나 때로는 예외를 던지는 것을 방지하기 위해 그래야 할 경우도 있다.

47. 함수에서 `null`을 반환할 때는 함수 이름 뒤에  `OrNull`을 붙인다.

    ```cs
    public string GetNameOrNull();
    ```

48. 개체 초기자(object initializer)를 사용하지 않으려고 노력한다. 그 대신 생성자와 이름으로 지정한 매개변수(named parameter)를 사용하는 게 더 좋은 방법이다. 이 원칙에 대한 두가지 예는 다음과 같다.

    1. 개체 생성을 딱 한 군데서만 할 경우 (예: 한군데서만 사용하는 DTO)
    2. 개체 생성을 해당 클래스 안에 있는 정적 메서드에서 하는 경우 (예: Factory 패턴)

49. 쉐이더 코드가 아닌 이상, 대부분의 경우 삼항연산자를 피한다.

50. LogFormat 대신 [string interpolation](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated)를 사용한다.

   **틀린 방식:**

   ```cs
   Debug.Log("Player " + playerId + " took a hit from " + damageSource + " for " + damageAmount + " damage.");
   Debug.LogFormat("Player {0} took a hit from {1} for {2} damage.", playerId, damageSource, damageAmount);
   ```

   **올바른 방식:**

   ```cs
   Debug.Log($"Player {playerId} took a hit from {damageSource} for {damageAmount} damage.");
   ```


## II. 소스 코드 포맷팅

1. 탭(tab)은 띄어쓰기 4칸을 탭으로 사용한다.

2. 중괄호( `{` )를 열 때 새로운 줄에서 열든지 말든지 알아서 한다.

3. 한 줄에 변수 하나만 선언한다.

   **틀린 방식:**

   ```cs
   int counter = 0, index = 0;
   ```

   **올바른 방식:**

   ```cs
   int counter = 0;
   int index = 0;
   ```
4. switch 문의 내부는 중괄호( `{ }` )를 사용한다.
   ```cs
   switch(colorId)
   {
       case PlayerBodyColors.White : {
               playerBody.SetTexture(whiteTexture);
               break;
           }           
       case PlayerBodyColors.Red : {
               playerBody.SetTexture(redTexture);
               break;
           }
       default : {
               playerBody.SetTexture(defaultTexture);
               break;
           }
   }
   ```

5. 코드가 작성된 파일은 개행문자로 끝나야 한다.


