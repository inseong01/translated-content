---
title: CSS 레이아웃
slug: Learn_web_development/Core/CSS_layout
original_slug: Learn/CSS/CSS_layout
l10n:
  sourceCommit: 45268b07c84a04b45d46bcdf104e2b33be00adcf
---

{{LearnSidebar}}

이 시점에서 우리는 이미 CSS 기본 사항, 텍스트 스타일 지정 방법, 콘텐츠가 들어 있는 박스의 스타일을 지정하고 조작하는 방법을 살펴보았습니다. 이제 뷰포트와 관련하여 박스를 올바른 장소에 배치하는 방법을 살펴볼 차례입니다. 우리는 필수 전제조건을 이미 다루었기 때문에 이제 다양한 디스플레이 설정, 포지셔닝, 플렉스박스 및 CSS 그리드와 같은 최신 레이아웃 도구, 그리고 당신이 여전히 알고 싶어 할 만한 레거시 기술들을 살펴보며 CSS 레이아웃에 대해 자세히 알아보겠습니다.

## 선결사항

이번 과정을 시작하기 전에, 여러분은 이미 아래 내용을 알고 있어야 합니다.

1. [HTML 소개](/ko/docs/conflicting/Learn_web_development/Core/Structuring_content) 과정에서 논의했듯이 HTML에 대해 기본적인 친숙도가 있어야 합니다.
2. [CSS 소개](/ko/docs/conflicting/Learn_web_development/Core/Styling_basics) 과정에서 논의한 대로 CSS 기본 사항에 대해 익숙해야 합니다.
3. [박스 스타일 지정](/ko/docs/Learn_web_development/Core/Styling_basics) 방법에 대한 이해가 있어야 합니다.

> [!NOTE]
> 직접 파일을 생성할 수 없는 컴퓨터/태블릿/기타 장치에서 작업하고 있는 경우, [JSBin](https://jsbin.com/)나 [Glitch](https://glitch.com/)과 같은 온라인 코딩 프로그램에서 코드 예제를 시험해 볼 수 있습니다.

## 안내서

이 글은 CSS에서 이용할 수 있는 기본 레이아웃 도구 및 기술에 대한 지침을 제공합니다. 과정 말미에는 웹페이지를 레이아웃하여 레이아웃 메서드에 대한 이해도를 확인할 수 있는 평가가 있습니다.

- [CSS 레이아웃 입문서](/ko/docs/Learn_web_development/Core/CSS_layout/Introduction)
  - 이 문서에서는 이전 과정에서 이미 다뤘던 CSS 레이아웃 기능, 예를 들어 다양한 {{cssxref("display")}} 속성값의 차이 등을 복습하고, 이번 과정에서 다룰 예정인 몇몇 CSS 개념을 소개합니다.
- [일반 흐름](/ko/docs/conflicting/Learn_web_development/Core/CSS_layout/Introduction)
  - 웹페이지의 요소 무리는 여러분이 무언가 변화를 주기전까지는 _normal flow_(일반 흐름)에 따라 요소들을 배치합니다. 이 문서에서는 일반 흐름을 변경하는 방법을 배우기 위한 기초로서 일반 흐름의 기본을 설명합니다.
- [플렉스박스(Flexbox)](/ko/docs/Learn_web_development/Core/CSS_layout/Flexbox)
  - [플렉스박스](/ko/docs/Web/CSS/CSS_Flexible_Box_Layout/%EA%B0%80%EB%B3%80%EC%83%81%EC%9E%90%EC%9D%98_%EB%8C%80%ED%91%9C%EC%A0%81%EC%9D%B8_%EC%82%AC%EC%9A%A9%EB%A1%80)는 행이나 열로 배치하는 1차원 레이아웃 메서드입니다. 항목은 좁은 공간에 맞게 축소되거나, 여분의 공간을 채우기 위해 변형됩니다. 이 문서에서는 모든 기본 사항을 설명합니다. 이 안내서를 공부한 후 [플렉스박스 기술을 테스트](/ko/docs/Learn/CSS/CSS_layout/Flexbox_skills)하여 이해도를 확인한 후 계속 진행할 수 있습니다.
- [그리드(Grids)](/ko/docs/Learn_web_development/Core/CSS_layout/Grids)
  - CSS 그리드 레이아웃(Grid Layout)은 웹페이지를 위한 2차원 레이아웃 시스템입니다. 이 기능을 통해 콘텐츠를 행과 열로 배치할 수 있으며, 복잡한 레이아웃을 간단하게 구축할 수 있는 많은 기능이 있습니다. 이 문서에서는 페이지 레이아웃을 시작하기 위해 필요한 모든 것을 설명합니다. 이 안내서를 공부한 후 [그리드 기술을 테스트](/ko/docs/Learn/CSS/CSS_layout/Grid_skills)해 볼 수 있습니다.
- [플로트(Floats)](/ko/docs/Learn_web_development/Core/CSS_layout/Floats)
  - 원래 텍스트 블록 안에 플로팅 이미지를 넣기 위해 사용되던 {{cssxref("float")}} 속성은 웹 페이지에서 다단 레이아웃을 생성할 용도로 가장 일반적으로 사용되는 도구 중 하나로 자리매김했었습니다. 플렉스박스와 그리드의 등장으로 플로트 속성은 원래의 용도로 돌아갔습니다.
- [포지셔닝(Positioning)](/ko/docs/Learn_web_development/Core/CSS_layout/Positioning)
  - 포지셔닝을 사용하면 요소를 일반적인 문서 레이아웃 흐름에서 벗어나, 요소 위에 배치하거나, 뷰포트 내부에서 항상 같은 위치에 있는 등 다르게 동작하도록 할 수 있습니다. 이 문서에서는 다양한 {{cssxref("position")}} 값을 설명하고, 그 사용법에 대해 설명합니다.
- [다단 레이아웃](/ko/docs/Learn_web_development/Core/CSS_layout/Multiple-column_Layout)
  - CSS 다단 레이아웃 규격은 신문에서 볼 수 있듯이 콘텐츠를 단으로 배치하는 방법을 제공합니다. 이 문서에서는 이 기능을 어떻게 사용하는지 설명합니다.
- [반응형 디자인](/ko/docs/Learn/CSS/CSS_layout/%EB%B0%98%EC%9D%91%ED%98%95_%EB%94%94%EC%9E%90%EC%9D%B8)
  - 웹 기반 장치에 다양한 화면 크기가 등장함에 따라 반응형 웹 디자인(RWD) 개념이 등장했습니다. 이것은 다양한 화면 너비와 해상도 등에 맞게 웹 페이지가 레이아웃과 모양을 변경할 수 있는 일련의 관행입니다. 이는 멀티 디바이스 웹을 위한 디자인 방식을 바꾼 아이디어로, 이 문서에서는 그 내용을 숙달하기 위해 알아야 하는 주요 기술을 이해하도록 도울 것입니다.
- [미디어 쿼리 초보자 안내서](/ko/docs/Learn_web_development/Core/CSS_layout/Media_queries)
  - **CSS Media Query**는 예를 들어 "뷰포트가 480 픽셀보다 넓다."라고 여러분이 지정한 규칙에 브라우저 및 장치 환경이 일치하는 경우에만 CSS를 적용할 수 있는 방법을 제공합니다. 미디어 쿼리는 반응형 웹 디자인의 핵심 요소입니다. 뷰포트의 크기에 따라 서로 다른 레이아웃을 생성할 수 있기 때문입니다. 또한 사용자가 마우스가 아닌 터치스크린을 사용하는지 여부와 같이 실행 중인 사이트 환경의 여러 내용들을 감지하는 데도 사용할 수 있습니다. 이번 과정에서는 먼저 미디어 쿼리에 사용되는 구문에 대해 배우고, 간단한 디자인을 반응형으로 만드는 방법을 보여주는 예제를 살펴보겠습니다.
- [레거시 레이아웃 메서드](/ko/docs/Learn_web_development/Core/CSS_layout/Legacy_Layout_Methods)
  - 그리드 시스템은 CSS 레이아웃에서 사용되는 매우 일반적인 기능이며, CSS 그리드 레이아웃(Grid Layout) 이전에는 플로트(Floats) 또는 기타 레이아웃 기능을 이용하여 그리드 레이아웃(Grid Layout)을 구현하는 경향이 있었습니다. 먼저 레이아웃을 정해진 수의 열(예를 들어 4, 6 또는 12열)이라 상상한 뒤, 여러분의 콘텐츠를 그 가상의 열 안에 콘텐츠 열을 끼워 맞추는 방식이었습니다. 이 글에서 이 오래된 메서드가 어떻게 작동하는지 탐구할 것입니다. 이는 여러분이 오래된 프로젝트에 몸을 담게 될 경우에 그 메서드의 사용 방법에 대한 이해를 돕기 위함입니다.
- [이전 브라우저 지원](/ko/docs/Learn/CSS/CSS_layout/%EC%9D%B4%EC%A0%84_%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80_%EC%A7%80%EC%9B%90)
  - 이 과정에서는 플렉스박스 및 그리드를 웹디자인을 위한 주 레이아웃 방법으로 사용할 것을 권장합니다. 그러나 이전 브라우저 또는 당신이 사용하는 메서드를 지원하지 않는 브라우저를 사용하는 사이트 방문자가 있을 수 있습니다. 이런 일은 웹상에서 항상 있는 일입니다. 즉 새로운 기능이 개발됨에 따라 브라우저마다 다른 기능의 우선순위를 정하기 때문에 발생합니다. 이 문서에서는 이전 기술의 사용자들을 배제하지 않고 현대적인 웹 기술을 사용하는 방법에 대해 설명합니다.

## 평가

다음 평가는 위 가이드에서 다룬 CSS 레이아웃 방법에 대한 이해도를 테스트합니다.

- [레이아웃 이해의 핵심 사항](/ko/docs/Learn_web_development/Core/CSS_layout/Fundamental_Layout_Comprehension)
  - 웹페이지를 레이아웃하여 다양한 레이아웃 방법에 대한 지식을 테스트하는 평가입니다.

## 같이 보기

- [포지셔닝 실례](/ko/docs/Learn/CSS/CSS_layout/Practical_positioning_examples)
  - : 이 문서에서는 포지셔닝으로 어떤 작업을 수행할 수 있는지 설명하기 위해 몇 가지 실제 사례를 구축하는 방법을 보여줍니다.
- [CSS 레이아웃 안내서](/ko/docs/Web/CSS/Layout_cookbook)
  - : CSS 레이아웃 안내서(cookbook)는 사이트에 구현해야 할 수 있는 일반적인 레이아웃 패턴에 대한 레시피를 한데 모으는 것을 목표로 합니다. 이 레시피는 프로젝트의 시작점으로 사용할 수 있는 코드를 제공할 뿐만 아니라 레이아웃 사양을 사용할 수 있는 다양한 방법과 개발자로서의 선택 사항을 강조합니다.
