---
title: 소수 자릿수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4921a6162b6d711e657f223b5be5783dfa37bca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285163"
---
# <a name="decimal-digits"></a>십진수
소수점 및 숫자 데이터 형식의 *소수 자릿수는* 소수점 오른쪽의 최대 자릿수 또는 데이터의 배율로 정의됩니다. 대략적인 부동 소수점 수 열 또는 매개변수의 경우 소수점 오른쪽의 자릿수가 고정되지 않으므로 배율이 정의되지 않습니다. 초 구성 요소를 포함하는 datetime 또는 간격 데이터의 경우 소수 자릿수는 데이터의 초 구성 요소에서 소수점의 오른쪽에 있는 자릿수로 정의됩니다.  
  
 SQL_DECIMAL 및 SQL_NUMERIC 데이터 형식의 경우 최대 축척은 일반적으로 최대 정밀도와 동일합니다. 그러나 일부 데이터 원본은 최대 축척에 별도의 제한을 가합니다. 데이터 형식에 허용되는 최소 및 최대 축척을 결정하기 위해 응용 프로그램은 **SQLGetTypeInfo**를 호출합니다.  
  
 각 간결한 SQL 데이터 형식에 대해 정의된 소수 자릿수는 다음 표에 나와 있습니다.  
  
|SQL 유형|10진수|  
|--------------|--------------------|  
|모든 문자 및 이진 유형[a]|해당 없음|  
|SQL_DECIMAL<br />SQL_NUMERIC|소수점 오른쪽에 정의된 자릿수입니다. 예를 들어 NUMERIC(10,3)으로 정의된 열의 배율은 3입니다. 지수 표기법의 사용 없이 매우 큰 수의 저장소를 지원하는 음수일 수 있습니다. 예를 들어 "12000"은 -3의 배율로 "12"로 저장할 수 있습니다.|  
|SQL_DECIMAL 및 SQL_NUMERIC 이외의 모든 정확한 숫자 유형[a]|0|  
|모든 대략적인 데이터 유형[a]|해당 없음|  
|SQL_TYPE_DATE 초 구성 요소가 없는 모든 간격 유형[a]|해당 없음|  
|SQL_TYPE_DATE 제외한 모든 일시 입력 및 초 구성 요소가 있는 모든 간격 형식|값의 초 부분(소수점)의 소수점 오른쪽에 있는 숫자 수입니다. 이 숫자는 음수일 수 없습니다.|  
|SQL_GUID|해당 없음|  
  
 [a] **SQLBindParameter의** *DecimalDigits* 인수는 이 데이터 형식에 대해 무시됩니다.  
  
 소수 자릿수에 대해 반환된 값은 하나의 설명자 필드의 값과 일치하지 않습니다. 값은 다음 표와 같이 데이터 형식에 따라 SQL_DESC_SCALE 또는 SQL_DESC_PRECISION 필드에서 올 수 있습니다.  
  
|SQL 유형|대응하는 설명자 필드<br /><br /> 10 진수|  
|--------------|----------------------------------------------------------|  
|모든 문자 및 이진 형식|해당 없음|  
|모든 정확한 숫자 유형|SCALE|  
|SQL_BIT|해당 없음|  
|모든 대략적인 숫자 유형|해당 없음|  
|모든 날짜 유형|PRECISION|  
|초 구성 요소가 있는 모든 간격 유형|PRECISION|  
|초 구성 요소가 없는 모든 간격 유형|해당 없음|
