主題：Springはテストに関してどのようなサポートをしてくれているのか？

超大枠：

1. TDD、なかなかうまくいかないよね。なぜ？→大変だから
2. Springはテストの大変な部分をめっちゃ簡単にしてくれるよ。
3. そもそもSpringで作ることで既にテストしやすいよ。
4. さらにたくさんの便利なアノテーションを提供してくれているよ。
5. 具体的ににどんなことができるかみてみよう。
----
# 1. 基礎編１
## 1.1 TDDについて
要約：要約：TDDってなかなか難しい。＝テストが難しい。でもspringはそれを簡単にしてくれるために色々サポートしてくれます。How?これから説明します。

## 1.2 Springのテストに関するサポートを一言でいうと、マジカルアノテーションとかがいっぱいある。

（便利モックオブジェクト＋サポートクラス＋アノテーションがいっぱいある図を出す）

図の目的：めっちゃサポートしてくれる（主にインテグレーションテストに関して）ことを示す

### アノテーションのカテゴライズ図
Springが指すのはどこか（core? boot?その他Umbrella projects?)

- カテゴライズその１：Spring / Spring Boot / Umbrella projects (i.e. Spring Cloud Contract)
- カテゴライズその２：Unit Test / Integration Test（インテグレーションテスト用が圧倒的に多い）

      確認すべきパッケージ（ライブラリ）
      Spring
        - spring-test
      Spring boot
        - spring-boot-test
        - spring-boot-test-autoconfigure
      Umbrella projects
          テストのためではない
            - Spring Security
              - spring-security-test
          テストの二次利用
            - Spring RestDocs（Test codes → Documents）
          テストの拡張
            - Spring Cloud Contract（発展的な TDD / アーキテクチャレベルの TDD みたいな）

## 1.3 Spring と Unit Test と Integration Test
### ユニットテスト
true unit test＝基本的には Spring は関係するべきでないとレファレンスにすら書いてある。

また、ユニットテストは本来RTI（DBなど）の関与が一切ないので、ものすごく早く実行されるものである。

>True unit tests typically run extremely quickly, as there is no runtime infrastructure to set up.

IoCベースで作られたアプリケーションのユニットテストにspringが関与する余地はあまりないが、springはいくつかのモックオブジェクトやサポートクラスを一応提供している。

##### Mock Objects
- Environment
  - MockEnvironment
  - MockPropertySource
- JNDI
  - ExpectedLookupTemplate
  - SimpleNamingContext
  - SimpleNamingContextBuilder)
- ServletAPI
  - [too many to list here](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/mock/web/package-summary.html)
- Spring Web Reactive
  - MockServerHttpRequest
  - MockServerHttpResponse
  - MockServerWebExchange
##### Support Classes
- General testing utilities
  - org.springframework.test.util package (use in unit & integration testing)
- Spring MVC
  - org.springframework.test.web package

      実際のコードサンプルを貼る。
      Springのロゴが出てるログのキャプチャ貼って、
      いちいち起動してるとテストに時間がかかってしまうことの説明もアリ


### インテグレーションテストのゴールについて
##### Spring Integration Testのゴール（springの恩恵を受けれる）はこれだ！
  - **Cache (絵を持って説明「時短だよ」)**
  - **テストで必ず必要なbeanをDIしてくれる**
  - **適切なトランザクション処理をしてくれる（rollbackとか）**
  - 便利クラスの提供

# 2. 基礎編２
## 2.1 MVC層のテスト（[Reference](https://docs.spring.io/spring/docs/current/spring-framework-reference/testing.html#spring-mvc-test-framework)）
### MockMvc

### WebApplicationContext

## 2.2 データアクセス層のテスト（[Reference](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-testing.html#boot-features-testing-spring-boot-applications-testing-autoconfigured-jpa-test)）

## 2.3 Spring Bootのテストサポート([Reference](https://docs.spring.io/spring-security/site/docs/current/reference/html/test-method.html))

### SecurityContextHolder

###### .getContext().setAuthentication()

### SecurityMockMvcConfigurers.springSecurity()
 > will perform all of the initial setup we need to integrate Spring Security with Spring MVC Test

### Annotations

###### @WithMockUser

###### @WithUserDetails
