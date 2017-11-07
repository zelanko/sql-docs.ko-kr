---
title: "Analysis Services 테이블 형식 모델에서 지원 되는 데이터 형식 | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 6d18cbe5b20882581afa731ce5d207cbbc69be6c
ms.openlocfilehash: d86b23c7c1b56d7407e0068c2e77e184be1aa36d
ms.contentlocale: ko-kr
ms.lasthandoff: 10/21/2017

---
# <a name="data-types-supported-in-tabular-models"></a>테이블 형식 모델에서 지원 되는 데이터 형식

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  이 문서에서는 테이블 형식 모델에서 사용할 수 있는 데이터 형식에 대해 설명하고 DAX(Data Analysis Expressions) 수식에서 데이터를 계산하거나 사용할 때 암시적으로 수행되는 데이터 형식 변환에 대해 설명합니다.  

  
##  <a name="bkmk_data_types"></a>테이블 형식 모델에서 사용 되는 데이터 형식  
수식에서 데이터를 가져오거나 값을 사용하는 경우 원래 데이터 원본에 다른 데이터 형식이 포함되어 있더라도 다음 데이터 형식 중 하나로 데이터가 변환됩니다. 수식의 결과 값도 이러한 데이터 형식을 사용합니다.  
  
 일반적으로 이러한 데이터 형식은 계산 열의 정확한 계산을 위해 구현되며 일관성을 위해 모델의 나머지 데이터에도 동일한 제한이 적용됩니다.  
  
 숫자, 통화, 날짜 및 시간에 사용되는 서식은 모델 데이터로 작업하는 데 사용된 클라이언트에서 지정한 로캘의 서식을 따라야 합니다. 모델에서 서식 옵션을 사용하여 값이 표시되는 방식을 제어할 수 있습니다.  
  
||||  
|-|-|-|  
|**모델의 데이터 형식**|**DAX의 데이터 형식**|**Description**|  
|정수|64비트(8바이트) 정수 값*<br /><br /> 참고:<br />         DAX 수식은 너무 작아서 설명에 나열된 최소 값을 저장할 수 없는 데이터 형식을 지원하지 않습니다.|소수 자릿수가 없는 숫자입니다. 정수는 양수나 음수가 될 수 있지만 -9,223,372,036,854,775,808(-2^63)부터 9,223,372,036,854,775,807(2^63-1) 사이의 정수여야 합니다.|  
|10진수|64비트(8바이트) 실수*<br /><br /> 참고:<br />         DAX 수식은 너무 작아서 설명에 나열된 최소 값을 저장할 수 없는 데이터 형식을 지원하지 않습니다.|실수는 소수 자리를 가질 수 있는 수입니다. 실수는 광범위한 값을 포함합니다.<br /><br /> -1.79E +308에서 -2.23E -308 사이의 음수 값<br /><br /> 0<br /><br /> 2.23E -308에서 1.79E + 308 사이의 양수 값<br /><br /> 하지만 유효 숫자 수는 열일곱 자릿수로 제한됩니다.|  
|Boolean|Boolean|True 또는 False 값입니다.|  
|텍스트|문자열|유니코드 문자 데이터 문자열입니다. 문자열, 숫자 또는 날짜를 텍스트 형식으로 표시 될 수 있습니다.|  
|날짜|날짜/시간|허용되는 날짜-시간 표현의 날짜 및 시간<br /><br /> 유효한 날짜는 1900년 3월 1일 이후의 모든 날짜입니다.|  
|Currency|Currency|통화 데이터 형식에는 -922,337,203,685,477.5808부터 922,337,203,685,477.5807 사이의 소수 자릿수가 고정된 네 자릿수를 사용할 수 있습니다.|  
|해당 사항 없음|공백|공백은 SQL null을 나타내거나 대체하는 DAX의 데이터 형식입니다. BLANK 함수를 사용하여 공백을 만들고 논리 함수 ISBLANK를 사용하여 공백을 테스트할 수 있습니다.|  
  
 \*큰 숫자 값을 가진 데이터 하려고 하면 다음 오류와 함께 가져오기가 실패할 수 있습니다.  
  
 메모리 내 데이터베이스 오류:는 '\<열 이름 >'의 열은 '\<테이블 이름 >' 테이블에 값이 있는 ' 1.7976931348623157 e + 308' 지원 되지 않습니다. 작업이 취소 되었습니다.  
  
 이 오류는 모델 디자이너에서 해당 값을 사용하여 null을 나타내기 때문에 발생합니다. 다음 목록의 값은 앞에서 말한 null 값과 동의어입니다.  
  
||  
|-|  
|Value|  
|9223372036854775807|  
|-9223372036854775808|  
|1.7976931348623158e+308|  
|2.2250738585072014e-308|  
  
 데이터에서 값을 제거 하 고 가져오기를 다시 시도 하십시오.  
  
> [!NOTE]  
>  131,072자가 넘는 문자열이 포함된 **varchar(max)** 열에서는 가져올 수 없습니다.  
  
### <a name="table-data-type"></a>테이블 데이터 형식  
 또한 DAX에서는 *table* 데이터 형식도 사용합니다. 이 데이터 형식은 DAX에서 집계 및 시간 인텔리전스 계산과 같은 여러 함수에 사용됩니다. 일부 함수에는 테이블에 대한 참조가 필요하고 일부 함수는 다른 함수의 입력으로 사용할 수 있는 테이블을 반환합니다. 테이블을 입력으로 사용해야 하는 일부 함수에서는 테이블로 계산되는 식을 지정할 수 있고 일부 함수에는 기본 테이블에 대한 참조가 필요합니다. 특정 함수에 대한 요구 사항은 [DAX 함수 참조](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b)를 참조하십시오.  
  
##  <a name="bkmk_implicit"></a>DAX 수식의 암시적 및 명시적 데이터 형식 변환
  
 각 DAX 함수에는 입력 및 출력으로 사용되는 데이터 형식과 관련된 특정 요구 사항이 있습니다. 예를 들어 정수와 날짜를 인수로 사용해야 하는 함수도 있고 텍스트 또는 테이블을 인수로 사용해야 하는 함수도 있습니다.  
  
 인수로 지정 하는 열의 데이터가 함수에 필요한 데이터 형식과 호환 되지 않으면 대부분의 경우 DAX는 오류를 반환 합니다. 그러나 아무 곳에 나 가능한 DAX 하려고 암시적으로 데이터를 필요한 데이터 형식으로 변환 합니다. 예를 들어  
  
-   숫자(예: "123")를 문자열로 입력할 수 있습니다. DAX는 문자열을 구문 분석 하 고 숫자 데이터 형식으로 지정 하려고 합니다.  
  
-   TRUE + 1을 추가하여 2라는 결과를 얻을 수 있습니다. TRUE가 암시적으로 숫자 1로 변환되어 1+1 연산이 수행되기 때문입니다.  
  
-   두 열의 값을 더할 때 한 값은 텍스트("12")로 표시되고 다른 값은 숫자(12)로 표시된 경우 DAX에서 암시적으로 문자열을 숫자로 변환한 다음 더하여 숫자 결과를 반환합니다. 다음 식은 44: = "22" + 22를 반환합니다.  
  
-   두 숫자를 연결 하려고 하면 문자열로 표시 되며 다음 연결 됩니다. 다음 식은 "1234": = 12 & 34를 반환합니다.  
  
 다음 표에는 수식에서 수행되는 암시적 데이터 형식 변환이 요약되어 있습니다. 일반적으로 의미 체계 모델 디자이너는 Microsoft Excel처럼 작동하며 지정된 작업에 필요한 경우 가능하면 항상 암시적 변환을 수행합니다.  
  
### <a name="table-of-implicit-data-conversions"></a>암시적 데이터 변환 표  
 요청된 연산을 수행하기 전에 필요한 값을 캐스팅하는 연산자에 의해 수행되는 변환 유형이 결정됩니다. 다음 표에서는 연산자를 나열하고 교차 행의 데이터 형식과 함께 사용되는 열의 각 데이터 형식에 대해 수행되는 변환을 표시합니다.  
  
> [!NOTE]  
>  텍스트 데이터 형식은 이 표에 포함되어 있지 않습니다. 많은 경우에 따라 텍스트 형식으로 표현 될 때 모델 디자이너 숫자 형식을 결정 하 고 숫자로 표시 하려고 합니다.  
  
#### <a name="addition-"></a>더하기(+)  
  
||||||  
|-|-|-|-|-|  
|연산자(+)|INTEGER|Currency|REAL|날짜/시간|  
|INTEGER|INTEGER|Currency|REAL|날짜/시간|  
|Currency|Currency|Currency|REAL|날짜/시간|  
|REAL|REAL|REAL|REAL|날짜/시간|  
|날짜/시간|날짜/시간|날짜/시간|날짜/시간|날짜/시간|  
  
 예를 들어 더하기 연산에서 실수(R8)를 통화 데이터(CY)와 함께 사용하는 경우 두 값이 R8로 변환되고 결과가 R8로 반환됩니다.  
  
#### <a name="subtraction--"></a>빼기(-)  
 다음 표에서 행 머리글은 감수 (왼쪽) 및 열 머리글은 감수 (오른쪽):  
  
||||||  
|-|-|-|-|-|  
|연산자(-)|INTEGER|Currency|REAL|날짜/시간|  
|INTEGER|INTEGER|Currency|REAL|REAL|  
|Currency|Currency|Currency|REAL|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|날짜/시간|날짜/시간|날짜/시간|날짜/시간|날짜/시간|  
  
 예를 들어 빼기 연산에서 날짜를 다른 데이터 형식과 함께 사용하면 두 값이 날짜로 변환되고 결과 값도 날짜로 반환됩니다.  
  
> [!NOTE]  
>  테이블 형식 모델에서는 단항 연산자인 -(음수)도 지원하지만 이 연산자는 피연산자의 데이터 형식을 변경하지 않습니다.  
  
#### <a name="multiplication-"></a>곱하기(*)  
  
||||||  
|-|-|-|-|-|  
|연산자(*)|INTEGER|Currency|REAL|날짜/시간|  
|INTEGER|INTEGER|Currency|REAL|INTEGER|  
|Currency|Currency|REAL|Currency|Currency|  
|REAL|REAL|Currency|REAL|REAL|  
  
 예를 들어 곱하기 연산에서 정수를 실수와 함께 사용하는 경우 두 숫자가 실수로 변환되고 반환 값도 실수입니다.  
  
#### <a name="division-"></a>나누기(/)  
 다음 표에서 행 머리글은 피감수(왼쪽)이고 열 머리글은 감수(오른쪽)입니다.  
  
||||||  
|-|-|-|-|-|  
|연산자(/)<br /><br /> (행/열)|INTEGER|Currency|REAL|날짜/시간|  
|INTEGER|REAL|Currency|REAL|REAL|  
|Currency|Currency|REAL|Currency|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|날짜/시간|REAL|REAL|REAL|REAL|  
  
 예를 들어 나누기 연산에서 정수를 통화 값과 함께 사용하는 경우 두 값이 실수로 변환되고 결과도 실수가 됩니다.  
  
#### <a name="comparison-operators"></a>비교 연산자  
비교 작업에 대 한 혼합 된 데이터 형식 조합의 제한 된 집합에만 사용할 수 있습니다. 자세한 내용은 [DAX 연산자 참조](https://msdn.microsoft.com/library/ee634237.aspx)를 참조하세요.  
  
## <a name="bkmk_hand_blanks"></a>공백, 빈 문자열 및 0 값 처리  
 다음 표에서에서 공백이 처리 되는 방법은 Microsoft Excel 및 DAX 간의 차이점이 요약 되어 있습니다.  
  
||||  
|-|-|-|  
|식|DAX|Excel|  
|BLANK + BLANK|공백|0(영)|  
|BLANK +5|5|5|  
|BLANK * 5|공백|0(영)|  
|5/BLANK|Infinity|오류|  
|0/BLANK|NaN|오류|  
|BLANK/BLANK|공백|오류|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|공백|오류|  
|BLANK AND BLANK|공백|오류|  
  
 특정 함수 또는 연산자에서 공백을 처리하는 방법은 [DAX 함수 참조](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b)섹션에서 각 DAX 함수에 대한 항목을 참조하세요.  
  

