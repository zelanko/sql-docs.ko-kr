---
title: C 간격 구조 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02c86ebe24a0e12531e355f95185b01f3089a31b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292155"
---
# <a name="c-interval-structure"></a>C 간격 구조
[C 데이터 유형](../../../odbc/reference/appendixes/c-data-types.md) 섹션에 나열된 각 C 간격 데이터 형식은 동일한 구조를 사용하여 간격 데이터를 포함합니다. **SQLFetch**, **SQLFetch스크롤**또는 **SQLGetData가** 호출되면 드라이버는 SQL_INTERVAL_STRUCT 구조로 데이터를 반환하고, C 데이터 형식에 대한 응용 프로그램에서 지정한 값을 SQL_INTERVAL_STRUCT **sqlGetData**또는 **SQLBindParameter호출에서**사용하고, SQL_INTERVAL_STRUCT 내용을 해석하고, C 형식에 해당하는 *열거형* 값으로 구조의 *interval_type* 필드를 채웁니다. **SQLGetData** 드라이버는 간격의 유형을 결정하기 위해 *interval_type* 필드를 읽지 않습니다. SQL_DESC_CONCISE_TYPE 설명자 필드의 값을 검색합니다. 구조가 매개 변수 데이터에 사용되는 경우 드라이버는 응용 프로그램이 *interval_type* 필드의 값을 다른 값으로 설정하더라도 APD의 SQL_DESC_CONCISE_TYPE 필드에 응용 프로그램에서 지정한 값을 사용하여 SQL_INTERVAL_STRUCT 내용을 해석합니다.  
  
 이 구조는 다음과 같이 정의됩니다.  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 SQL_INTERVAL_STRUCT *interval_type* 필드는 응용 프로그램에 어떤 구조가 조합에 보관되어 있는지, 그리고 구조의 구성원이 어떤 관련이 있는지를 나타냅니다. *interval_sign* 필드에는 인터벌 선행 필드가 서명되지 않은 경우 SQL_FALSE 값이 있습니다. SQL_TRUE 경우 선행 필드는 음수입니다. 선행 필드 자체의 값은 *interval_sign*값에 관계없이 항상 서명되지 않습니다. *interval_sign* 필드는 기호 비트 역할을 합니다.
