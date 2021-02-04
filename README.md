# hc_contr

* 참고문서:
  * contract test
    * https://kouzie.github.io/spring/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C-%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C%EC%84%9C%EB%B9%84%EC%8A%A4-%ED%85%8C%EC%8A%A4%ED%8A%B8/#pact-consumer

  * 위 페이지에 포함된 소스링크(페이지에 나와 있음)
    * github: https://github.com/Kouzie/sample-spring-cloud/tree/msa-test

* 실행순서
1. https://github.com/Kouzie/sample-spring-cloud/tree/msa-test의 Readme.md의 내용 수행
   1) zipkin
   2) elk
      * github: https://github.com/deviantony/docker-elk 를 다운받으면(clone)
        * docker-elk폴더가 생김
        * docker-elk/elasticsearch/config/elasticsearch.yaml의 내용 중에서
        * xpack.license.self_generated.type: trial을 xpack.license.self_generated.type: basic 으로 수정
      * docker-elk 폴더 안에서 다음 내용 수행
       * docker-compose up -d 
   3) rabbit mq
   4) pack 설치
2. https://github.com/Kouzie/sample-spring-cloud/tree/msa-test 의 소스 다운로드(clone)
  1) msa-test 폴더 안으로 이동 (cd msa-test)
   - mvn install
   - eureka unit test 오류시 disable (eurekaserver/src/test/java/.../EurekaserverApplicationTests.java에 @SpringBootTest아래에 @Disable를 추가
   - mvn install
  2) customer에서 contract 테스트 진행   
   - constomerConsumerContractTest 를 테스트 하기 전에 disabled를 주석처리 @Disabled 앞에 // 추가
   - customer 폴더로 이동
   - mvn test
   - mvn pact:publish
   - 테스트 등록확인: http://127.0.0.1:9292/
  3) provider 테스트 진행
   - account에서 AccountProviderContractTest에서 disabled를 주석처리 @Disabled 앞에 // 추가
   - account 폴더로 이동
   - mvn test

* 위에서 2.3)에서 문제 없으면 contract 테스트가 성공한 것임
