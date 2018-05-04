---
title: 10 진수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b4aaf614ac165d7ca867b3bf394ea942a992e19
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="decimal-digits"></a>10 진수
*10 진수* decimal 및 numeric 데이터 형식 소수점 오른쪽 자릿수 또는 데이터의 소수 자릿수의 최대 수로 정의 됩니다. 근사 부동 소수점 숫자 열 또는 매개 변수 눈금 정의 되지 않습니다 소수점 오른쪽 자릿수 하지 고정 되어 있으므로. 초 구성 요소가 포함 된 날짜/시간 또는 간격 데이터에 대 한 10 진수 숫자 데이터의 초 구성 요소에서 소수점 오른쪽 자릿수의 수로 정의 됩니다.  
  
 SQL_DECIMAL 및 SQL_NUMERIC 데이터 형식의 최대 소수 자릿수는 일반적으로 최대 전체 자릿수와 동일 합니다. 그러나 일부 데이터 원본에는 최대 소수 자릿수 대 한 별도 제한을 적용 합니다. 데이터 형식에 대 한 최소 및 최대 눈금을 확인 하려면 응용 프로그램이 호출 **SQLGetTypeInfo**합니다.  
  
 각 간결한 SQL 데이터 형식에 대해 정의 된 소수 자릿수는 다음 표에 표시 됩니다.  
  
|SQL 유형|10 진수|  
|--------------|--------------------|  
|모든 문자 및 이진 유형 [a]|n/a|  
|SQL_DECIMAL<br />SQL_NUMERIC|정의 개수의 소수점 오른쪽 자릿수입니다. 예를 들어 NUMERIC(10,3)로 정의 된 열의 소수 자릿수는 3입니다. 음수 지 수 표기법; 사용 하지 않고 매우 많은 수의 저장소를 지원 하기 위해 수 있습니다. 예를 들어 "12000" – 3 배율이 "12"로 저장할 수 있습니다.|  
|SQL_DECIMAL 및 [a] SQL_NUMERIC 이외의 모든 정확한 숫자 형식|0|  
|모든 근사 데이터 형식 [a]|n/a|  
|SQL_TYPE_DATE, 및 초 구성 요소가 없는 [a] 모든 간격 유형|n/a|  
|SQL_TYPE_DATE 제외한 모든 날짜/시간 형식 및 초 구성 요소와 모든 간격 유형|수 (소수 자릿수 초) 값의 초 부분은 소수점 오른쪽 자릿수입니다. 이 번호는 음수일 수 없습니다.|  
|SQL_GUID|n/a|  
  
 [a]는 *DecimalDigits* 의 인수 **SQLBindParameter** 이 데이터 형식에 대해 무시 됩니다.  
  
 한 설명자 필드의 값에 10 진수 숫자에 대 한 반환 되는 값을 일치 하지 않습니다. 다음 표에 나와 있는 것 처럼 값의 자릿수가 SQL_DESC_SCALE 또는 SQL_DESC_PRECISION 필드 데이터 형식에 따라에서 가져올 수 있습니다.  
  
|SQL 유형|에 해당 하는 설명자 필드<br /><br /> 10 진수|  
|--------------|----------------------------------------------------------|  
|모든 문자 및 이진 유형|n/a|  
|모든 정확한 숫자 형식|SCALE|  
|SQL_BIT|n/a|  
|모든 근사 숫자 형식|n/a|  
|모든 날짜/시간 형식|PRECISION|  
|초 구성 요소와 모든 간격 유형|PRECISION|  
|초 구성 요소가 없는 모든 간격 유형|n/a|
