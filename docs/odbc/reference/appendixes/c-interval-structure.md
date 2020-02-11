---
title: C 간격 구조 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3387b4fa48eb1a04102daadcc08f971765d7ca2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037784"
---
# <a name="c-interval-structure"></a>C 간격 구조
[C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션에 나열 된 각 c interval 데이터 형식은 동일한 구조를 사용 하 여 간격 데이터를 포함 합니다. **Sqlfetch**, **Sqlfetchscroll**또는 **SQLGetData** 가 호출 되 면 드라이버는 SQL_INTERVAL_STRUCT 구조에 데이터를 반환 하 고, **SQLBindCol**, **SQLGetData**또는 **SQLBindParameter**에 대 한 호출에서 c 데이터 형식에 대해 응용 프로그램에서 지정 된 값을 사용 하 여 SQL_INTERVAL_STRUCT 내용을 해석 하 고, 구조체의 *interval_type* 필드를 c 형식에 해당 하는 *열거형* 값으로 채웁니다. 드라이버는 *interval_type* 필드를 읽지 않으므로 간격 유형을 결정 하지 않습니다. SQL_DESC_CONCISE_TYPE 설명자 필드의 값을 검색 합니다. 구조를 매개 변수 데이터에 사용 하는 경우 드라이버는 응용 프로그램에서 *interval_type* 필드의 값을 다른 값으로 설정 하는 경우에도 apd의 SQL_DESC_CONCISE_TYPE 필드에서 응용 프로그램에 지정 된 값을 사용 하 여 SQL_INTERVAL_STRUCT 내용을 해석 합니다.  
  
 이 구조는 다음과 같이 정의 됩니다.  
  
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
  
 SQL_INTERVAL_STRUCT의 *interval_type* 필드는 union에서 보유 하 고 있는 구조와 관련 된 구조체의 멤버를 응용 프로그램에 나타냅니다. 간격 선행 필드가 unsigned 인 경우 *interval_sign* 필드에 SQL_FALSE 값이 있습니다. SQL_TRUE 되는 경우 선행 필드는 음수입니다. 선행 필드 자체의 값은 *interval_sign*값에 관계 없이 항상 부호가 없습니다. *Interval_sign* 필드는 부호 비트 역할을 합니다.
