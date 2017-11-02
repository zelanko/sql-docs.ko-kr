---
title: "식 (보고서 작성기 및 SSRS)의 연산자 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 35e702d0d1944cd5e7f2b7120da07e272f30cf70
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>식의 연산자(보고서 작성기 및 SSRS)
  연산자는 식에서 한 개 이상의 항목에 적용되는 동작을 나타내는 기호입니다. 식에서 지원되는 연산자의 범주는 산술 연산자, 비교 연산자, 연결 연산자, 논리 또는 비트 연산자, 비트 시프트 연산자입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>산술  
 산술 연산자는 식에서 두 숫자 항목에 대한 수치 연산을 수행합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|^|특정 숫자를 다른 숫자의 승수로 거듭제곱합니다.|  
|*|두 숫자를 곱합니다.|  
|/|두 숫자를 나누고 부동 소수점 결과를 반환합니다.|  
|\|두 숫자를 나누고 정수 결과를 반환합니다.|  
|Mod|나누기의 정수 나머지를 반환합니다. 예를 들어 7을 5로 나누면 나머지가 2이므로 7 Mod 5는 2입니다.|  
|+|두 수를 더합니다.|  
|-|두 숫자 사이의 차를 반환하거나 숫자 항목의 음수 값을 나타냅니다.|  
  
### <a name="comparison"></a>비교  
 비교 연산자는 두 식이 동일한지 여부를 테스트합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|<|보다 작음|  
|\<=|작거나 같음|  
|>|보다 큼|  
|>=|크거나 같음|  
|=|같음|  
|<>|같지 않음|  
|Like|특정 문자열이 지정된 패턴과 일치하는지를 확인합니다. 패턴은 일반 문자와 와일드카드 문자를 포함할 수 있습니다. 패턴 일치에서 일반 문자는 문자열에 지정된 문자와 정확하게 일치해야 합니다. 그러나 와일드카드 문자는 문자열에서 어느 한 부분만 일치하면 됩니다. LIKE 연산자에 와일드카드 문자를 사용할 경우 = 및 != 문자열 비교 연산자를 사용하는 것보다 훨씬 융통성이 있습니다.<br /><br /> 다음 표에서는 와일드카드로 사용할 수 있는 문자를 나열합니다.<br /><br /> %: 0개 이상의 문자를 가진 문자열<br /><br /> _: 단일 문자<br /><br /> [ ]: 지정된 범위(예: [a-f]) 또는 집합(예: [aeiou])에 속하는 한 개의 문자<br /><br /> [^]: 지정된 범위(예: [^a - f]) 또는 집합(예: [^aeiou])에 속하지 않는 한 개의 문자|  
|Is|두 개체 참조를 비교합니다.|  
  
### <a name="string-concatenation"></a>문자열 연결  
 문자열 연결은 식에서 첫 번째 문자열에 두 번째 문자열을 추가합니다. 다른 문자열 연산의 경우 기본 제공 함수를 사용하십시오.  
  
|연산자|Description|  
|--------------|-----------------|  
|&|두 문자열을 연결합니다.|  
|+|두 문자열을 연결합니다.|  
  
### <a name="logical-and-bitwise"></a>논리 및 비트  
 논리 및 비트 연산자는 식에서 두 정수 항목 사이의 논리 조작을 수행합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|And|두 부울 식에 논리 결합을 수행하거나 두 숫자 식에 비트 결합을 수행합니다.|  
|Not|부울 식에 논리 부정을 수행하거나 숫자 식에 비트 부정을 수행합니다.|  
|또는|두 부울 식에 논리 분리를 수행하거나 두 숫자 값에 비트 분리를 수행합니다.|  
|Xor|두 부울 식에 논리 제외 연산을 수행하거나 두 숫자 식에 비트 제외를 수행합니다.|  
|AndAlso|두 식에 논리 결합을 수행합니다.|  
|OrElse|두 식에 논리 분리를 수행합니다.|  
  
### <a name="bit-shift"></a>비트 시프트  
 비트 연산자는 식에서 두 정수 항목 사이에 비트 조작을 수행합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|<\<|비트 패턴에 산술 왼쪽 시프트를 수행합니다.|  
|>>|비트 패턴에 산술 오른쪽 시프트를 수행합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [식 대화 상자](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [식 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [식 예 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [식 &#40;의 데이터 형식 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [식 대화 상자 &#40; 보고서 작성기 &#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
