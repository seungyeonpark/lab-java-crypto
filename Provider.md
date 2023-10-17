### 1. Provider
  - CSP(Cryptographic Service Provider)
  - java.security.Provider 클래스의 구현체
  - 사용자가 특정 알고리즘의 인스턴스를 요청하면 JCA는 프로바이더 저장소에서 해당 알고리즘에 적합한 구현체를 찾아 인스턴스를 생성
    - 동일한 알고리즘이 여러 프로바이더에 정의되어 있으면 저장소의 선호 순서를 따름
    - 명시적으로 특정 프로바이터에 인스턴스를 요청할 수도 있음
      ``` java
      MessageDigest md = MessageDigest.getInstance("MD5", "BC");
      ```
      - 이 방법은 애플리케이션이 해당 프로바이더에 종속 상태가 되므로 권장하지 않음

### 2. Bouncy Castle 프로바이더를 등록해 보자 !
  1. 자바 실행 환경에 프로바이더 등록하기
     - BC 라이브러리 자바 실행 환경의 확장 라이브러리 디럭터리에 복사
      ```
     <JAVA_HOME>/jre/lib/ext
     <JRE_HOME>/lib/ext
      ```
     - java.security 파일에 Bouncy Castle 프로바이더 추가
      ```
      security.provider.1=sun.security.provider.Sun
      security.provider.2=sun.security.rsa.SunRsaSign
      security.provider.3=sun.security.ec.SunEC
      security.provider.4=com.sun.net.ssl.internal.ssl.Provider
      security.provider.5=com.sun.crypto.provider.SunJCE
      security.provider.6=sun.security.jgss.SunProvider
      security.provider.7=com.sun.security.sasl.Provider
      security.provider.8=org.jcp.xml.dsig.internal.dom.XMLDSigRI
      security.provider.9=sun.security.smartcardio.SunPCSC
      security.provider.10=sun.security.mscapi.SunMSCAPI
      security.provider.11=org.bouncycastle.jce.provider.BouncyCastleProvider
      ```
     - 프로바이더 가저오기
      ``` java
      Provider provider = Security.getProvider("BC");
      ```
  2. 애플리케이션에서 프로바이더 등록하기
     - BC 의존성 추가
     - 프로바이더 추가
      ``` java
      Security.addProvider(new BouncyCastleProvider());
      ```