---
title: 형식 식별자 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79aa4de5d722208195477f7ffef53cac6c61a2de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093019"
---
# <a name="type-identifiers"></a>형식 식별자
ODBC SQL 및 C에 해당 하는 데이터의 종류를 설명 하기 위해 두 가지를 정의 *식별자*합니다. 형식 식별자는 SQL 열 또는 C 버퍼 유형을 설명합니다. 것을 **#define** 값 및 일반적으로 함수 인수로 전달 되었거나 메타 데이터에 반환 합니다.  
  
 다음을 호출 하는 예를 들어 **SQLBindParameter** SQL_DATE_STRUCT 형식의 변수 SQL 문에서 날짜 매개 변수를 바인딩합니다. C 형식 식별자 SQL_C_TYPE_DATE의 유형을 지정 합니다 *날짜* 변수와 SQL 유형 식별자 SQL_TYPE_DATE 동적 매개 변수의 형식을 지정 합니다.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
