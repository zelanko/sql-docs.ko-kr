---
title: 유형 식별자 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a274a19eaa0a2fdf98bcaa9ef42406ee8a6b6461
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306434"
---
# <a name="type-identifiers"></a>형식 식별자
SQL 및 C 데이터 형식을 설명하기 위해 ODBC는 두 가지 *형식 식별자*집합을 정의합니다. 형식 식별자는 SQL 열 또는 C 버퍼의 형식을 설명합니다. **#define** 값이며 일반적으로 함수 인수로 전달되거나 메타데이터에서 반환됩니다.  
  
 예를 들어 **SQLBindParameter에** 대한 다음 호출은 SQL_DATE_STRUCT 형식의 변수를 SQL 문의 날짜 매개 변수에 바인딩합니다. C 형식 식별 SQL_C_TYPE_DATE자는 *date* 변수의 형식을 지정하고 SQL 형식 식별자는 SQL_TYPE_DATE 동적 매개 변수의 형식을 지정합니다.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
