---
title: 10 진수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e58551ae3c6edda3cd865817223fd8052d03ec5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130046"
---
# <a name="decimal-digits"></a>십진수
Decimal 및 numeric 데이터 형식의 *10* 진수는 소수점 오른쪽의 최대 자릿수 또는 데이터의 소수 자릿수로 정의 됩니다. 근사 부동 소수점 수 열 또는 매개 변수의 경우 소수점 오른쪽의 자릿수가 고정 되어 있지 않으므로 소수 자릿수가 정의 되지 않습니다. 초 구성 요소를 포함 하는 날짜/시간 또는 간격 데이터의 경우 10 진수는 데이터의 초 구성 요소에서 소수점 오른쪽의 자릿수를 지정 합니다.  
  
 SQL_DECIMAL 및 SQL_NUMERIC 데이터 형식의 경우 최대 배율은 일반적으로 최대 전체 자릿수와 동일 합니다. 그러나 일부 데이터 원본은 최대 배율에 대해 별도의 제한을 적용 합니다. 데이터 형식에 대해 허용 되는 최소 및 최대 눈금을 확인 하기 위해 응용 프로그램은 **SQLGetTypeInfo**를 호출 합니다.  
  
 각 간결한 SQL 데이터 형식에 대해 정의 된 10 진수는 다음 표에 나와 있습니다.  
  
|SQL 유형|10진수|  
|--------------|--------------------|  
|모든 문자 및 이진 형식 [a]|해당 없음|  
|SQL_DECIMAL<br />SQL_NUMERIC|소수점 오른쪽에 정의 된 자릿수입니다. 예를 들어 숫자 (10, 3)로 정의 된 열의 소수 자릿수는 3입니다. 지 수 표기법을 사용 하지 않고 매우 큰 숫자의 저장소를 지원할 수 있는 음수가 될 수 있습니다. 예를 들어 "12000"은 소수 자릿수가-3 인 "12"로 저장 될 수 있습니다.|  
|SQL_DECIMAL 및 SQL_NUMERIC [a] 이외의 모든 정확한 숫자 형식|0|  
|모든 근사치 데이터 형식 [a]|해당 없음|  
|SQL_TYPE_DATE 및 초 구성 요소가 없는 모든 간격 유형 [a]|해당 없음|  
|SQL_TYPE_DATE를 제외한 모든 datetime 형식과 초 구성 요소가 있는 모든 간격 형식|값의 초 부분에 있는 소수점 오른쪽의 자릿수 (소수 자릿수 초)입니다. 이 숫자는 음수일 수 없습니다.|  
|SQL_GUID|해당 없음|  
  
 [a]이 데이터 형식에 대해 **SQLBindParameter** 의 *DecimalDigits* 인수는 무시 됩니다.  
  
 10 진수에 대해 반환 된 값은 한 설명자 필드의 값과 일치 하지 않습니다. 다음 표와 같이 데이터 형식에 따라 SQL_DESC_SCALE 또는 SQL_DESC_PRECISION 필드에서 값을 가져올 수 있습니다.  
  
|SQL 유형|에 해당 하는 설명자 필드<br /><br /> 10 진수|  
|--------------|----------------------------------------------------------|  
|모든 문자 및 이진 형식|해당 없음|  
|모든 정확한 숫자 형식|SCALE|  
|SQL_BIT|해당 없음|  
|모든 근사 숫자 형식|해당 없음|  
|모든 날짜/시간 형식|PRECISION|  
|초 구성 요소를 포함 하는 모든 간격 유형|PRECISION|  
|초 구성 요소가 없는 모든 간격 유형|해당 없음|
