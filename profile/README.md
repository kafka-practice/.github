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

**🌲 프로젝트 아키텍쳐 구조** - 프로젝트 구현 완료 후 <br>
![제목 없는 다이어그램 drawio](https://github.com/user-attachments/assets/9d289fef-41b6-4701-af3f-0cac782dec4f)
각 리소스 흐름 복습을 위해 네임스페이스를 중심으로 아키텍쳐를 그렸습니다.
<br>
<br>

## 💾 소스 코드 구조
- [x] [kafka-user](https://github.com/kafka-practice/kafka-user) - `메시지 프로듀싱`, `gRPC 서버`
- [x] [kafka-post](https://github.com/kafka-practice/kafka-post) - `메시지 컨슈밍`, `gRPC 클라이언트`

<br>

🖥️ Reference <br>
1. [Transactional Outbox Pattern with Microservices and Kafka - CuriousJinan 블로그](https://curiousjinan.tistory.com/entry/transactional-outbox-pattern-microservices-kafka#Transactional%20Outbox%20Pattern%EC%9D%98%20%EC%82%AC%EC%9A%A9%20%EC%82%AC%EB%A1%80-1)<br>
2. [AmazingEffect - Github](https://github.com/AmazingEffect)
<br>
<br>

### 후기
이 프로젝트를 수행하기 전, 저는 단순히 Kafka로 MSA를 구현한다고만 알고 있었습니다. <br>
이후 어떻게 구현하지? 라는 생각에 무작정 블로그를 찾아보았고, `Transactional Outbox Pattern`에 대해 알게되었습니다. <br>
해당 블로그 내용을 근거로, 시도를 하려했지만 너무 어렵다 싶었고 해당 블로그는 코드로된 정보가 거의 없었습니다. <br>
그래서 저는 무작정 깃허브에 `Transactional Outbox Pattern`을 검색했고, 위의 **AmazingEffect** 레포지토리를 발견했습니다. <br>
그덕에 프로젝트를 시작할 수 있었습니다. <br>
생각보다 매우 어려웠습니다. 처음 보는 코드들, 너무나 많은 클래스들이 있었지만 하나하나 분석하면서 흐름을 파악하였고, <br>
코드를 작성할 수 있었습니다. <br>
<br>
코드 작성을 하며 `AOP in Logging`, `새로운 패키지 아키텍쳐`, `Kafka in Spring`, `Trace` 등에 대해 알게되었습니다.<br>
특히나, AOP는 Trace 및 Span을 위해 필수적이며 어노테이션 기반 로깅을 구현하는 것은 매우 재미있었습니다.<br>
<br>
다음으로는 DevOps Engineer로써 역량을 높일 수 있었습니다. <br>
며칠 전까지만 해도, 저는 Jaeger 및 OpenTelemetry가 무엇인지 알지 못했습니다. <br>
그러나, 내 코드와 AmazingEffect 코드를 비교하면서 다른 점들을 분석하며 해당 오픈소스들의 존재를 알게되었습니다. <br>
그리고 인터넷을 찾아보며 공부하고 구축하여 어떤 흐름인지 파악하며 DevOps 지식을 얻을 수 있었습니다.. <br>
특히, Spring -> OpenTelemetry -> Jaeger 로깅 시스템 구축은 매우 어려웠지만, 성공 후에는 매우 뿌듯하고 신기했습니다. <br>
<br>
프로젝트를 진행하면서 프로젝트 진행 상황 및 구축 과정들은 빠지지 않고 해놓았습니다. <br>
저는 이러한 프로젝트 경험을 바탕으로, 이후 개발 팀프로젝트에서 더 자신감있게 DevOps를 담당하려고 합니다.<br>
이렇게 성장할 수 있는 기회를 준 AmazingEffect 레포지토리 주인분에게 정말정말 감사드립니다.
<br>
<br>
