---
title: 식에서의 Integration Services 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- expressions [Integration Services], data types
- data types [Integration Services], expressions
ms.assetid: c296ad10-4080-4988-8c2c-2c250f7a1884
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a06b8864c458817185223a9ee45c3dd25c4a2d33
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183485"
---
# <a name="integration-services-data-types-in-expressions"></a>식에서의 Integration Services 데이터 형식
  식 계산기는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 사용합니다. 데이터가 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에 처음 포함될 때 데이터 흐름 엔진이 모든 열 데이터를 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환하므로 식에 사용되는 열 데이터는 이미 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식입니다. 조건부 분할 및 파생 열 변환에 사용된 식은 열 데이터가 포함된 데이터 흐름에 속해 있으므로 열을 참조할 수 있습니다.  
  
## <a name="variables"></a>변수  
 식에 변수를 사용할 수도 있습니다. 변수는 Variant 데이터 형식으로, 식 계산기는 식을 계산하기 전에 변수의 데이터 형식을 Variant 하위 형식에서 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환합니다. 변수는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식의 하위 집합만 사용할 수 있습니다. 예를 들어 변수는 BLOB(Binary Large Object Block) 데이터 형식을 사용할 수 없습니다.  
  
 Variant 데이터 형식을 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식으로 매핑하는 방법과 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식에 대한 자세한 내용은 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="literals"></a>리터럴  
 또한 식은 문자열, 부울 및 숫자 리터럴을 포함할 수 있습니다. 숫자 리터럴을 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 숫자 데이터 형식으로 변환하는 방법은 [리터럴&#40;SSIS&#41;](numeric-string-and-boolean-literals.md)을 참조하세요.  
  
## <a name="implicit-data-conversion"></a>암시적 데이터 변환  
 데이터 형식의 암시적 변환은 식 계산기가 자동으로 데이터를 한 데이터 형식에서 다른 데이터 형식으로 변환할 때 발생합니다. 예를 들어 경우는 `smallint` 과 비교 되는 `int`, `smallint` 암시적으로 변환할 `int` 비교를 수행 하기 전에.  
  
 인수와 피연산자의 데이터 형식이 호환되지 않는 경우 식 계산기는 암시적 데이터 변환을 수행할 수 없습니다. 또한 식 계산기는 암시적으로 임의의 값을 부울로 변환할 수 없습니다. 대신 인수 및 피연산자는 캐스트 연산자를 사용하여 명시적으로 변환해야 합니다. 자세한 내용은 [캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)를 참조하세요.  
  
 다음 다이어그램에서는 BINARY 연산의 암시적 변환의 결과 유형을 보여 줍니다. 이 테이블에서 열과 행의 교집합은 왼쪽(원본) 및 오른쪽(대상) 유형의 피연산자가 있는 이진 연산의 결과 유형입니다.  
  
 ![데이터 형식 간 암시적 데이터 형식 변환](../media/mw-dts-impl-conver-02.gif "데이터 형식 간 암시적 데이터 형식 변환")  
  
 부호 있는 정수와 부호 없는 정수의 교집합은 두 인수 중 하나보다 클 수도 있는 부호 있는 정수입니다.  
  
 연산자는 문자열, 날짜, 부울 및 기타 데이터 형식을 비교합니다. 연산자가 두 값을 비교하기 전에 식 계산기는 특정 암시적 변환을 수행합니다. 식 계산기는 항상 문자열 리터럴을 DT_WSTR 데이터 형식으로 변환하고 부울 리터럴을 DT_BOOL 데이터 형식으로 변환합니다. 식 계산기는 따옴표로 묶인 모든 값을 문자열로 해석합니다. 숫자 리터럴은 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 숫자 데이터 형식 중 하나로 변환됩니다.  
  
> [!NOTE]  
>  부울 값은 숫자가 아니라 논리 값입니다. 일부 환경에서는 부울 값이 숫자로 표시될 수 있지만 숫자로 저장되지는 않으며, 다양한 프로그래밍 언어에서는 부울 값을 .NET Framework 메서드와는 다른 숫자 값으로 표시합니다.  
>   
>  예를 들어 Visual Basic에서 사용할 수 있는 변환 함수는 `True`를 -1로 변환하지만 .NET Framework의 `System.Convert.ToInt32` 메서드는 `True`를 +1로 변환합니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 식 언어 변환 `True` 를-1입니다.  
>   
>  오류나 예기치 않은 결과를 방지하려면 `True` 및 `False`에 특정 숫자 값을 사용하는 코드를 작성하지 말아야 합니다. 가능하면 부울 변수는 부울 변수용으로 설계된 논리 값으로만 사용해야 합니다.  
  
 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [= = &#40;같은&#41; &#40;SSIS 식&#41;](equal-ssis-expression.md)  
  
-   [\!= &#40;같지 않음&#41;&#40;SSIS 식&#41;](unequal-ssis-expression.md)  
  
-   [&#62;&#40;보다 큰&#41; &#40;SSIS 식&#41;](greater-than-ssis-expression.md)  
  
-   [&#60;&#40;미만&#41; &#40;SSIS 식&#41;](less-than-ssis-expression.md)  
  
-   [&#62;= &#40;보다 크거나 같음&#41; &#40;SSIS 식&#41;](greater-than-or-equal-to-ssis-expression.md)  
  
-   [&#60;= &#40;보다 작거나&#41; &#40;SSIS 식&#41;](less-than-or-equal-to-ssis-expression.md)  
  
 인수가 하나인 함수는 다음과 같은 경우를 제외하고 해당 인수의 데이터 형식으로 결과를 반환합니다.  
  
-   DAY, MONTH 및 YEAR는 날짜를 받아서 정수(DT_I4) 결과를 반환합니다.  
  
-   ISNULL은 모든 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 데이터 형식의 식을 받아서 부울(DT_BOOL) 결과를 반환합니다.  
  
-   SQUARE 및 SQRT는 숫자 식을 받아서 비정수 숫자(DT_R8) 결과를 반환합니다.  
  
 인수의 데이터 형식이 같으면 결과도 해당 형식이 됩니다. 단, DT_DECIMAL 데이터 형식의 두 값에 대한 이진 연산의 반환 결과는 DT_NUMERIC 데이터 형식입니다.  
  
## <a name="requirements-for-data-used-in-expressions"></a>식에 사용되는 데이터에 대한 요구 사항  
 식 계산기는 모든 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 지원합니다. 그러나 연산이나 함수에 따라 피연산자와 인수에 특정 데이터 형식이 필요합니다. 식 계산기는 식에 사용된 데이터에 대해 다음 데이터 형식 요구 사항을 설정합니다.  
  
-   **논리** 연산에 사용된 피연산자는 부울 값이어야 합니다. 예를 들어 ColumnA > 1&&ColumnB < 2가 있습니다.  
  
-   **수치** 연산에 사용된 피연산자는 숫자 값이어야 합니다. 예를 들어 23.75 * 4와 같습니다.  
  
-   논리 및 등가 연산과 같은 비교 연산에 사용된 피연산자는 호환 가능한 데이터 형식이어야 합니다.  
  
     예를 들어 다음 예의 식 중 하나는 DT_DBTIMESTAMPOFFSET 데이터 형식을 사용합니다.  
  
     `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30" != (DT_DBDATE)"1999-10-12"`  
  
     시스템은 `(DT_DBDATE)"1999-10-12"`식을 DT_DBTIMESTAMPOFFSET으로 변환합니다. 변환된 식은 "1999-10-12 00:00:00.000 +00:00"이 되고, 이는 다른 식인 `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30"`과 같지 않으므로 예는 TRUE로 계산됩니다.  
  
-   수치 연산 함수에 전달된 인수는 숫자 데이터 형식이어야 합니다. 함수나 연산에 따라 특정 숫자 데이터 형식이 필요할 수 있습니다. 예를 들어 HEX 함수는 부호 있는 정수나 부호 없는 정수가 필요합니다.  
  
-   문자열 함수에 전달된 인수는 DT_STR 또는 DT_WSTR과 같은 문자 데이터 형식이어야 합니다. 예를 들어 UPPER("flower")와 같습니다. SUBSTRING과 같은 일부 문자열 함수는 시작 위치와 문자열 길이를 나타내는 추가 정수 인수가 필요합니다.  
  
-   날짜 및 시간 함수에 전달된 인수는 유효한 날짜여야 합니다. 예를 들어 DAY(GETDATE())와 같습니다. DATEADD와 같은 일부 함수는 날짜에 추가할 일 수를 나타내는 추가 정수 인수가 필요합니다.  
  
 부호 없는 8바이트 정수와 부호 있는 정수를 결합하는 연산에서 결과 형식을 명확히 하려면 명시적 캐스트가 필요합니다. 자세한 내용은 [캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)를 참조하세요.  
  
 많은 연산 및 함수 결과에는 미리 결정된 데이터 형식이 있습니다. 인수의 데이터 형식이거나 식 계산기가 결과를 캐스팅하는 데이터 형식일 수 있습니다. 예를 들어 논리적 OR 연산자(||)의 결과는 항상 부울이고 ABS 함수의 결과는 인수의 숫자 데이터 형식이며 곱하기의 결과는 손실 없이 결과를 유지할 수 있는 가장 작은 숫자 데이터 형식입니다. 결과의 데이터 형식에 대한 자세한 내용은 [연산자&#40;SSIS 식&#41;](operators-ssis-expression.md) 및 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 구성 요소에서 식 사용](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   pragmaticworks.com의 기술 문서 - [SSIS 식 치트 시트](http://go.microsoft.com/fwlink/?LinkId=217683)  
  
-   social.technet.microsoft.com의 기술 문서 - [SSIS 식 예](http://go.microsoft.com/fwlink/?LinkId=220761)  
  
  