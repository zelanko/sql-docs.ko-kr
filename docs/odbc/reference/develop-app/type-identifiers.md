---
description: 형식 식별자
title: 유형 식별자 | Microsoft Docs
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
ms.openlocfilehash: 4ed41716cd351631578d01027663aa9e0f028c7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487446"
---
# <a name="type-identifiers"></a>형식 식별자
ODBC는 SQL 및 C 데이터 형식을 설명 하기 위해 두 개의 *형식 식별자*집합을 정의 합니다. 유형 식별자는 SQL 열 또는 C 버퍼의 유형을 설명 합니다. **#Define** 값 이며 일반적으로 함수 인수로 전달 되거나 메타 데이터에서 반환 됩니다.  
  
 예를 들어 **SQLBindParameter** 에 대 한 다음 호출은 SQL_DATE_STRUCT 형식의 변수를 SQL 문의 DATE 매개 변수에 바인딩합니다. C 형식 식별자 SQL_C_TYPE_DATE *날짜* 변수의 형식을 지정 하 고, SQL 형식 식별자는 동적 매개 변수의 형식을 지정 SQL_TYPE_DATE 합니다.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
