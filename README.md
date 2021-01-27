# hc_contr

* 참고문서:
  * contract test
    * https://kouzie.github.io/spring/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C-%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C%EC%84%9C%EB%B9%84%EC%8A%A4-%ED%85%8C%EC%8A%A4%ED%8A%B8/#pact-consumer

위 페이지에 포함된 소스링크(페이지에 나와 있음)
github: https://github.com/Kouzie/sample-spring-cloud/tree/msa-test

실행순서
1) zipkin
2) elk
   github: https://github.com/deviantony/docker-elk 에서 yaml 파일 수정 후
   docker-compose up -d 
3) rabbit mq
4) pack 설치
5) 소스 mvn install
   -> 최상위 폴더에서 mvn install
   -> eureka unit test 오류시 disable
6) customer에서 contract 테스트 진행   
   -> constomerConsumerContractTest 를 테스트 하기 전에 disabled를 주석처리
   -> customer 폴더로 이동
   -> mvn test
   -> mvn pact:publish
   -> 테스트 등록확인: http://127.0.0.1:9292/
7) provider 테스트 진행
   -> account에서 AccountProviderContractTest에서 disabled를 주석처리
   -> account 폴더로 이동
   -> mvn test

* 위에서 7)에서 문제 없으면 contract 테스트가 성공한 것임
