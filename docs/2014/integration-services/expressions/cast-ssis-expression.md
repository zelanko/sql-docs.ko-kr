---
title: 캐스트(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CAST function
- cast operator
- converting data types [Integration Services]
- data types [Integration Services], expressions
- data types [Integration Services], converting
ms.assetid: d4e915cc-1c7b-4b2e-93b0-13a8b0cb9242
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6068ef0fea56681048b8a31a9e87b6b01d4f8c96
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819325"
---
# <a name="cast-ssis-expression"></a>캐스트(SSIS 식)
  식의 데이터 형식을 다른 데이터 형식으로 명시적으로 변환합니다. 캐스트 연산자는 잘라내기 연산자로 실행될 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
(type_spec) expression  
  
```  
  
## <a name="arguments"></a>인수  
 *type_spec*  
 유효한 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 데이터 형식입니다.  
  
 *expression*  
 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 *type_spec*데이터 형식입니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 다음 다이어그램에서는 유효한 캐스트 연산을 보여 줍니다.  
  
 ![데이터 형식 간 유효한 캐스트 및 유효하지 않은 캐스트](../media/data-conversion.gif "데이터 형식 간 유효한 캐스트 및 유효하지 않은 캐스트")  
  
 일부 데이터 형식으로의 캐스트는 매개 변수가 필요합니다. 다음 표에서는 이러한 데이터 형식과 해당 매개 변수를 보여 줍니다.  
  
|데이터 형식|매개 변수|예제|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252)는 1252 코드 페이지를 사용하여 30바이트 또는 30자의 단일 문자를 DT_STR 데이터 형식으로 캐스팅합니다.|  
|DT_WSTR|*Charcount*|(DT_WSTR,20)은 20바이트 쌍 또는 20자의 유니코드 문자를 DT_WSTR 데이터 형식으로 캐스팅합니다.|  
|DT_BYTES|*Bytecount*|(DT_BYTES,50)은 50바이트를 DT_BYTES 데이터 형식으로 캐스팅합니다.|  
|DT_DECIMAL|*소수 자릿수*|(DT_DECIMAL,2)는 소수 자릿수 2를 사용하여 숫자 값을 DT_DECIMAL 데이터 형식으로 캐스팅합니다.|  
|DT_NUMERIC|*전체 자릿수*<br /><br /> *소수 자릿수*|(DT_NUMERIC,10,3)은 전체 자릿수 10, 소수 자릿수 3을 사용하여 숫자 값을 DT_NUMERIC 데이터 형식으로 캐스팅합니다.|  
|DT_TEXT|*Codepage*|(DT_TEXT,1252)는 1252 코드 페이지를 사용하여 값을 DT_TEXT 데이터 형식으로 캐스팅합니다.|  
  
 문자열을 DT_DATE로 캐스팅하거나 그 반대의 경우 변환 로캘이 사용됩니다. 단, 로캘 기본 설정이 ISO 형식을 사용하는지 여부에 관계없이 날짜는 ISO 형식 YYYY-MM-DD로 설정됩니다.  
  
> [!NOTE]  
>  문자열을 DT_DATE가 아닌 다른 날짜 데이터 형식으로 변환하려면 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
 코드 페이지가 멀티바이트 문자 코드 페이지이면 바이트 수와 문자 수가 다를 수 있습니다. 동일한 *charcount* 값을 사용하여 DT_WSTR에서 DT_STR로 캐스팅하면 변환된 문자열의 마지막 문자가 잘릴 수 있습니다. 대상 테이블의 열에 사용 가능한 저장 공간이 충분한 경우 멀티바이트 코드 페이지에 필요한 바이트 수를 반영하여 *charcount* 매개 변수의 값을 설정합니다. 예를 들어 936 코드 페이지를 사용하여 문자 데이터를 DT_STR 데이터 형식으로 캐스팅하는 경우 *charcount* 를 데이터에 포함될 예상 문자 수보다 최대 2배의 값으로 설정해야 합니다. UTF-8 코드 페이지를 사용하여 문자 데이터를 캐스팅하는 경우에는 *charcount* 를 최대 4배의 값으로 설정해야 합니다.  
  
 날짜 데이터 형식의 구조에 대한 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하십시오.  
  
## <a name="ssis-expression-examples"></a>SSIS 식 예  
 이 예에서는 숫자 값을 정수로 캐스팅합니다.  
  
```  
(DT_I4) 3.57  
```  
  
 이 예에서는 1252 코드 페이지를 사용하여 정수를 문자열로 캐스팅합니다.  
  
```  
(DT_STR,1,1252)5  
```  
  
 이 예에서는 3자 문자열을 더블바이트 문자로 캐스팅합니다.  
  
```  
(DT_WSTR,3)"Cat"  
```  
  
 이 예에서는 정수를 소수 자릿수 2의 10진수로 캐스팅합니다.  
  
```  
(DT_DECIMAl,2)500  
```  
  
 이 예에서는 정수를 전체 자릿수가 7이고 소수 자릿수가 3인 정수로 캐스팅합니다.  
  
```  
(DT_NUMERIC,7,3)4000  
```  
  
 이 예에서는 1252 코드 페이지를 사용하여 **nvarchar** 데이터 형식과 길이 50으로 정의된 **FirstName** 열의 값을 문자열로 캐스팅합니다.  
  
```  
(DT_STR,50,1252)FirstName  
```  
  
 이 예에서는 DT_DBDATE 형식의 **DateFirstPurchase** 열에 있는 값을 길이가 20인 유니코드 문자열에 캐스팅합니다.  
  
```  
(DT_WSTR,20)DateFirstPurchase  
```  
  
 이 예에서는 문자열 "True"를 부울로 캐스팅합니다.  
  
```  
(DT_BOOL)"True"  
```  
  
 이 예에서는 문자열 리터럴을 DT_DBDATE로 캐스팅합니다.  
  
```  
(DT_DBDATE) "1999-10-11"  
```  
  
 이 예에서는 문자열 리터럴을 소수 자릿수 초에 5자리를 사용하는 DT_DBTIME2 데이터 형식으로 캐스팅합니다. DT_DBTIME2 데이터 형식은 소수 자릿수 초에 지정된 0부터 7자리까지 가질 수 있습니다.  
  
```  
(DT_DBTIME2, 5) "16:34:52.12345"  
```  
  
 이 예에서는 문자열 리터럴을 소수 자릿수 초에 4자리를 사용하는 DT_DBTIMESTAMP2 데이터 형식으로 캐스팅합니다. DT_DBTIMESTAMP2 데이터 형식은 소수 자릿수 초에 지정된 0부터 7자리까지 가질 수 있습니다.  
  
```  
(DT_DBTIMESTAMP2, 4) "1999-10-11 16:34:52.1234"  
```  
  
 이 예에서는 문자열 리터럴을 소수 자릿수 초에 7자리를 사용하는 DT_DBTIMESTAMPOFFSET 데이터 형식으로 캐스팅합니다. DT_DBTIMESTAMPOFFSET 데이터 형식은 소수 자릿수 초에 지정된 0부터 7자리까지 가질 수 있습니다.  
  
```  
(DT_DBTIMESTAMPOFFSET, 7) "1999-10-11 16:34:52.1234567 + 5:35"  
```  
  
## <a name="see-also"></a>관련 항목  
 [연산자 우선 순위 및 계산 방향](operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](operators-ssis-expression.md)   
 [Integration Services&#40;SSIS&#41; 식](integration-services-ssis-expressions.md)   
 [식에서의 Integration Services 데이터 형식](integration-services-data-types-in-expressions.md)  
  
  
