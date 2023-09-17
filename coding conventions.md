# Source code organization
  * **소스 파일 이름**
    * 소스 파일에 최상위 클래스가 하나 뿐인 경우 파일 이름에 대소문자를 구분하는 이름과 ```.kt``` 확장자 반영해야 한다.
    ```kotlin
      // MyClass.kt
      class MyClass { }
    ```
    * 소스 파일에 최상위 수준 선언이 여러 개 있는 경우 파일의 콘텐츠를 설명하는 이름으로 작성.
    * 소스 파일 이름은 파스칼 표기법(```Pascal Case```)을 따른다.
    * 파일 이름은 파일에 있는 코가 무엇을 하는지 설명해야하기 때문에  ```"Util"```과 같은 의미 없는 단어 사용을 피해야 한다.
    ```kotlin
      // Bar.kt
      class Bar { }
      fun Runnable.toBar(): Bar = // …

      // Map.kt
      fun <T, O> Set<T>.map(func: (T) -> O): List<O> = // …
      fun <T, O> List<T>.map(func: (T) -> O): List<O> = // …
    ```
    <br>

  * **클래스 레이아웃**
    * 클래스는 다음의 순서로 정렬된다. 
      * Property declarations and initializer blocks
      * Secondary constructors
      * Method declarations
      * Companion object
     
    ```kotlin
    class MyClass {
     // 속성 선언
     private var property1 : String 
      
      // 초기화 블록    
      init {
          property1 = "Property declarations and initializer blocks"
      }
    
      // 보조 생성자
      constructor(property2 : String){
          println("Secondary constructors")
      }
      
      // 메소드 선언
      fun method() 
          println("Method declarations")
      }
   
      // Companion object
      companion object {
        var age : Int = 10
      }
}

  fun main() {
  }
    ```
    * 메소드 선언은 관련 내용을 종합하여 위에서 아래로 클래스를 읽는 사람이 무슨 일이 일어나고 있는지 논리를 따를 수 있도록 선언한다.
    * 중첩 클래스는 해당 클래스를 사용하는 코드 다음에 선언한다.
    * 중첩 클래스가 클래스 내부에서 참조되지 않고 외부에서만 참조되는 않는 경우 companion object 다음에 선언한다.


    ```kotlin
    class MyClass {
     
      ... 

      // 메소드 선언
      fun method() 
          println("Method declarations")
      }
   
      // 내부에서 사용된 Nested classes
      private class NestedClass { }
 
      // Companion object
      companion object {
        var age : Int = 10
      }

      // 외부에서 사용된 Nested classes 
      class OuterNestedClass { ... }
      }

  fun main() {
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
    
    fun methode3()
}
        ```
    <br>

  * **오버로딩 레이아웃**
    * 오버로딩 메서드는 서로 이웃하게(근처에) 배치한다.
        ```kotlin
class Calculator {
 fun sum(num1 : Int , num2 : Int) : Int {
     return num1 + num2
 }
 
  fun sum(num1 : Int , num2 : Int, num3 : Int) : Int {
     return num1 + num2 + num3
 }
  
  fun subtract(num1 : Int , num2 : Int) : Int {
     return num1 - num2
 }
 
  fun subtract(num1 : Int , num2 : Int, num3 : Int) : Int {
     return num1 - num2 - num3
 }
  
}
        ```
    <br>

# Naming rules

* **함수 이름**
* **테스트 메소드 이름**
* **프로퍼티 이름**
* **backing 프로퍼티 이름**

# 참조
<https://adjh54.tistory.com/59>
  <https://developer.android.com/kotlin/style-guide?hl=ko>
