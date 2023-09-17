# 소스파일
  * **소스 파일 이름**
    ```kotlin
      // MyClass.kt
      class MyClass { }
    ```
    * 소스 파일에 최상위 클래스가 하나 뿐인 경우 파일 이름에 대소문자를 구분하는 이름과 ```.kt``` 확장자 반영

    ```kotlin
      // Bar.kt
      class Bar { }
      fun Runnable.toBar(): Bar = // …

      // Map.kt
      fun <T, O> Set<T>.map(func: (T) -> O): List<O> = // …
      fun <T, O> List<T>.map(func: (T) -> O): List<O> = // …
    ```
    * 소스 파일에 최상위 수준 선언이 여러 개 있는 경우 파일의 콘텐츠를 설명하는 이름으로 작성.
    * 파일 이름은 을 따를 것 = ```Upper Camel Case``` (```Pascal Case```)
    * 파일 이름은 파일에 있는 코드가 무엇을 하는지 설명해야 한다.
    * 따라서 파일 이름에 ```"Util"```과 같은 의미 없는 단어를 사용하는 것은 피해야 한다.
    <br>

  * **클래스 레이아웃**
    * 일반적으로 클래스의 내용은 다음의 순서로 정렬된다. 
      * Property declarations and initializer blocks
      * Secondary constructors
      * Method declarations
      * Companion object
      <br>

# 참조
