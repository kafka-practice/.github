# MSA 환경 도전 + 적응기 - MSA with Kafka

<br>
기존의 프로젝트에서 저는 DB를 하나로 사용한 MSA 환경을 구성했었습니다.<br>
하지만 ✨하나의 DB로 모든 서비스를 연동✨ 시, 관리가 편하다는 장점이 있지만<br>
✨동시성 문제✨ 등의 문제가 발생 가능하다는 것을 알게되었습니다.<br>
그렇다면, 어떻게 실무에서는 다중 DB를 구현할까라는 의문점이 생겼습니다.<br>
이후 Kafka에 대해 알게되었고, ✨Kafka를 통해 MSA DB 동기화를 수행한다는 것✨을 알게되었습니다.<br>
Kubernetes 환경에서 ✨Kafka with SASL_TLS✨는 구현해본 상태이며<br>
실제 프로젝트에 적용해보기 전, ✨간이 MSA 환경 with 독립적 DB✨를 구성해보려 합니다.<br>
<br>

**✨ 목표** <br>
- [x] Github Actions + ArgoCD를 활용하여 CI/CD를 구성
- [x] GCP Kubenetes 환경을 Terraform을 이용하여 수행
- [x] 각 MSA 프로젝트를 쿠버네티스 상에 배포
- [ ] Spring Cloud를 적용하여 API Gateway 역할 수행 서버 생성
- [x] Kafka를 SASL_TLS 적용하여 쿠버네티스 상에서 관리
- [x] kafka-user -> kafk-post 서버로 DB 데이터 동기화 - Transactional Outbox Pattern
- [x] gRPC를 사용하여 MSA 간 API 요청
- [x] istio를 적용하여 애플리케이션 간 mTLS 활성화
- [x] OpenTelemetry + Jaeger를 이용하여 Trace 정보 수집 및 시각화
<br>

**🌲 프로젝트 아키텍쳐 구조** - 계획 변경 후 <br>
![제목 없는 다이어그램 drawio](https://github.com/user-attachments/assets/9d289fef-41b6-4701-af3f-0cac782dec4f)
<br>
<br>

## 💾 소스 코드 구조
- [x] [kafka-user](https://github.com/kafka-practice/kafka-user)
- [x] [kafka-post](https://github.com/kafka-practice/kafka-post)

<br>

🖥️ Reference <br>
1. [Transactional Outbox Pattern with Microservices and Kafka - CuriousJinan 블로그](https://curiousjinan.tistory.com/entry/transactional-outbox-pattern-microservices-kafka#Transactional%20Outbox%20Pattern%EC%9D%98%20%EC%82%AC%EC%9A%A9%20%EC%82%AC%EB%A1%80-1)<br>
2. [AmazingEffect - Github](https://github.com/AmazingEffect)

