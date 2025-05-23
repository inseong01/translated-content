---
title: CSS 디버깅
slug: Learn_web_development/Core/Styling_basics/Debugging_CSS
original_slug: Learn/CSS/Building_blocks/Debugging_CSS
l10n:
  sourceCommit: 751d58669499de0c6ea0d5b356e0e1448418c5d3
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/CSS/Building_blocks/Styling_tables", "Learn/CSS/Building_blocks/Organizing", "Learn/CSS/Building_blocks")}}

때로는 CSS를 작성할 때 CSS가 예상한 대로 동작하지 않는 문제가 발생합니다. 아마도 특정 선택자가 요소와 일치해야 하지만, 아무 일도 일어나지 않거나 박스의 크기가 예상과 다릅니다. 이 기사에서는 CSS 문제를 디버깅하는 방법에 대한 지침을 제공하고 모든 최신 브라우저에 포함된 개발자 도구가 진행 상황을 찾는 데 어떻게 도움이 되는지 보여줍니다.

<table class="learn-box standard-table">
  <tbody>
    <tr>
      <th scope="row">필요한 사전 지식:</th>
      <td>
        <p>
          기본 컴퓨터 활용 능력,
          <a
            href="https://developer.mozilla.org/ko/Learn/Getting_started_with_the_web/Installing_basic_software"
            >기본 소프트웨어 설치</a
          >,
          <a
            href="https://developer.mozilla.org/ko/Learn/Getting_started_with_the_web/Dealing_with_files"
            >파일 작업</a
          >
          에 대한 기본 지식, HTML 기본 사항 (<a
            href="/ko/docs/Learn/HTML/Introduction_to_HTML"
            >HTML 소개</a
          >
          학습) 및 , CSS 작동 방식 이해 (<a
            href="/ko/docs/Learn/CSS/First_steps"
            >CSS 첫 번째 단계</a
          >
          학습)
        </p>
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        브라우저 개발자 도구의 기본 사항과 CSS의 간단한 검사 및 편집방법 배우기.
      </td>
    </tr>
  </tbody>
</table>

## 브라우저 개발자 도구 사용 방법

[브라우저 개발자 도구란](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools) 기사는 다양한 브라우저 및 플랫폼에서 도구를 사용하는 방법을 설명하는 최신 안내서입니다. 대부분 특정 브라우저에서 개발하도록 선택할 수 있으므로, 해당 브라우저에 포함된 도구에 가장 익숙해지지만, 다른 브라우저에서 해당 도구에 액세스하는 방법을 알아야 합니다. 여러 브라우저 간에 다른 렌더링이 표시되는 경우 도움이 됩니다.

또한 브라우저마다 개발자 도구에서 집중하는 부분이 다르다는 것을 알 수 있습니다. 예를 들어, Firefox에는 CSS 레이아웃으로 시각적으로 작업하기 위한 훌륭한 도구가 있으며, [그리드 레이아웃](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/examine_grid_layouts/index.html), [Flexbox](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/examine_flexbox_layouts/index.html) 및 [Shapes](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/edit_css_shapes/index.html)를 검사하고 편집할 수 있습니다. 그러나, 모든 브라우저마다 유사한 기본 도구가 있습니다. 이러한 기본 도구는 예를 들면 페이지의 요소에 적용된 속성 및 값을 검사하고 편집기에서 변경하는 데 사용됩니다.

이 수업에서는 CSS 작업을 위한 Firefox 개발자 도구의 유용한 기능을 살펴봅니다. 이를 위해 [예제 파일](https://mdn.github.io/css-examples/learn/inspecting/inspecting.html)을 사용하겠습니다. 따라하고 싶다면, 새 탭에 로드하고 위에 링크된 기사에 설명된 대로 개발자 도구를 여세요.

## DOM vs 소스 보기

새로운 사용자가 개발자 도구에서 혼동할 수 있는 것은 웹 페이지의 [소스 보기](https://firefox-source-docs.mozilla.org/devtools-user/view_source/index.html) 를 보거나 서버에 넣은 HTML 파일을 볼 때 표시되는 것과 개발자 도구의 [HTML 창](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/ui_tour/index.html#html_pane)에서 보이는 것의 차이입니다. 소스 보기를 통해 볼 수 있는 것과 거의 비슷해 보이지만 몇 가지 차이점이 있습니다.

렌더링 된 DOM에서 브라우저가 잘못 작성된 HTML을 수정했을 수 있습니다. `<h2>`를 열고 `</h3>`로 닫는 등의 요소를 잘못 닫은 경우, 브라우저는 수행하려는 작업을 파악하고 DOM의 HTML은 `<h2>`를 `</h2>`로 올바르게 닫습니다. 또한 브라우저에서는 모든 HTML을 표준화하고, DOM은 JavaScript로 변경한 내용도 표시합니다.

소스 보기는 서버에 저장된 HTML 소스 코드입니다. 개발자 도구의 [HTML tree](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/examine_and_edit_html/index.html#html_tree)는 특정 시점에 브라우저가 렌더링하는 내용을 정확하게 보여주므로, 실제로 어떤 일이 일어나고 있는지 파악할 수 있습니다.

## 적용된 CSS 검사

페이지에서 요소를 마우스 오른쪽/ctrl 키를 누른 채 클릭하고 **검사(Inspect)** 를 선택하거나, 개발자 도구 디스플레이 왼쪽의 HTML tree에서 요소를 선택하세요. `box1` 클래스의 요소를 선택하세요. 이것은 테두리 박스가 그려진 페이지의 첫 번째 요소입니다.

![개발자 도구가 열려 있는 이 튜토리얼의 예제 페이지](inspecting1.png)

HTML 오른쪽의 [Rules view](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/ui_tour/index.html#rules_view)를 보면 해당 요소에 적용된 CSS 속성과 값을 볼 수 있습니다. `box1` 클래스에 직접 적용된 규칙과 상자가 조상으로부터 상속받은 CSS(이 경우 `<body>`)를 볼 수 있습니다. 이것은 예상하지 못한 일부 CSS가 적용되는 경우에 유용합니다. 아마도 부모 요소에서 상속되고 있고 이 요소의 컨텍스트에서 덮어쓰는 규칙을 추가해야 합니다.

또한 단축 속성을 확장하는 기능도 유용합니다. 이 예에서는 `margin` 단축 속성이 사용되었습니다.

**보기를 확장하려면 작은 화살표를 클릭하여 다양한 속성과 해당 값을 표시합니다.**

**해당 패널이 활성 상태일 때 규칙 보기에서 값을 켜고 끌 수 있습니다. 이 패널 위에 마우스를 가져가면 확인란이 나타납니다. `border-radius`와 같은 규칙의 확인란을 선택 취소하면 CSS가 적용을 중지합니다.**

예를 들어 레이아웃이 잘못되어 어떤 속성이 문제일 때 이것을 사용하여 A/B 비교를 수행하여 규칙을 적용했을 때 더 나은지 여부를 결정하고 디버그에 도움을 줄 수 있습니다.

다음 비디오는 Firefox 개발자 도구를 사용하여 CSS를 디버그하는 데 유용한 팁을 제공합니다.

{{EmbedYouTube("O3DAm82vIvU")}}

## 값 편집

속성을 켜고 끄는 것 외에도 해당 값을 편집할 수 있습니다. 다른 색상이 더 잘 보이는지 확인하고 싶거나 크기를 조정하고 싶으신가요? 개발자 도구를 사용하면 스타일시트를 편집하고 페이지를 다시 로드하는 데 많은 시간을 절약할 수 있습니다.

**`box1`을 선택한 상태에서 테두리에 적용된 색상을 표시하는 견본(색상이 지정된 작은 원)을 클릭합니다. 색상 선택자가 열리고 몇 가지 다른 색상을 시도할 수 있습니다. 페이지에서 실시간으로 업데이트됩니다. 비슷한 방식으로 테두리의 너비나 스타일을 변경할 수 있습니다.**

![색상 선택자가 열린 개발자 도구](inspecting2-color-picker.png)

## 새 속성 추가

개발자 도구를 사용하여 속성을 추가할 수 있습니다. 상자가 `<body>` 요소의 글꼴 크기를 상속하는 것을 원하지 않고 고유한 특정 크기를 설정하기를 원하시나요? CSS 파일에 추가하기 전에 개발자 도구에서 시도할 수 있습니다.

**규칙에서 닫는 중괄호를 클릭하여 새 선언 입력을 시작할 수 있습니다. 이 시점에서 새 속성 입력을 시작할 수 있으며 개발자 도구는 일치하는 속성의 자동 완성 목록을 표시합니다. `font-size`를 선택한 후 시도하려는 값을 입력합니다. + 버튼을 클릭하여 동일한 선택자로 규칙을 추가하고 거기에 새 규칙을 추가할 수도 있습니다.**

![개발자 도구 패널, 규칙에 새 속성을 추가하고, 폰트 자동 완성을 열고 있습니다.](inspecting3-font-size.png)

> [!NOTE]
> 규칙 보기에는 다른 유용한 기능도 있습니다. 예를 들어 유효하지 않은 값이 있는 선언에는 줄이 그어 표시됩니다. 자세한 내용은 [CSS 검사 및 수정](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/examine_and_edit_css/index.html)에서 확인할 수 있습니다.

## 박스 모델 이해

이전 강의에서 [박스 모델](/ko/docs/Learn_web_development/Core/Styling_basics/Box_model)과 변경되는 대체 박스 모델이 있다는 사실에 대해 논의했습니다. 요소의 크기가 요소에 제공한 크기와 패딩 및 테두리를 기반으로 계산되는 방식입니다. 개발자 도구는 요소의 크기가 어떻게 계산되는지 이해하는 데 실제로 도움이 될 수 있습니다.

[레이아웃 보기](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/ui_tour/index.html#layout_view)는 선택한 요소의 박스 모델 다이어그램과 함께 요소가 배치되는 방식을 변경하는 속성 및 값에 대한 설명이 표시됩니다. 여기에는 요소에 명시적으로 사용하지 않았지만, 초기 값이 설정된 속성에 대한 설명이 포함됩니다.

이 패널에서 세부 속성 중 하나는 요소가 사용하는 박스 모델을 제어하는 `box-sizing` 속성입니다.

**`box1` 및 `box2` 클래스가 있는 두 상자를 비교합니다. 둘 다 동일한 너비(400px)가 적용되지만 `box1`이 시각적으로 더 넓습니다. 레이아웃 패널에서 `content-box`를 사용하고 있는 것을 볼 수 있습니다. 이것은 요소에 지정한 크기에 패딩 및 테두리 너비를 추가하는 값입니다.**

`box2` 클래스가 있는 요소는 `border-box`를 사용하므로 여기에서 요소에 지정한 크기에서 패딩과 테두리를 뺍니다. 즉, 상자가 페이지에서 차지하는 공간이 지정한 정확한 크기(이 경우 `width: 400px`)입니다.

![개발자 도구의 레이아웃 섹션](inspecting4-box-model.png)

> **참고:** [박스 모델 검사](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/examine_and_edit_the_box_model/index.html)에서 자세히 알아보십시오.

## 특이성 문제 해결

개발 중에, 특히 기존 사이트에서 CSS를 편집해야 하는 경우 일부 CSS를 적용하는 데 어려움을 겪을 수 있습니다. 무엇을 하든지 요소는 CSS를 사용하지 않는 것 같습니다. 여기에서 일반적으로 발생하는 것은 보다 구체적인 선택자가 변경 사항을 재정의한다는 것입니다. 여기서 개발자 도구가 정말 도움이 될 것입니다.

예제 파일에는 `<em>` 요소로 래핑된 두 단어가 있습니다. 하나는 주황색으로 표시되고 다른 하나는 핫핑크로 표시됩니다. 우리가 적용한 CSS는 다음과 같습니다.

```css
em {
  color: hotpink;
  font-weight: bold;
}
```

스타일시트의 그 위에는 `.special` 선택자가 있는 규칙이 있습니다.

```css
.special {
  color: orange;
}
```

특이성에 대해 논의한 [캐스케이드 및 상속](/ko/docs/Learn_web_development/Core/Styling_basics/Handling_conflicts) 강의에서 기억하시겠지만, 클래스 선택자는 요소 선택자보다 더 구체적입니다. 따라서 클래스 선택자가 적용됩니다. 개발자 도구는 특히 정보가 거대한 스타일시트의 어딘가에 묻혀 있는 경우 이러한 문제를 찾는 데 도움이 될 수 있습니다.

**`.special` 클래스로 `<em>`을 검사하면 개발자 도구에서 주황색이 적용되는 색상임을 보여주고 또한 em에 적용된 `color` 속성은 그어진 선으로 표시됩니다. 이제 클래스가 요소 선택자를 재정의하는 것을 볼 수 있습니다.**

![em을 선택하고 개발자 도구에서 색상을 재정의](inspecting5-specificity.png)

## Firefox 개발자 도구에 대해 자세히 알아보기

여기 MDN에 Firefox 개발자 도구에 대한 많은 정보가 있습니다. 주요 [개발자 도구 섹션](https://firefox-source-docs.mozilla.org/devtools-user/index.html)을 살펴보고 이 강의에서 간략하게 다룬 내용에 대한 자세한 내용은 [방법 안내](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/index.html#how-to)를 참조하세요.

## CSS의 디버깅 문제

개발자 도구는 CSS 문제를 해결할 때 큰 도움이 될 수 있으므로 CSS가 예상대로 작동하지 않는 상황에 처했을 때 어떻게 해결해야 할까요? 다음 단계가 도움이 될 것입니다.

### 문제에서 한발 물러나서

코딩 문제, 특히 CSS 문제는 좌절감을 줄 수 있습니다. 솔루션을 찾는 데 도움이 되는 온라인 검색 오류 메시지가 표시되지 않는 경우가 많기 때문입니다. 답답해지면 잠시 문제에서 한 발짝 떨어져 보세요. 산책을 하거나, 술을 마시거나, 동료와 이야기를 나누거나, 잠시 동안 다른 일을 해보세요. 문제에 대한 생각을 멈추면 솔루션이 마술처럼 나타나는 경우가 있고, 그렇지 않더라도 기분이 상쾌할 때 작업하기가 훨씬 수월합니다.

### 유효한 HTML과 CSS가 있습니까?

브라우저는 CSS와 HTML이 올바르게 작성되기를 기대하지만, 브라우저도 매우 관대하며 마크업이나 스타일시트에 오류가 있는 경우에도 웹페이지를 표시하기 위해 최선을 다할 것입니다. 코드에 실수가 있는 경우 브라우저는 의도한 바를 추측해야 하며 사용자가 염두에 둔 것과 다른 결정을 내릴 수 있습니다. 또한 두 가지 다른 브라우저가 두 가지 다른 방법으로 문제에 대처할 수 있습니다. 따라서 좋은 첫 번째 단계는 유효성 검사기를 통해 HTML 및 CSS를 실행하여 오류를 찾아 수정하는 것입니다.

- [CSS Validator](https://jigsaw.w3.org/css-validator/)
- [HTML validator](https://validator.w3.org/)

### 테스트 중인 브라우저에서 속성과 값을 지원하나요?

브라우저는 이해하지 못하는 CSS를 무시합니다. 사용 중인 속성이나 값이 테스트 중인 브라우저에서 지원되지 않으면 아무것도 중단되지 않지만, 해당 CSS는 적용되지 않습니다. 개발자 도구는 일반적으로 어떤 방식으로든 지원되지 않는 속성과 값을 강조 표시합니다. 아래 스크린샷에서 브라우저는 {{cssxref("grid-template-columns")}}의 하위 그리드 값을 지원하지 않습니다.

![grid-template-columns: subgrid 값이 지원되지 않아 subgrid가 제외된 브라우저 개발자 도구의 이미지](no-support.png)

또한 MDN의 각 속성 페이지 하단에 있는 브라우저 호환성 표를 볼 수 있습니다. 이것들은 해당 속성에 대한 브라우저 지원을 보여주며, 속성의 일부 사용에 대한 지원이 있고 다른 것은 지원하지 않는 경우 종종 세분화됩니다. [`shape-outside` 속성의 호환성 표를 참조하세요](/ko/docs/Web/CSS/shape-outside#browser_compatibility).

### 다른 요소가 CSS를 재정의하고 있나요?

여기서 특이성에 대해 배운 정보가 매우 유용할 것입니다. 당신이 하려고 하는 것을 재정의하는 더 구체적인 무언가가 있다면, 당신은 무엇을 하려고 하는지 알아내려는 매우 좌절감을 주는 게임에 빠질 수 있습니다. 그러나 위에서 설명한 대로, 개발자 도구는 적용되는 CSS를 보여주며, 새 선택자를 충분히 구체적으로 만들어 재정의할 수 있도록 할 수 있습니다.

### 문제의 축소된 테스트 사례 만들기

위 단계를 수행해도 문제가 해결되지 않으면 추가 조사가 필요합니다. 이 시점에서 가장 좋은 것은 축소된 테스트 케이스로 알려진 것을 만드는 것입니다. "문제를 줄인다"는 것은 정말 유용한 기술입니다. 자신과 동료의 코드에서 문제를 찾는 데 도움이 되며 버그를 보고하고 더 효과적으로 도움을 요청할 수 있습니다.

축소된 테스트 사례는 관련 없는 주변 콘텐츠와 스타일이 제거된 가장 간단한 방법으로 문제를 보여주는 코드 예제입니다. 이는 종종 레이아웃에서 문제가 있는 코드를 제거하여 해당 코드나 기능만 보여주는 작은 예제를 만드는 것을 의미합니다.

축소된 테스트 케이스를 만드는 방법은 다음과 같습니다.

1. 마크업이 동적으로 생성되는 경우(예: CMS를 통해) 문제를 보여주는 출력의 정적 버전을 만드세요. [CodePen](https://codepen.io/)과 같은 코드 공유 사이트는 축소된 테스트 사례를 호스팅하는 데 유용합니다. 그러면 온라인에서 액세스할 수 있고 동료와 쉽게 공유할 수 있기 때문입니다. 페이지에서 소스 보기를 수행하고 HTML을 CodePen에 복사한 다음 관련 CSS 및 JavaScript를 가져와서 포함할 수 있습니다. 그 후에도 문제가 여전히 분명한지 확인할 수 있습니다.
2. JavaScript를 제거해도 문제가 해결되지 않으면 JavaScript를 포함하지 마세요. JavaScript를 제거해도 문제가 _해결되지 않는_ 경우 가능한 한 많은 JavaScript를 제거하고 문제의 원인은 그대로 두세요.
3. 문제의 원인이 되지 않는 HTML을 제거하세요. 구성 요소 또는 레이아웃의 주요 요소를 제거합니다. 다시 말하지만, 여전히 문제를 보여주는 가장 작은 양의 코드를 찾아보세요.
4. 문제에 영향을 주지 않는 CSS를 제거하세요.

이 작업을 수행하는 과정에서 문제의 원인을 발견하거나 최소한 특정 항목을 제거하여 문제를 켜고 끌 수 있습니다. 무언가를 발견할 때 코드에 몇 가지 주석을 추가할 가치가 있습니다. 도움을 요청해야 하는 경우 이미 시도한 내용을 도움을 주는 사람에게 보여줄 것입니다. 이렇게 하면 들리는 문제와 해결 방법을 검색할 수 있는 충분한 정보를 얻을 수 있습니다.

여전히 문제를 해결하는 데 어려움을 겪고 있다면 테스트 케이스를 축소하여 포럼에 게시하거나 동료에게 보여줌으로써 도움을 요청할 수 있습니다. 도움을 요청하기 전에 문제를 줄이고, 문제가 발생한 위치를 정확히 식별하는 작업을 완료했음을 보여줄 수 있다면 도움을 받을 가능성이 훨씬 더 높습니다. 경험이 더 많은 개발자는 문제를 신속하게 찾아내고 올바른 방향으로 안내할 수 있으며, 그렇지 않더라도 축소된 테스트 사례를 통해 빠르게 살펴보고 최소한 도움을 줄 수 있을 것입니다.

문제가 실제로 브라우저의 버그인 경우 축소된 테스트 사례를 사용하여 관련 브라우저 공급업체에 버그 보고서를 제출할 수도 있습니다(예: Mozilla의 [bugzilla 사이트](https://bugzilla.mozilla.org)).

CSS에 대한 경험이 많을수록 문제를 더 빨리 파악하게 될 것입니다. 그러나 우리 중 가장 경험이 많은 사람들조차도 때때로 도대체 무슨 일이 일어나고 있는지 궁금해합니다. 체계적인 접근 방식을 취하고 축소된 테스트 사례를 만들고 다른 사람에게 문제를 설명하면 일반적으로 수정 사항을 찾을 수 있습니다.

## 요약

이렇게 CSS 디버깅에 대한 소개를 마쳤습니다. 이를 통해 나중에 당신의 경력에서 CSS 및 다른 유형의 코드를 디버깅할 때 유용한 기술을 얻을 수 있습니다.

이 과정의 마지막 글에서는 [CSS를 구성하는 방법](/ko/docs/Learn_web_development/Core/Styling_basics/Organizing)을 살펴보겠습니다.

{{PreviousMenuNext("Learn/CSS/Building_blocks/Styling_tables", "Learn/CSS/Building_blocks/Organizing", "Learn/CSS/Building_blocks")}}
