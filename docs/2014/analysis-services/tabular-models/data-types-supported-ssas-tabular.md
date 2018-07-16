---
title: 데이터 형식 지원 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57bf1633f05f9692c3e5cc132bce6585734830a4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237633"
---
# <a name="data-types-supported-ssas-tabular"></a>지원되는 데이터 형식(SSAS 테이블 형식)
  이 문서에서는 테이블 형식 모델에서 사용할 수 있는 데이터 형식에 대해 설명하고 DAX(Data Analysis Expressions) 수식에서 데이터를 계산하거나 사용할 때 암시적으로 수행되는 데이터 형식 변환에 대해 설명합니다.  
  
 이 문서에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [테이블 형식 모델에 사용되는 데이터 형식](#bkmk_data_types)  
  
-   [DAX 수식의 명시적 및 암시적 데이터 형식 변환](#bkmk_implicit)  
  
-   [공백, 빈 문자열 및 0 값 처리](#bkmk_hand_blanks)  
  
##  <a name="bkmk_data_types"></a> 테이블 형식 모델에 사용되는 데이터 형식  
 다음과 같은 데이터 형식이 지원됩니다. 수식에서 데이터를 가져오거나 값을 사용하는 경우 원래 데이터 원본에 다른 데이터 형식이 포함되어 있더라도 다음 데이터 형식 중 하나로 데이터가 변환됩니다. 수식의 결과 값도 이러한 데이터 형식을 사용합니다.  
  
 일반적으로 이러한 데이터 형식은 계산 열의 정확한 계산을 위해 구현되며 일관성을 위해 모델의 나머지 데이터에도 동일한 제한이 적용됩니다.  
  
 숫자, 통화, 날짜 및 시간에 사용되는 서식은 모델 데이터로 작업하는 데 사용된 클라이언트에서 지정한 로캘의 서식을 따라야 합니다. 모델에서 서식 옵션을 사용하여 값이 표시되는 방식을 제어할 수 있습니다.  
  
||||  
|-|-|-|  
|모델의 데이터 형식|DAX의 데이터 형식|Description|  
|정수|64비트(8바이트) 정수 값 <sup>1, 2</sup>|소수 자릿수가 없는 숫자입니다. 정수는 양수나 음수가 될 수 있지만 -9,223,372,036,854,775,808(-2^63)부터 9,223,372,036,854,775,807(2^63-1) 사이의 정수여야 합니다.|  
|10진수|64비트(8바이트) 실수 <sup>1, 2</sup>|실수는 소수 자리를 가질 수 있는 수입니다. 실수는 광범위한 값을 포함합니다.<br /><br /> -1.79E +308에서 -2.23E -308 사이의 음수 값<br /><br /> 0<br /><br /> 2.23E -308에서 1.79E + 308 사이의 양수 값<br /><br /> 하지만 유효 숫자 수는 열일곱 자릿수로 제한됩니다.|  
|Boolean|Boolean|True 또는 False 값입니다.|  
|텍스트 모드|String|유니코드 문자 데이터 문자열입니다. 텍스트 형식으로 표시된 문자열, 숫자 또는 날짜가 될 수 있습니다.|  
|Date|날짜/시간|허용되는 날짜-시간 표현의 날짜 및 시간<br /><br /> 유효한 날짜는 1900년 3월 1일 이후의 모든 날짜입니다.|  
|Currency|Currency|통화 데이터 형식에는 -922,337,203,685,477.5808부터 922,337,203,685,477.5807 사이의 소수 자릿수가 고정된 네 자릿수를 사용할 수 있습니다.|  
|해당 사항 없음|공백|공백은 SQL null을 나타내거나 대체하는 DAX의 데이터 형식입니다. BLANK 함수를 사용하여 공백을 만들고 논리 함수 ISBLANK를 사용하여 공백을 테스트할 수 있습니다.|  
  
 <sup>1</sup> DAX 수식은 테이블에 나열 된 것 보다 작은 데이터 형식을 지원 하지 않습니다.  
  
 <sup>2</sup> 매우 큰 숫자 값이 포함 된 데이터를 가져오려고 하면 다음 오류로 인해 가져오기가 실패할 수 있습니다.  
  
 메모리 내 데이터베이스 오류:는 '\<열 이름 >'의 열은 '\<테이블 이름 >' 테이블에 값이 있는 ' 1.7976931348623157 e + 308'는 지원 되지 않습니다. 작업이 취소되었습니다.  
  
 이 오류는 모델 디자이너에서 해당 값을 사용하여 null을 나타내기 때문에 발생합니다. 다음 목록의 값은 앞에서 말한 null 값과 동의어입니다.  
  
||  
|-|  
|값|  
|9223372036854775807|  
|-9223372036854775808|  
|1.7976931348623158e+308|  
|2.2250738585072014e-308|  
  
 데이터에서 값을 제거한 후 다시 가져와야 합니다.  
  
> [!NOTE]  
>  131,072자가 넘는 문자열이 포함된 **varchar(max)** 열에서는 가져올 수 없습니다.  
  
### <a name="table-data-type"></a>테이블 데이터 형식  
 또한 DAX에서는 *table* 데이터 형식도 사용합니다. 이 데이터 형식은 DAX에서 집계 및 시간 인텔리전스 계산과 같은 여러 함수에 사용됩니다. 일부 함수에는 테이블에 대한 참조가 필요하고 일부 함수는 다른 함수의 입력으로 사용할 수 있는 테이블을 반환합니다. 테이블을 입력으로 사용해야 하는 일부 함수에서는 테이블로 계산되는 식을 지정할 수 있고 일부 함수에는 기본 테이블에 대한 참조가 필요합니다. 특정 함수에 대한 요구 사항은 [DAX 함수 참조](https://msdn.microsoft.com/library/ee634396.aspx)를 참조하십시오.  
  
##  <a name="bkmk_implicit"></a> DAX 수식의 명시적 및 암시적 데이터 형식 변환  
 각 DAX 함수에는 입력 및 출력으로 사용되는 데이터 형식과 관련된 특정 요구 사항이 있습니다. 예를 들어 정수와 날짜를 인수로 사용해야 하는 함수도 있고 텍스트 또는 테이블을 인수로 사용해야 하는 함수도 있습니다.  
  
 인수로 지정하는 열의 데이터가 함수에 필요한 데이터 형식과 호환되지 않는 경우 대부분 오류가 반환됩니다. 그러나 가능한 경우 항상 DAX에서는 데이터를 필요한 데이터 형식으로 암시적으로 변환하려고 시도합니다. 예를 들어:  
  
-   숫자(예: "123")를 문자열로 입력할 수 있습니다. DAX에서 문자열을 구문 분석하여 숫자 데이터 형식으로 지정하려고 합니다.  
  
-   TRUE + 1을 추가하여 2라는 결과를 얻을 수 있습니다. TRUE가 암시적으로 숫자 1로 변환되어 1+1 연산이 수행되기 때문입니다.  
  
-   두 열의 값을 더할 때 한 값은 텍스트("12")로 표시되고 다른 값은 숫자(12)로 표시된 경우 DAX에서 암시적으로 문자열을 숫자로 변환한 다음 더하여 숫자 결과를 반환합니다. 다음 식은 44: = "22" + 22를 반환합니다.  
  
-   두 숫자를 연결하려고 하면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 추가 기능에서 두 수를 문자열로 표시한 다음 연결합니다. 다음 식은 "1234": = 12 & 34를 반환합니다.  
  
 다음 표에는 수식에서 수행되는 암시적 데이터 형식 변환이 요약되어 있습니다. 일반적으로 의미 체계 모델 디자이너는 Microsoft Excel처럼 작동하며 지정된 작업에 필요한 경우 가능하면 항상 암시적 변환을 수행합니다.  
  
### <a name="table-of-implicit-data-conversions"></a>암시적 데이터 변환에 대한 표  
 요청된 연산을 수행하기 전에 필요한 값을 캐스팅하는 연산자에 의해 수행되는 변환 유형이 결정됩니다. 다음 표에서는 연산자를 나열하고 교차 행의 데이터 형식과 함께 사용되는 열의 각 데이터 형식에 대해 수행되는 변환을 표시합니다.  
  
> [!NOTE]  
>  텍스트 데이터 형식은 이 표에 포함되어 있지 않습니다. 숫자가 텍스트 형식으로 표시되어 있으면 모델 디자이너에서 숫자 형식을 결정하고 숫자로 표시하려고 하는 경우가 종종 있습니다.  
  
#### <a name="addition-"></a>더하기(+)  
  
||||||  
|-|-|-|-|-|  
|연산자(+)|INTEGER|Currency|real|날짜/시간|  
|INTEGER|INTEGER|Currency|real|날짜/시간|  
|Currency|Currency|Currency|real|날짜/시간|  
|real|real|real|real|날짜/시간|  
|날짜/시간|날짜/시간|날짜/시간|날짜/시간|날짜/시간|  
  
 예를 들어 더하기 연산에서 실수(R8)를 통화 데이터(CY)와 함께 사용하는 경우 두 값이 R8로 변환되고 결과가 R8로 반환됩니다.  
  
#### <a name="subtraction--"></a>빼기(-)  
 다음 표에서 행 머리글은 피감수(왼쪽)이고 열 머리글은 감수(오른쪽)입니다.  
  
||||||  
|-|-|-|-|-|  
|연산자(-)|INTEGER|Currency|real|날짜/시간|  
|INTEGER|INTEGER|Currency|real|real|  
|Currency|Currency|Currency|real|real|  
|real|real|real|real|real|  
|날짜/시간|날짜/시간|날짜/시간|날짜/시간|날짜/시간|  
  
 예를 들어 빼기 연산에서 날짜를 다른 데이터 형식과 함께 사용하면 두 값이 날짜로 변환되고 결과 값도 날짜로 반환됩니다.  
  
> [!NOTE]  
>  테이블 형식 모델에서는 단항 연산자인 -(음수)도 지원하지만 이 연산자는 피연산자의 데이터 형식을 변경하지 않습니다.  
  
#### <a name="multiplication-"></a>곱하기(*)  
  
||||||  
|-|-|-|-|-|  
|연산자(*)|INTEGER|Currency|real|날짜/시간|  
|INTEGER|INTEGER|Currency|real|INTEGER|  
|Currency|Currency|real|Currency|Currency|  
|real|real|Currency|real|real|  
  
 예를 들어 곱하기 연산에서 정수를 실수와 함께 사용하는 경우 두 숫자가 실수로 변환되고 반환 값도 실수입니다.  
  
#### <a name="division-"></a>나누기(/)  
 다음 표에서 행 머리글은 피감수(왼쪽)이고 열 머리글은 감수(오른쪽)입니다.  
  
||||||  
|-|-|-|-|-|  
|연산자(/)<br /><br /> (행/열)|INTEGER|Currency|real|날짜/시간|  
|INTEGER|real|Currency|real|real|  
|Currency|Currency|real|Currency|real|  
|real|real|real|real|real|  
|날짜/시간|real|real|real|real|  
  
 예를 들어 나누기 연산에서 정수를 통화 값과 함께 사용하는 경우 두 값이 실수로 변환되고 결과도 실수가 됩니다.  
  
#### <a name="comparison-operators"></a>비교 연산자  
 비교 식에서 부울 값은 문자열 값보다 위로 간주되고 문자열 값은 숫자 또는 날짜/시간 값보다 위로 간주됩니다. 숫자 및 날짜/시간 값은 동일한 순위로 간주됩니다. 부울 또는 문자열 값에 대해서는 암시적 변환이 수행되지 않고, BLANK 공백 값은 다른 비교 값의 데이터 형식에 따라 0/""/false로 변환됩니다.  
  
 다음 DAX 식은 이 동작을 보여 줍니다.  
  
 `=IF(FALSE()>"true","Expression is true", "Expression is false")`를 반환 합니다 `"Expression is true"`  
  
 `=IF("12">12,"Expression is true", "Expression is false")`를 반환 합니다 `"Expression is true"`  
  
 `=IF("12"=12,"Expression is true", "Expression is false")`를 반환 합니다 `"Expression is false"`  
  
 숫자 또는 날짜/시간 형식에 대해서는 다음 표에서 설명한 대로 암시적으로 변환이 수행됩니다.  
  
||||||  
|-|-|-|-|-|  
|비교 연산자|INTEGER|Currency|real|날짜/시간|  
|INTEGER|INTEGER|Currency|real|real|  
|Currency|Currency|Currency|real|real|  
|real|real|real|real|real|  
|날짜/시간|real|real|real|날짜/시간|  
  
##  <a name="bkmk_hand_blanks"></a> 공백, 빈 문자열 및 0 값 처리  
 DAX에서 0 값, Null 및 빈 문자열을 처리하는 방법은 Microsoft Excel 및 SQL Server와 다릅니다. 이 섹션에서는 처리 방법의 차이점과 이러한 데이터 형식을 처리하는 방법에 대해 설명합니다.  
  
 기억할 중요한 사항은 에서 공백 값, 빈 셀 또는 누락된 값을 모두 새 데이터 형식인 BLANK로 표시한다는 것입니다. 더하기 또는 연결과 같은 연산에서 공백이 처리되는 방식은 개별 함수에 따라 다릅니다. BLANK 함수를 사용하여 공백을 생성하거나 ISBLANK 함수를 사용하여 공백을 테스트할 수도 있습니다. 의미 체계 모델에서는 데이터베이스 Null이 지원되지 않으며 DAX 수식에서 Null 값이 포함된 열이 참조되는 경우 Null은 암시적으로 공백으로 변환됩니다.  
  
### <a name="defining-blanks-nulls-and-empty-strings"></a>공백, Null 및 빈 문자열 정의  
 다음 표에는 공백 처리 방식과 관련하여 DAX 및 Microsoft Excel 간의 차이점이 요약되어 있습니다.  
  
||||  
|-|-|-|  
|식|DAX|내보내기|  
|BLANK + BLANK|공백|0(영)|  
|BLANK +5|5|5|  
|BLANK * 5|공백|0(영)|  
|5/BLANK|Infinity|Error|  
|0/BLANK|NaN|Error|  
|BLANK/BLANK|공백|Error|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|공백|Error|  
|BLANK AND BLANK|BLANK|Error|  
  
 특정 함수 또는 연산자에서 공백을 처리하는 방법은 [DAX 함수 참조](https://msdn.microsoft.com/library/ee634396.aspx)섹션에서 각 DAX 함수에 대한 항목을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../data-sources-ssas-tabular.md)   
 [데이터 가져오기 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../import-data-ssas-tabular.md)  
  
  
