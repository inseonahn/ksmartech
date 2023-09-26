## 1. Source code organization
  * ### 1.1 소스 파일 이름
    * 소스 파일에 최상위 클래스가 하나뿐인 경우 파일 이름에 대소문자를 구분하는 이름과 ```.kt``` 확장자 반영해야 한다.
    ```kotlin
      // MyClass.kt
      class MyClass {}
    ```
    * 소스 파일에 최상위 수준 선언이 여러 개 있는 경우 파일의 콘텐츠를 설명하는 이름으로 작성.
    * 소스 파일 이름은 파스칼 표기법(```Pascal Case```)을 따른다.
    * 파일 이름은 파일에 있는 코드가 무엇을 하는지 설명해야 하기 때문에  ```"Util"```과 같은 의미 없는 단어 사용을 피해야 한다.
    ```kotlin
      // Bar.kt
      class Bar {}
      fun Runnable.toBar(): Bar = // …

      // Map.kt
      fun <T, O> Set<T>.map(func: (T) -> O): List<O> = // …
      fun <T, O> List<T>.map(func: (T) -> O): List<O> = // …
    ```
    <br>

  * **클래스 레이아웃**
    * 클래스는 다음의 순서로 정렬된다. 
      * 프로퍼티 선언 및 초기화 블럭
      * 보조 생성자
      * 메소드 선언
      * Companion object
     
    ```kotlin
    class MyClass {
        // 속성 선언
        private var property1: String
    
        // 초기화 블록    
        init {
            property1 = "Property declarations and initializer blocks"
        }
    
        // 보조 생성자
        constructor(property2: String) {
            println("Secondary constructors")
        }
    
        // 메서드 선언
        fun method() {
            println("Method declarations")
        }
    
        // Companion object
        companion object {
            var age: Int = 10
        }
    }
    ```
    * 메소드 선언은 관련 내용을 종합하여 위에서 아래로 클래스를 읽는 사람이 무슨 일이 일어나고 있는지 논리를 따를 수 있도록 선언한다.
    * 중첩 클래스는 해당 클래스를 사용하는 코드 다음에 선언한다.
    * 중첩 클래스가 클래스 내부에서 참조되지 않고 외부에서만 참조되는 않는 경우 companion object 다음에 선언한다.
    ```kotlin
    class MyClass {
        // 메소드 선언
        fun method() {
            println("Method declarations")
        }
    
        // 내부에서 사용된 Nested classes
        private class NestedClass {}
    
        // Companion object
        companion object {
            var age: Int = 10
        }
    
        // 외부에서 사용된 Nested classes 
        class OuterNestedClass {}
    }
    ```
    <br>

  * **인터페이스 레이아웃**
    * 인터페이스를 구현할 때는 인터페이스의 구성원과 동일한 순서로 구현 구성원을 유지
    ```kotlin
    interface MyInterface {
        fun methode1()
        fun methode2()
    }
    
    class MyClass : MyInterface {
        override fun methode1() {}
        override fun methode2() {}
        fun methode3() {}
    }
    ```

  * **오버로딩 레이아웃**
    * 오버로딩 메서드는 서로 이웃하게(근처에) 배치한다.
    ```kotlin
    class Calculator {
      fun sum(num1: Int, num2: Int) : Int {
          return num1 + num2
      }
      
       fun sum(num1: Int, num2: Int, num3: Int) : Int {
          return num1 + num2 + num3
      }
       
       fun subtract(num1: Int, num2: Int) : Int {
          return num1 - num2
      }
      
       fun subtract(num1: Int, num2: Int, num3: Int) : Int {
          return num1 - num2 - num3
      }
    }
    ```
    <br>

## 2. Naming rules
  * ### 2.1 명명 규칙 종류
   |                            용어                           |                                              설명                                              |           예시          |
   |:---------------------------------------------------------:|:----------------------------------------------------------------------------------------------:|:-----------------------:|
   |                  카멜 케이스(Camel Case)                  | 첫 글자는 소문자로 시작하여 소문자로 작성하며, 구분자를 대문자로 가지고 네이밍을 구성하는 방법 | val userId = "kst1234"  |
   |                 파스칼 케이스(Pascal Case)                | 첫 글자는 대문자로 네이밍을 구성하는 방법                                                      | val Userid = "kst1234"  |
   | 스네이크 케이스(Snake Case) / 팟홀 표기법 (Potholes Case) | 단어 별로 언더바(_)의 구분자를 가지고 네이밍을 구성하는 방법                                   | val user_id = "kst1234" |
   |                  케밥 케이스 (Kebab Case)                 | 단어 별로 하이픈(-)의 구분자를 가지고 네이밍을 구성하는 방법                                   | val user-id = "kst1234" |
   |         camel case with an uppercase first letter         | 첫 글자는 대문자로 작성하고 이후 문자는 카멜 케이스의 네이밍을 통해 구성하는 방법              | val UserId = "kst1234"  |
   |              upper case underscore-separated              | 대문자로 구성하며 언더바(_)를 기반하여 단어 별로 구분자로 구성하는 방법                        | var USER_ID = "kst1234" |


  * ### 2.2 패키지 이름
    * 패키지 이름은 항상 소문자이며 언더스코어(_)를 사용하지 않는다.
    * 여러 단어로 구성된 이름을 사용하는 것은 일반적으로 권장되지 않지만, 여러 단어를 사용해야 하는 경우에는 단어를 연결하거나 카멜 표기법을 사용한다.
    ```kotlin
       // Okay
       package com.example.deepspace
       // WRONG!
       package com.example.deepSpace
       // WRONG!
       package com.example.deep_space
    ```
    
  * ### 2.3 클래스(class)와 객체(object)
    * 이름은 대문자로 시작하고 카멜 케이스()를 사용한다.
      ```kotlin
      open class DeclarationProcessor { /*...*/ }

      object EmptyDeclarationProcessor : DeclarationProcessor() { /*...*/ }
      ```
      
  * ### 2.4 함수 이름
    * 함수 이름은 카멜 표기법 작성한다.
      ```kotlin
      fun processDeclarations() { /*...*/ }
      var declarationCount = 1
      ```
    * 팩토리 패턴에서 팩토리 함수는 추상 반환 유형과 동일한 이름을 가질 수 있습니다.
      ```kotlin
      interface Foo { /*...*/ }
      class FooImpl : Foo { /*...*/ }
      fun Foo(): Foo { return FooImpl() }
      ```
    * 팩토리 패턴에서 팩토리 함수는 추상 반환 유형과 동일한 이름을 가질 수 있습니다.

  * ### 2.5 테스트 메소드 이름
    * ```Backtick(`)```으로 감싸서 공백을 포함한 이름을 작성할 수 있다.
    * 유의할 점은 아직 Android 런타임에서는 지원되지 않는다.
    * 메소드 이름에 언더스코어도 허용된다.
    * 테스트 클래스의 이름은 테스트 중인 클래스의 이름으로 시작하고 Test로 끝납니다. 예를 들면 HashTest 또는 HashIntegrationTest입니다.
      ```kotlin
      class HashTest {
        @Test fun `ensure everything works`() { ... }

        @Test fun ensureEverythingWorks_onAndroid() { ... }
      }
      ```
      
  * ### 2.6 properties
    * 값이 변경되지 않는 속성으로 ```const```로 표시되거나 사용자 지정 get 함수가 없는 최상위 또는 객체 ```val``` 속성은 대문자 밑줄로 구분된 이름(```screaming snake case```)을 사용.
      ```kotlin
      const val NUMBER = 5
      val NAMES = listOf("Alice", "Bob")
      val AGES = mapOf("Alice" to 35, "Bob" to 32)
      val COMMA_JOINER = Joiner.on(',') // Joiner is immutable
      val EMPTY_ARRAY = arrayOf()
      ```
      
    * 동작 또는 변경 가능한 데이터가 있는 개체를 보유하는 최상위 수준 또는 개체 속성의 이름은 카멜 케이스 이름을 사용해야 합니다. (인스턴스 속성, 로컬 속성, 매개변수)
      ```kotlin
       val variable = "var"
       val nonConstScalar = "non-const"
       val mutableCollection: MutableSet = HashSet()
       val mutableElements = listOf(mutableInstance)
       val mutableValues = mapOf("Alice" to mutableInstance, "Bob" to mutableInstance2)
       val logger = Logger.getLogger(MyClass::class.java.name)
       val nonEmptyArray = arrayOf("these", "can", "change")
      ```
      
    * Top-level 또는 ```object```에 선언된 프로퍼티 중 동작이나 ```Mutable``` 데이터가 있는 객체를 다룰 경우 카멜 표기법을 따른다.
      ```kotlin
      val mutableCollection: MutableSet<String> = HashSet()
      ```
      
    * 싱글톤 오브젝트를 참조하는 경우 ```object``` 선언과 동일한 네이밍 스타일을 사용할 수 있다.
      ```kotlin
      val PersonComparator: Comparator<Person> = ...
      ```
      
    * ```Enum```의 경우 사용법에 따라 언더스코어로 구분된 대문자로 사용하거나 파스칼 표기법을 사용해도 괜찮다.
<br>
        
  * ### 2.7 backing properties
    * 개념적으로 같은 프로퍼티이지만 하나는 클래스 외부에 공개하고 다른 하나는 내부 구현을 담을 때 private으로 선언하고 언더스코어로 작성한 뒤 공개용 프로퍼티의 getter로 할당한다.
      ```kotlin
      class C {
        private val _elementList = mutableListOf<Element>()

        val elementList: List<Element>
             get() = _elementList
      }
      ```

  * ### 2.8 좋은 이름 선택
   * 클래스의 이름은 명사 또는 명사구로 작성한다. ex) ```List```, ```PersonReader```
   * 메소드의 이름은 동사 또는 동사구로 작성한다. ex) ```close```, ```readPersons```,```sort```, ```sorted```
   * 이름은 목적이 명확하게 나타나야하므로 의미 없는 단어(```Manager```, ```Wrapper``` 등)를 사용하는 것은 피하자.
   * 이름에 약어를 사용하는 경우 두 개의 문자(```IOStream```)일 때는 둘 다 대문자로 표기하고 그보다 더 긴 경우(```XmlFormatter```, ```HttpInputStream```) 파스칼 표기법으로 작성하자. 

<br>

# 3.Formatting
  * **들여쓰기(Indentation)**
    * 들여쓰기에 탭(tab)을 사용하지 않고, 4 spaces를 사용하길 권장.
    * 중괄호의 경우 여는 중괄호를 구문이 시작되는 줄 끝에 배치하고 닫는 중괄호를 여는 구문과 수평으로 정렬된 별도의 줄에 배치
       ```kotlin
       if (elements != null) {
           for (element in elements) {
               // ...
           }
       }
       ```
    * Kotlin에서는 세미콜론이 선택사항이므로 줄 바꿈이 중요합니다. 언어 디자인은 Java 스타일 중괄호를 가정하므로 다른 형식 지정 스타일을 사용하려고 하면 놀라운 동작이 발생할 수 있습니다.
   <br>
      
  * **가로공백(Horizontal whitespace)**
    * 이항 연산자 주위에 공백을 넣으세요 (```a + b```).
    * 범위 연산자 주위에는 공백을 넣지 마세요 (```0..i```).
    * 단항 연산자 주위에 공백을 넣지 마세요 (```a++```).
    * ```(```, ```[```,의 뒤 ```]```, ```)```,의 앞에는 공백을 두지 않는다.
    * 제어 흐름 키워드 (```if```, ```when```, ```for```, ```while```)와 해당하는 여는 괄호 사이에 공백을 넣으세요.
        ```kotlin
         // WRONG!
         for(i in 0..1) {
         }
         // Okay
         for (i in 0..1) {
         }
       ```
    * 기본 생성자 선언, 메소드 선언 또는 메소드 호출에서 여는 괄호 앞에 공백을 넣지 마세요.
       ```kotlin
       class A(val x: Int)
       
       fun foo(x: Int) { ... }
       
       fun bar() {
           foo(1)
       }
       ```
    * 쉼표(,) 또는 콜론(:) 뒤
       ```kotlin
         // WRONG!
         val oneAndTwo = listOf(1,2)
         // Okay
         val oneAndTwo = listOf(1, 2)
       
         // Okay
         class Foo : Runnable

         // WRONG!
         if (list.isEmpty()){
         }
         // Okay
         if (list.isEmpty()) {
         }
       ```
    * ```.```이나 ```?.``` 주위에 공백을 넣지 마세요. ```foo.bar().filter { it > 2 }.joinToString(), foo?.bar()```
    * ```//``` 뒤에 공백을 넣으세요. // 주석
    * 타입 매개변수를 지정하는 데 사용되는  ```<>```  주위에 공백을 넣지 마세요 ```class Map<K, V> { ... }```
    * ```::```사이에 공백을 두지 않는다. ```Foo::class, String::length```
         ```kotlin
         // WRONG!
         val toString = Any :: toString
         // Okay
         val toString = Any::toString
        ```
    * nullable 타입을 표시하는 ```?``` 앞에 공백을 넣지 마세요 ```String?```
    * 일반적으로 어떤 종류의 수평 정렬도 피하세요. 식별자의 이름을 다른 길이의 이름으로 바꾸더라도 선언이나 사용 형식에 영향을 주어서는 안 됩니다.
<br>

  * **줄바꿈**
    * 코드의 열 제한은 100자입니다. 아래 언급된 경우를 제외하고 아래 설명된 대로 이 제한을 초과하는 줄은 줄바꿈되어야 합니다.
    * 예외
      * 열 제한을 준수할 수 없는 줄(예: KDoc의 긴 URL)
      * ```package``` 및 ```import``` 문
      * 잘라서 셸에 붙여넣을 수 있는 주석의 명령줄
    * 줄바꿈 위치
      * 우선적으로 줄바꿈은 더 높은 구문 수준에서 하는 것이 좋습니다. 기타 정보:
      * 다음과 같은 '연산자 형식' 기호에서 행을 나누면 기호 앞에서 줄바꿈이 발생합니다.
       * 점 구분자(```.```, ```?.```)
       * 멤버 참조의 두 콜론(```::```)
      * 메서드 또는 생성자 이름은 뒤에 오는 열린 괄호(```(```)에 연결된 상태로 유지됩니다.
      * 쉼표(```,```)는 앞에 오는 토큰에 연결된 상태로 유지됩니다.
      * 람다 화살표(```->```)는 앞에 오는 인수 목록에 연결된 상태로 유지됩니다.
        
  * **콜론(Colon)**
    * 기본 클래스 또는 인터페이스를 지정하기 위해 클래스 선언에 사용된 경우나, 일반 제약조건의 where 절에 사용된 경우에만 콜론(```:```) 앞에 공백을 두며, 콜론(```:```)뒤에는 항상 공백 .
       ```kotlin
         // WRONG!
         class Foo: Runnable
         // Okay
         class Foo : Runnable

         // WRONG!
         fun <T: Comparable> max(a: T, b: T)
         // Okay
         fun <T : Comparable> max(a: T, b: T)

         class FooImpl : Foo() {
         constructor(x: String) : this(x) { /*...*/ }
  
         val x = object : IFoo { /*...*/ }
        }
       ```
       <br>
       
  * **Class headers(class header(매개변수, 기본 생성자 및 기타 사항 지정))**
    * 클래스 선언은 class name, class header(매개변수, 기본 생성자 및 기타 사항 지정) 및 중괄호로 묶인 class body(바디)으로 구성된다.
    * header와 body는 선택사항이며, 클래스에 body가 없으면 중괄호를 생략해도 된다.
    * 헤더가 짧은 기본 생성자의 경우 클래스는 한 줄로 작성 가능
       ```kotlin
       class Person(id: Int, name: String)
       ```
    * 헤더가 긴 기본 생성자의 경우 들여 쓰기와 함께 라인으로 구분하며, 또한 닫는 소괄호 ```)```는 새로운 라인에 있어야 한다.
       ```kotlin
        class Person(
          id: Int,
          name: String,
          surname: String
        )
       ```
    * 상속을 사용하는 경우 슈퍼클래스 생성자 호출 또는 구현된 인터페이스 목록은 괄호와 같은 줄에 있어야 한다.
       ```kotlin
        class Person(
            id: Int,
            name: String,
            surname: String
        ) : Human(id, name) { /*...*/ }
       ```
    * 여러 인터페이스의 경우 슈퍼클래스 생성자 호출을 먼저 찾은 다음 각 인터페이스를 다른 줄에 배치
       ```kotlin
        class MyFavouriteVeryLongClassHolder :
            MyLongHolder<MyFavouriteVeryLongClass>(),
            SomeOtherInterface,
            AndAnotherOne {
        
            fun foo() { /*...*/ }
        }
       ```
       <br>
  * **함수(Functions)**
   * 함수 서명이 한 줄에 들어가지 않으면 각 매개변수 선언을 한 줄에 하나씩 표시
   * 이 형식으로 정의된 매개변수에서는 단일 들여쓰기(+4)를 사용해야하며, 닫는 괄호(```)```) 및 반환 유형은 추가 들여쓰기 없이 한 줄에 하나씩 입력
        ```kotlin
         fun longMethodName(
             argument: ArgumentType = defaultValue,
             argument2: AnotherArgumentType,
         ): ReturnType {
             // body
         }
        ```
   * 단일 표현식으로 구성된 본문이 있는 함수는 표현식 함수 사용을 권장.
        ```kotlin
         fun foo(): Int {     // bad
             return 1
         }
         fun foo() = 1        // good
        ```
   * 속성 이니셜라이저가 한 줄에 들어가지 않을 경우 등호(=) 뒤에서 줄바꿈하고 들여쓰기를 사용합니다.
        ```kotlin
         private val defaultCharset: Charset? =
             EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
        ```
        <br>

  * **Properties**
   * ```Read-only```의 간단한 프로퍼티의 경우 한 줄 작성 권장.
        ```kotlin
        val isEmpty: Boolean get() = size == 0
        ```
   * 복잡한 프로퍼티의 경우 ```get``` 과 ```set``` 을 분리된 라인에 선언.
      ```kotlin
      val foo: String
          get() { ... }      
      ```
   * 초기화 코드가 있는 프로퍼티의 경우, 초기화 코드가 길다면 줄바꿈 처리하여 4칸 공백 들여 쓰기 한다.
      ```kotlin
      private val defaultCharset: Charset? =
          EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)      
      ```
<br>

  * **제어문 형식**
   *  ```if```나 ```when```과 같은 조건문이 멀티라인일 경우 항상 중괄호```{```를 실행 구문에 가깝게 둔다.
   * 조건의 닫는 괄호```}```를 여는 중괄호와 함께 별도의 줄에 배치.
      ```kotlin
       if (!component.isSyncing &&
           !hasAnyKotlinRuntimeInScope(module)
       ) {
           return createKotlinNotConfiguredPanel(module)
       }
      ```
   * ```else```, ```catch```, ```finally``` 키워드와 ```do/while```, ```while``` 루프 키워드는 이전 중괄호 ```}```와 동일한 라인에 둔다.
      ```kotlin
       if (condition) {
           // body
       } else {
           // else part
       }
       
       try {
           // body
       } finally {
           // cleanup
       }
      ```
   * 명령문 에서 ```when```분기가 한 줄 이상인 경우 빈 줄을 사용하여 인접한 케이스 블록과 분리 권장.
      ```kotlin
       private fun parsePropertyValue(propName: String, token: Token) {
           when (token) {
               is Token.ValueToken ->
                   callback.visitValue(propName, token.value)
       
               Token.LBRACE -> { // ...
               }
           }
       }
       
       when (foo) {
           true -> bar() // good
           false -> { baz() } // bad
       }
      ```
<br>

  * **메소드 호출**
   * 체인된 호출을 줄 바꿈할 때는 ```.``` 문자나 ```?.``` 연산자를 다음 줄에 작성하고, 들여쓰기를 한 번 추가하세요.
   * ```=```인수 이름과 값을 구분하는 기호 주위에 공백을 두십시오 .
      ```kotlin
       drawSquare(
           x = 10, y = 10,
           width = 100, height = 100,
           fill = true
       )
      ```
 <br>

  * **체이닝 호출**
   * 긴 인수 목록에서는 여는 괄호 뒤에 줄 바꿈을 넣습니다. 인수를 공백 4개로 들여씁니다. 밀접하게 관련된 여러 인수를 같은 줄에 그룹화합니다.
   * =인수 이름과 값을 구분하는 기호 주위에 공백을 두십시오 .
      ```kotlin
      val anchor = owner
          ?.firstChild!!
          .siblings(forward = true)
          .dropWhile { it is PsiComment || it is PsiWhiteSpace }
      ```
 <br>
 
  * **람다**
   * 중괄호(```{}```) 주위와 매개변수를 본문에서 구분하는 화살표(```>```) 주위에 공백을 사용.
   * 여러 줄의 람다에서 매개변수 이름을 선언할 때 첫 번째 줄에 이름을 입력하고 그 뒤에 화살표와 줄 바꿈을 입력합니다.
     ```kotlin
      appendCommaSeparated(properties) { prop ->
          val propertyValue = prop.get(obj)  // ...
      }
      ```

   *  매개변수 목록이 너무 길어서 한 줄에 다 들어갈 수 없다면 화살표를 별도의 줄에 넣으세요.
      ```kotlin
      foo {
         context: Context,
         environment: Env
         ->
         context.configureEnv(environment)
      }
      ```
<br>

## 4.참고
* <https://developer.android.com/kotlin/style-guide?hl=ko>
* <https://kotlinlang.org/docs/coding-conventions.html>
