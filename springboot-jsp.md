# 문제
- 결제모듈(EXIMBAY)에서 JSP 코드만 제공해서 Springboot에 JSP를 사용해야 했다.
- react에서 해결하는 방법도 고려해봤지만 JSP를 사용하는게 더 효율적이라고 판단했다. (cors에러, 암호화, 불필요한 Http요청과 응답)

## 해결
- springboot에 내장된 tomcat은 JSP를 지원하지 않아 Jasper라는 의존성을 추가했다.
```xml
<dependency>
  <groupId>org.apache.tomcat.embed</groupId>
  <artifactId>tomcat-embed-jasper</artifactId>
  <scope>provided</scope>
</dependency>
```
- jstl 문법을 사용하기 위해 의존성을 추가했다.
```xml
<dependency>
  <groupId>jstl</groupId>
  <artifactId>jstl</artifactId>
  <version>1.2</version>
</dependency>
```
- 위의 두가지를 추가했으나 Invocation Nullpoint Error가 발생하여 boot 실행시 추가 설정을 했다.
```java
	@Bean
	public TomcatServletWebServerFactory tomcatFactory() {
		return new TomcatServletWebServerFactory() {
			@Override
			protected void postProcessContext(Context context) {
				((StandardJarScanner) context.getJarScanner()).setScanManifest(false);
			}};
	}
```
## 배운 점
- jsp를 servlet으로 변환 시켜주는 Jasper에 대해 알게 되었다. [jasper 공식문서 보러가기](https://tomcat.apache.org/tomcat-9.0-doc/jasper-howto.html)

## 느낀 점
- 무조건적으로 레거시를 사용하지 않는 것보단 현재 상황을 고려하여 서비스에 적용하는 것이 좋다.
