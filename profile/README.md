## MSA 환경 도전 + 적응기

기존의 프로젝트에서 저는 DB를 하나로 사용한 MSA 환경을 구성했었습니다.<br>
하지만 하나의 DB로 모든 서비스를 연동 시, 관리가 편하다는 장점이 있지만<br>
교착 상태 등의 문제가 발생 가능하다는 것을 알게되었습니다.<br>
이후 Kafka에 알게되어 ✨Kafka with SASL_TLS✨는 구현해본 상태이며<br>
실제 프로젝트에 적용해보기 전, ✨간이 MSA 환경 with 독립적 DB✨를 구성해보려 합니다.<br>

✨ - 목표 -
1. Github Actions + ArgoCD를 활용하여 CI/CD를 구성
2. GCP Kubenetes 환경을 Terraform을 이용하여 수행
3. 각 MSA 프로젝트를 쿠버네티스 상에 배포
4. Kafka를 SASL_TLS 적용하여 쿠버네티스 상에서 관리
5. Member -> Post 서버로 DB 데이터 동기화 - Transactional Outbox Pattern
6. gRPC를 사용하여 Post -> Member 데이터 확인

🖥️ Reference
[Transactional Outbox Pattern with Microservices and Kafka - CuriousJinan 블로그](https://curiousjinan.tistory.com/entry/transactional-outbox-pattern-microservices-kafka#Transactional%20Outbox%20Pattern%EC%9D%98%20%EC%82%AC%EC%9A%A9%20%EC%82%AC%EB%A1%80-1)
[AmazingEffect - Github](https://github.com/AmazingEffect)

