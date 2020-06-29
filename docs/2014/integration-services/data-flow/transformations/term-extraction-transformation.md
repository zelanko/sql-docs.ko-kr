---
title: 용어 추출 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextractiontrans.f1
helpviewer_keywords:
- word boundaries [Integration Services]
- extracting data [Integration Services]
- sentence boundaries
- word extractions [Integration Services]
- Term Extraction transformation
- tagging words
- normalized data [Integration Services]
- tokenizing text [Integration Services]
- parts of speech [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- stemming words [Integration Services]
ms.assetid: d0821526-1603-4ea6-8322-2d901568fbeb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0e6ab9017c28d722904d4e5efc22652d5b5a65a2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430140"
---
# <a name="term-extraction-transformation"></a>용어 추출 변환
  용어 추출 변환은 변환 입력 열의 텍스트에서 용어를 추출한 후 용어를 변환 출력 열에 기록합니다. 변환은 영어 텍스트에서만 작동되며 자체 영어 사전과 영어에 대한 언어적 정보가 사용됩니다.  
  
 용어 추출 변환을 사용하면 데이터 집합의 내용을 확인할 수 있습니다. 예를 들어 전자 메일 메시지가 포함된 텍스트는 제품에 대한 유용한 피드백을 제공할 수 있으므로 용어 추출 변환을 사용하여 메시지의 주요 내용을 추출하고 고객 의견을 분석할 수 있습니다.  
  
## <a name="extracted-terms-and-data-types"></a>추출된 용어 및 데이터 형식  
 용어 추출 변환에서는 명사 또는 명사구를 따로 추출하거나 모두 추출할 수 있습니다. 명사는 단일 명사이며, 명사구는 하나의 명사와 명사 또는 형용사를 포함하는 두 개 이상의 단어입니다. 예를 들어 명사만 추출하는 옵션이 사용된 경우에는 변환에서 *bicycle* 및 *landscape*등과 같은 용어가 추출되며 명사구 옵션이 사용된 경우에는 *new blue bicycle*, *bicycle helmet*및 *boxed bicycles*와 같은 용어가 추출됩니다.  
  
 관사와 대명사는 추출되지 않습니다. 예를 들어 용어 추출 변환은 *the bicycle* , *my bicycle*및 *that bicycle*에서 *bicycle*을 추출합니다.  
  
 용어 추출 변환은 추출되는 각 용어에 대한 순위를 생성합니다. 순위는 TFIDF 값이나 입력에서 기본 용어가 나타나는 횟수를 의미하는 기본 빈도일 수 있습니다. 어느 경우에도 순위는 0 이상의 실수로 표현됩니다. 예를 들어 TFIDF 순위 값이 0.5이거나 빈도 값이 1.0 또는 2.0일 수 있습니다.  
  
 용어 추출 변환의 출력에는 두 개의 열만 포함됩니다. 한 열에는 추출된 용어가 포함되고 다른 열에는 순위가 포함됩니다. 열의 기본 이름은 **Term** 및 `Score` 입니다. 입력의 텍스트 열에는 여러 용어가 포함될 수 있기 때문에 용어 추출 변환의 출력에는 일반적으로 입력보다 많은 개수의 행이 포함됩니다.  
  
 추출된 용어를 테이블에 기록하는 경우에는 용어 조회, 유사 항목 조회 및 조회 변환과 같은 다른 조회 변환에서 해당 용어를 사용할 수 있습니다.  
  
 용어 추출 변환에서는 데이터 형식이 DT_WSTR 또는 DT_NTEXT인 열의 텍스트만 사용할 수 있습니다. 열에 텍스트가 있지만 데이터 형식이 다른 경우 데이터 변환으로 데이터 흐름에 DT_WSTR 또는 DT_NTEXT 데이터 형식의 열을 추가하고 열 값을 새 열로 복사할 수 있습니다. 그런 다음 데이터 변환의 출력을 용어 추출 변환에 대한 입력으로 사용할 수 있습니다. 자세한 내용은 [Data Conversion Transformation](data-conversion-transformation.md)을 참조하세요.  
  
## <a name="exclusion-terms"></a>제외 용어  
 선택적으로 용어 추출 변환은 데이터 집합에서 용어를 추출할 때 건너뛸 수 있는 용어를 의미하는 제외 용어가 포함된 테이블의 열을 참조할 수 있습니다. 이 기능은 특정 비즈니스 및 분야에서 텍스트에 너무 자주 나와서 쓸모가 없는 단어와 같은 일련의 용어를 중요하지 않은 용어로 이미 정의해 둔 경우에 유용합니다. 예를 들어 특정 상표의 자동차에 대한 고객 지원 정보가 포함된 데이터 집합에서 용어를 추출할 때 해당 상표 이름은 너무 자주 나와서 중요하지 않으므로 제외될 수 있습니다. 따라서 제외 목록의 값은 사용 중인 데이터 집합에 맞게 사용자 지정되어야 합니다.  
  
 제외 목록에 용어를 추가하면 해당 용어를 포함하는 단어나 명사구와 같은 모든 용어도 제외됩니다. 예를 들어 제외 목록에 *data*와 같은 한 단어가 있는 경우 *data*, *data mining*, *data integrity*및 *data validation* 과 같이 이 단어를 포함하는 모든 용어도 제외됩니다. *data*를 포함하는 복합어만 제외하려는 경우에는 제외 목록에 해당 복합 용어를 명시적으로 추가해야 합니다. 예를 들어 *data*항목은 추출하지만 *data validation*은 제외하려는 경우에는 제외 목록에 *data validation* 을 추가하고 제외 목록에서 *data* 가 제거되었는지 확인합니다.  
  
 참조 테이블은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 Access 데이터베이스의 테이블이어야 합니다. 용어 추출 변환은 별개의 OLE DB 연결을 사용하여 참조 테이블에 연결합니다. 자세한 내용은 [OLE DB Connection Manager](../../connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 용어 추출 변환은 완전히 사전 캐시된 모드에서 작동합니다. 용어 추출 변환은 런타임에 참조 테이블로부터 제외 용어를 읽고 변환 입력 행을 처리하기 전에 이를 프라이빗 메모리에 저장합니다.  
  
## <a name="extraction-of-terms-from-text"></a>텍스트에서 용어 추출  
 텍스트에서 용어를 추출하기 위해 용어 추출 변환은 다음과 같은 태스크를 수행합니다.  
  
### <a name="identification-of-words"></a>단어 식별  
 첫째, 용어 추출 변환은 다음 태스크를 수행하여 단어를 구분합니다.  
  
-   공백, 줄 바꿈 및 기타 영어에서 사용되는 단어 종료 문자를 사용하여 텍스트를 여러 단어로 구분합니다. 예를 들어 *?* 및 *:* 과 같은 문장 부호는 단어를 구분하는 문자입니다.  
  
-   하이픈이나 밑줄로 연결된 단어는 그대로 유지합니다. 예를 들어 *copy-protected* 및 *read-only* 와 같은 단어는 한 단어로 유지됩니다.  
  
-   마침표가 포함된 머리 글자어를 그대로 유지합니다. 예를 들어 *A.B.C* Company는 **ABC** 와 **Company**로 토큰화됩니다.  
  
-   특수 문자가 사용된 단어를 분할합니다. 예를 들어 *date/time* 단어는 *date* 와 *time*으로 추출되고, *(bicycle)* 은 *bicycle*로, C#은 C로 취급됩니다. 특수 문자는 삭제되며 단어로 취급될 수 없습니다.  
  
-   아포스트로피와 같이 단어를 분할하지 않는 특수 문자를 인식합니다. 예를 들어 *bicycle's* 는 두 단어로 분할되지 않으며 *bicycle* (명사)라는 단일 용어로 생성됩니다.  
  
-   시간 식, 통화 식, 전자 메일 주소 및 우편 주소를 분할합니다. 예를 들어 *January 31, 2004* 는 *January*, *31*및 *2004*의 3개의 토큰으로 분리됩니다.  
  
### <a name="tagged-words"></a>태그가 지정된 단어  
 둘째, 용어 추출 변환은 다음과 같은 문장 요소 중 하나로 단어를 분류합니다.  
  
-   단수 형태의 명사. 예를 들면 *bicycle* 과 *potato*가 있습니다.  
  
-   복수 형태의 명사. 예를 들면 *bicycles* 와 *potatoes*가 있습니다. 분류되지 않은 모든 복수 명사는 형태소 분석됩니다.  
  
-   단수 형태의 고유 명사. 예를 들면 *April* 과 *Peter*가 있습니다.  
  
-   복수 형태의 고유 명사. 예를 들면 *Aprils* 와 *Peters*가 있습니다. 고유 명사가 형태소 분석되기 위해서는 표준 영어 단어로 제한되는 내부 어휘집에 속해야 합니다.  
  
-   형용사. 예를 들면 *blue*가 있습니다.  
  
-   두 개의 사물을 비교하는 비교 형용사. 예를 들면 *higher* 와 *taller*가 있습니다.  
  
-   적어도 두 개 이상의 사물에 대해 성질이 높거나 낮은 사물을 나타내는 최상급 형용사. 예를 들면 *highest* 와 *tallest*가 있습니다.  
  
-   숫자. 예를 들면 *62* 와 *2004*가 있습니다.  
  
 이러한 문장 요소에 속하지 않는 단어는 삭제됩니다. 예를 들어 동사와 대명사는 삭제됩니다.  
  
> [!NOTE]  
>  문장 요소 분류는 통계 모델을 기반으로 하며 분류는 완전히 정확하지 않을 수 있습니다.  
  
 용어 추출 변환이 명사만 추출하도록 구성된 경우 명사 또는 고유 명사의 단/복수 형태로 분류되는 단어만 추출됩니다.  
  
 용어 추출 변환이 명사구만 추출하도록 구성된 경우 명사, 고유 명사, 형용사 및 숫자로 분류된 단어가 조합되어 명사구가 될 수 있지만 명사구에는 명사 또는 고유 명사의 단/복수 형태로 분류된 단어가 적어도 하나 이상 들어 있어야 합니다. 예를 들어 명사구 *highest mountain* 에는 최상급 형용사로 분류된 단어(*highest*)와 명사로 분류된 단어(*mountain*)가 조합되어 있습니다.  
  
 용어 추출 변환이 명사와 명사구를 모두 추출하도록 구성된 경우 명사에 대한 규칙과 명사구에 대한 규칙이 모두 적용됩니다. 예를 들어 변환에서는 *many beautiful blue bicycles* 라는 텍스트로부터 *bicycle* 및 *beautiful blue bicycle*이 추출됩니다.  
  
> [!NOTE]  
>  추출된 용어는 변환에서 사용되는 최대 용어 길이 및 빈도 임계값에 따라 유지됩니다.  
  
### <a name="stemmed-words"></a>형태소가 분석된 단어  
 용어 추출 변환은 또한 명사를 형태소 분석하여 명사의 단수 형태만 추출합니다. 예를 들어 변환은 *men* 을 *man*으로 추출하고, *mice* 를 *mouse*로, *bicycles* 는 *bicycle*로 추출합니다. 변환은 자체 사전을 사용하여 명사를 형태소 분석합니다. 사전에 표시되지 않은 동명사는 명사로 취급됩니다.  
  
 용어 추출 변환은 용어 추출 변환의 내부 사전을 사용하여 다음과 같이 사전의 단어 형태로 단어를 형태소 분석합니다.  
  
-   명사에서 *s* 를 제거합니다. 예를 들어 *bicycles* 는 *bicycle*이 됩니다.  
  
-   명사에서 *es* 를 제거합니다. 예를 들어 *stories* 는 *story*가 됩니다.  
  
-   불규칙 명사의 경우 사전에서 단수 형태를 검색합니다. 예를 들어 *geese* 는 *goose*가 됩니다.  
  
### <a name="normalized-words"></a>기본 형태로 변환된 단어  
 용어 추출 변환은 문장 내 위치 때문에 대문자로 표기된 용어를 해당 소문자 형태를 사용하여 기본 형태로 바꿉니다. 예를 들어 *Dogs chase cats* 및 *Mountain paths are steep*와 같은 문장에서 *Dogs* 와 *Mountain* 은 *dog* 및 *mountain*의 기본 형태로 바뀝니다.  
  
 용어 추출 변환은 단어를 기본 형태로 바꾸기 때문에 단어의 대/소문자가 달라도 다른 용어로 취급되지 않습니다. 예를 들어 *You see many bicycles in Seattle* 및 *Bicycles are blue*와 같은 텍스트에서 *bicycles* 와 *Bicycles* 는 같은 용어로 인식되고 *bicycle*만 변환에서 유지됩니다. 내부 사전에 나열되지 않은 고유 명사 및 단어는 기본 형태로 바뀌지 않습니다.  
  
### <a name="case-sensitive-normalization"></a>대/소문자를 구분하는 기본 형태  
 용어 추출 변환은 소문자 및 대문자 단어를 각각 고유한 용어로 인식하거나 동일 용어의 다른 표현으로 인식하도록 구성될 수 있습니다.  
  
-   대/소문자를 다르게 인식하도록 변환이 구성된 경우 *Method* 와 *method* 는 두 개의 서로 다른 용어로 추출됩니다. 문장의 첫 번째 단어가 아닌 대문자로 표시된 단어는 기본 형태로 바뀌지 않으며 고유 명사로 분류됩니다.  
  
-   대/소문자를 구분하지 않도록 변환이 구성된 경우 *Method* 및 *method* 와 같은 용어는 단일 용어의 다른 표현으로 인식됩니다. 추출된 용어 목록에는 입력 데이터 집합에서 단어가 표시된 순서에 따라 *Method* 또는 *method*가 포함될 수 있습니다. *Method* 가 문장의 첫 번째 단어이기 때문에 대문자로 표기된 경우에는 기본 형태로 바뀌어서 추출됩니다.  
  
## <a name="sentence-and-word-boundaries"></a>문장 및 단어 경계  
 용어 추출 변환은 다음과 같은 문자를 문장 경계로 사용하여 텍스트를 여러 문장으로 분리합니다.  
  
-   ASCII 줄 바꿈 문자 0x0d(캐리지 리턴) 및 0x0a(줄 바꿈). 이 문자를 문장 경계로 사용하려면 한 행에 두 개 이상의 줄 바꿈 문자가 있어야 합니다.  
  
-   하이픈(-). 이 문자를 문장 경계로 사용하려면 하이픈 왼쪽과 오른쪽의 문자가 모두 글자이면 안 됩니다.  
  
-   밑줄(_). 이 문자를 문장 경계로 사용하려면 하이픈 왼쪽과 오른쪽의 문자가 모두 글자이면 안 됩니다.  
  
-   0x19보다 작거나 같거나 0x7b보다 크거나 같은 모든 유니코드 문자.  
  
-   숫자, 문장 부호 및 영문자 조합. 예를 들어 *A23B#99* 는 용어 *A23B*를 반환합니다.  
  
-   문자,%, @, &, $, #, \* ,:,;,.,, **,** !,?, \<, > , +, =, ^, ~, |, \\ ,/, (,), [,], {,}, ", 및 '가 있습니다.  
  
    > [!NOTE]  
    >  하나 이상의 마침표(.)가 포함된 머리 글자어는 여러 문장으로 분리되지 않습니다.  
  
 그런 다음 용어 추출 변환은 다음과 같은 단어 경계를 사용하여 문장을 여러 단어로 분리합니다.  
  
-   Space  
  
-   탭  
  
-   ASCII 0x0d(캐리지 리턴)  
  
-   ASCII 0x0a(줄 바꿈)  
  
    > [!NOTE]  
    >  *we're* 또는 *it's*와 같이 축약형 단어에 아포스트로피가 사용된 경우에는 단어가 아포스트로피 앞에서 잘리고, 그렇지 않으면 아포스트로피 다음의 문자가 잘립니다. 예를 들어 *we're* 는 *we* 와 *'re*로 분할되고 *bicycle's* 는 *bicycle*로 잘립니다.  
  
## <a name="configuration-of-the-term-extraction-transformation"></a>용어 추출 변환 구성  
 용어 추출 변환은 내부 알고리즘과 통계 모델을 사용하여 결과를 생성합니다. 용어 추출 변환을 여러 번 실행하여 결과를 검토하고 텍스트 마이닝 솔루션에 적합한 결과를 생성하도록 변환을 구성해야 할 수도 있습니다.  
  
 용어 추출 변환에는 하나의 일반 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **용어 추출 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [용어 추출 변환 편집기&#40;용어 추출 탭&#41;](../../term-extraction-transformation-editor-term-extraction-tab.md)  
  
-   [용어 추출 변환 편집기&#40;제외 탭&#41;](../../term-extraction-transformation-editor-exclusion-tab.md)  
  
-   [용어 추출 변환 편집기&#40;고급 탭&#41;](../../term-extraction-transformation-editor-advanced-tab.md)  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
  
