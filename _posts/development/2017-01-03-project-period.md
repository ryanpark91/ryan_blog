---
layout: post
title: 개발 일정 산정은 어떻게 해야할까?
date: 2017-01-04
excerpt: "개발 기간 산정에는 늘 괴리감이 있었다. 최근 진행했던 프로젝트를 통해 이 괴리감이 왜 생겼는지 고민해보고 개선 방안을 적어보았다."
tags: [프로젝트, 개발, 일정, ddd, domain-driven-design]
comments: true
---

# 1. 서론

최근 회사에서 맡은 업무를 진행하면서, ‘개발 일정은 어떻게 산정해야 하는가?’라는 생각을 하게 되었다. 처음 내가 산정한 기간은 2주였다. 그러나 이것을 들은 팀장님께선 너무 짧게 잡은 것 같다 말씀하시며 한 달 정도의 기간을 산정하셨다. 개발을 시작하기도 전에 나는 일정 산정 앞에 괴리감을 느꼈다. 하지만 이것이 끝이 아니었다. 개발을 진행하면서 여러 이슈들이 생겨났고, 개발 기간은 점점 늘어나 한 달을 훌쩍 뛰어넘어 결국 9주라는 시간이 걸렸다. 처음 내가 산정했던 2주에 비하면 9주는 매우 긴 시간이며, 엄청난 차이다. 엄청난 괴리를 경험한 나는 개발 기간을 산정하고, 개발을 시작하고 완성하기까지 내가 겪었던 문제점들을 적음으로 다음 개발 일정 산정함 있어 유의해야 할 점들을 기억하고자 한다. 그리고 이 글을 읽는 독자들에게도 내가 겪은 문제점들과 유의점들을 통해 그들의 개발 일정 산정에 도움이 되었으면 좋겠다. 

# 2. 본론

## 2.1 처음에 왜 개발 기간을 2주로 산정하였나?

처음 개발 기간을 산정하던 당시 여러 이유가 있었던 것 같다.

-  **첫 번째 이유: 자기가 스스로에게 주는 압박**

   당시 나는 회사에 입사한지 4개월 정도 된 상태였다. 그때 맡은 프로젝트는 3개월의 수습이 끝난 뒤 맡은 첫 프로젝트였다. 더군다나 훈련소(병특이라 4주 훈련)에서 돌아온 뒤 맡은 첫 테스크였기 때문에, 열심히 하는 모습을 보여야 한다는 생각이 강했다. 그리고 무엇보다 팀장님이 생각한 것보다 기간을 길게 잡으면 안 될 것 같은 느낌(?)이 있었다. 그래서 조금은 빠듯하게 산정하였었던 것 같다. (지금 생각해보면 바보같은..)

-  **두 번째 이유: 기존 레거시 코드에 대한 분석 부족**

    기간 산정 당시의 모습을 돌이켜 보면서 발견한 문제점은 기존 레거시 코드에 대한 분석이 없었다는 것이다. 나는 단순히 주어진 요구사항들의 목록을 나열하고, 각각 예상되는 개발 기간을 “대충” 산정하였다. 지금 돌아보니 개발 시작 전 팀장님께서 “먼저 기존 코드들을 보고 도메인 규칙들을 정리해 보세요.” (*도메인 규칙이란 ‘물품이 배송되고 나면 배송지를 변경할 수 없다’와 같은 규칙들을 말한다. 자세한 것은 검색…) 라고 말하신 것이 이제야 조금 이해가 간다. 


## 2.2 실제 개발하면서 왜 9주까지 늘어나게 되었나?

앞서 (2.1 처음에 왜 개발 기간을 2주로 산정하였나?)에서 얘기한 문제점은 순수 나의 잘못이라면 여기서는 조금은 외부적인 문제도 있었다. 대부분 내가 예상하기 힘든 이슈들 이었다.

- **첫 번째 이유: 우리가 사용하고 있는 외부 라이브러리의 버그**

  우리는 외부 라이브러리로 **[Doctrine](https://en.wikipedia.org/wiki/Doctrine)**이라는 ORM을 사용하고 있었다. 버그의 간략한 내용을 말하면, main entity와 여기에 포함된 sub entity가 있을 때, entity를 save를 할 경우 main entity의 변경사항만 저장되고 sub entity의 변경사항은 저장되지 않는 문제가 있었다.(자세한 버그 내용은 [여기](https://github.com/doctrine/doctrine2/issues/4142)에..) 나는 당시에 버그일거란 생각은 상상조차 못한 채  나의 개발실력 부족이라는 생각만 하며 거의 이틀을 날려버렸다. 버그라는 것을 알았을 땐 허무했다...

- **두 번째 이유: 팀내에 새로 생겨나는 새로운 코드 규약**

  현재 팀내에서 **[DDD(Domain-Driven-Design)](https://en.wikipedia.org/wiki/Domain-driven_design)**을 적용하여 개발중에 있다. 아직 DDD를 적용하는데 초기 단계라서 다양한 경우에 대한 명확한 코드 규약이 없었다. 그래서 개발 중간 중간에 팀내의 새로운 코드 규약을 회의를 통해 정해야 할 때가 있었다. 예를 들어 '응용 서비스과 도메인 서비스의 네이밍을 어떻게 할것인가?', '디렉토리 구조는 어떻게 가져갈 것인가?'과 같은 것이다. 이것이 별것 아닌 것처럼 보일 수도 있지만, 개발 중간에 새로운 코드 규약이 어떻게 정해지냐에 따라 변경해야 할 파일들이 크게 늘어날 수 있다.

- **세 번째 이유: 개발중간에 새로 생겨나는 요구사항**

  이것은 초기에 누락한 요구사항인 경우도 있었고 개발이 완성될 쯤에 새로운 요구사항이 생긴 경우도 있었다. 새로운 요구 사항을 예를 들면, 기존의 요구사항에는 '관리자가 알림을 고객들에게 보낼 수 있다' 뿐이었지만, 추후에 생긴 추가 요구사항은 '관리자가 실수로 알림을 보낼수도 있기에 알림 회수기능이 필요하다'와 같은 것이다.

- **네 번째 이유: 생각보다 컸던 규모**

  이것은 (2.1 처음에 왜 개발 기간을 2주로 산정하였나?)에서 언급했던 두번째 이유랑 비슷한 맥락인데, 초기에 레거시 코드에 대한 분석 없이 개발을 시작하다 보니 개발을 진행 할수록 새로운 클래스가 추가적으로 필요하거나, 동일한 기능을 하는데 여러 클래스에 기능이 분산되어 있던 것을 뒤늦게 알아차리거나 같은 일이 생겨났다.


## 2.3 어떻게 이러한 문제점을 개선할 수 있을까?

나는 이러한 문제를 개선하기에 앞서, 개발 하는 내내 '내가 실력이 부족해서 이렇게 오래 딜레이 되었군아'라는 자괴감이 많이 들었던 것 같다. 이러한 생각이 들었던 이유는 **내가 하루 10이란 일을 했어야 했는데 5정도의 일을 한 것인지, 원래 5정도 밖에 할 수 없는 양인데 내가 10으로 잡은건지** 감이 안 잡혔기 때문이다. 
그럼 이것을 어떻게 개선할 수 있을까? 사실 이건 답이 없다. 그 동안의 축적된 경험으로 산정하기 때문이다. 이런 고민에 대해 팀장님께 여쭤보았는데 팀장님의 답변도 '감'이라고 하였다. 하지만 이러한 감을 잘 잡는데 도움이 될만한 방법이 있다.

### 2.3.1 매일의 업무 일지를 쓴다

조금 놀라웠던 거는 개발 경험이 많은 팀장님도 개발일지를 쓰고 계셨다. 여기서 말하는 개발 일지는 업무에 대해 자세하게 기록하진 않고 간략하게 오늘 자신에게 할당한 업무에 대해, 그리고 어느 정도 달성했는지 확인 할 수 있는 정도로 쓴다. 예를 들면 아래와 같다

|    해야 할 업무    |    갑자기 생긴 업무    |
| :-----------: | :-------------: |
| * 리뷰 추가 기능 수정 | - CMS 페이지 버그 수정 |
| - 리뷰 삭제 기능 추가 |       ...       |

*(참고: \*는 당일 반드시 끝내야 하는 업무를 표시한 것)*

왼쪽의 해야 할 업무는 전날 내가 미리 산정해 놓은 일일 할당량이다. 반대로 오른쪽은 그날 당일 갑자기 생긴 업무들을 적는다. 예를 들어 당일 갑자기 서비스 중인 서버에 문제가 생긴 경우나 급하게 요청온 것을 대응해야 할 경우가 오른쪽 영역에 적히게 된다. 이렇게 적어두고 퇴근 후 작성해 놓은 개발 일지를 검토해 보자. 이렇게 하루 이틀 쌓다 보면, 자신이 하루에 어느 정도 일을 처리할 수 있는지 감이 생길 것이다.

### 2.3.2 평상시에 프로젝트의 구조에 대해 잘 알아두자

지금은 그렇지 않지만 경력이 1년 미만이었던 시절, 내가 현재 맡은 업무 외의 것들에 대해선 무관심했다. 다른 사람들이 어떠한 업무를 하는지, 개발하면서 어떠한 이슈가 있었는지에 대해 별로 관심이 없었고 잘 듣지도 않았었다. 하지만 다른 사람의 업무에 대한 관심이 개발 산정에 도움이 된다. 왜냐하면 내가 코드를 보지 않아도 그 사람을 통해 코드의 구조가 어느 정도 머릿속에 그림이 그려지기 때문이다. 평상시에 내가 보았던 코드 외의 다른 것들은 어떠한 구조로 개발이 되었는지 전체적인 큰 틀을 아는 것이 개발 기간 산정에 큰 도움이 된다. 아무리 경력이 많은 사람일지라도 프로젝트의 전체적인 구조를 알고 개발하는 사람과 한번도 본 적없는 코드를 보고 개발하는 사람은 천지차이다.

# 정리

개발 기간 산정은 정말로 그저 '감'이다. 그리고 이러한 '감'은 개발해본 경력이 쌓이고 시간이 지나면 해결해 줄 것이다. 하지만 **매일매일 사소한 것 하나에 관심을 갖고, 그것들을 개선해 나가려고 노력한다면** 이러한 '감'을 좀 더 빨리 얻게 되지 않을까?