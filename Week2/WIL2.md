# 필수 정리 내용
## 1. 컨트롤러, 서비스, 리포지토리의 역할

- 컨트롤러 : 웹 MVC의 컨트롤러 역할
- 서비스 : 비즈니스 도메인 객체를 가지고 핵심 비즈니스 로직 구현 (ex. 회원은 중복가입이 안됨)
- 리포지토리 : 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리

## 2. TDD란? 왜 하는가?

- TDD(Test Driven Development, 테스트 주도 개발) : 테스트 케이스를 먼저 작성한 후, 테스트 케이스를 통과하기 위한 최소한의 코드를 개발하고 리팩토링하는 개발 방법이다.

### TDD를 하는 이유?
- 사전에 다양한 케이스를 고려해볼 수 있어 잠재적 오류들을 방어할 수 있다.
-  테스트를 통해 잘되고 있는가를 자주 확인하고 느낄 수 있어 피드백이 원활하게 이루어진다.
-  테스트 케이스는 설계를 할 당시에 코드가 어떤 의도를 가지고 작성되었는지, 어떤 결과 값이 나오길 기대하는지를 적기 때문에 코드를 쓴 사람의 의도를 충분히 파악할 수 있다.

# 선택 정리 내용
## 1. Mapping 하는 url을 바꿔보기

HelloController에서 helloMvc 메서드가 mapping하는 url을 hello-mvc에서 hello-name으로 변경

![image](https://user-images.githubusercontent.com/90572599/229357678-f3e50145-59af-4ea0-8979-50a4b2f15ec3.png)

실행 결과 

![image](https://user-images.githubusercontent.com/90572599/229357637-48ce97c2-1175-4734-b7e5-69154252b216.png)

## 2. 모델에 담아 뷰에 전해줄 때 값을 자신이 원하는 값들을 보내주기

HelloController에서 helloMvc 메서드가 mapping하는 url을 hello-add-value로 설정하고, 나이와 직업을 추가

![image](https://user-images.githubusercontent.com/90572599/229358434-e3057873-84a9-4c17-a8f2-240872fbddfc.png)

## 3. 자신만의 뷰 페이지에서 표시하고 싶은 값을 전해줘보기.  타임리프를 사용하여 웹상에서 이쁘게 출력해보기

값을 받아 적용할 문장 작성

![image](https://user-images.githubusercontent.com/90572599/229358497-a765b7bc-051b-4a43-8f21-053eaef33054.png)

실행 결과

![image](https://user-images.githubusercontent.com/90572599/229358529-7e9b0590-cc4e-48bc-b450-aeff50cbf63c.png)
