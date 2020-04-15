---
title: ODBC의 이스케이프 시퀀스 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d41b0c03ecbe6de63cba1a28a1f39f12a42dc86
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300423"
---
# <a name="escape-sequences-in-odbc"></a>ODBC의 이스케이프 시퀀스
외부 조인 및 스칼라 함수 호출과 같은 여러 언어 기능은 일반적으로 DBMS에 의해 구현됩니다. 그러나 이러한 기능에 대한 구문은 다양한 표준 기관에서 표준 구문이 정의되는 경우에도 DBMS에 특정되는 경향이 있습니다. 따라서 ODBC는 다음 언어 기능에 대한 표준 구문이 포함된 이스케이프 시퀀스를 정의합니다.  
  
-   날짜, 시간, 타임스탬프 및 날짜 시간 간격 리터럴  
  
-   숫자, 문자열 및 데이터 형식 변환 함수와 같은 스칼라 함수  
  
-   같은 조건자 탈출 문자  
  
-   외부 조인  
  
-   프로시저 호출  
  
 ODBC에서 사용하는 이스케이프 시퀀스는 다음과 같습니다.  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>설명  
 이스케이프 시퀀스는 이스케이프 시퀀스를 DBMS 별 문법으로 대체하는 드라이버에 의해 인식되고 구문 분석됩니다. 이스케이프 시퀀스 구문에 대한 자세한 내용은 부록 C: SQL 문법의 [ODBC 이스케이프 시퀀스를](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 참조하십시오.  
  
> [!NOTE]  
>  ODBC 2. *x*, 이스케이프 시퀀스의 표준 구문이었다: **--(공급업체\*이름),**_vendor-name_**제품(제품**_이름)_**)** ** \*확장)-** _extension_  
>   
>  이 구문 외에도 약식 구문이 양식에_extension_**}** 정의되었습니다. **{**  
>   
>  ODBC 3. *x*, 이스케이프 시퀀스의 긴 형태가 더 이상 사용되지 않았으며 약식 형식은 독점적으로 사용됩니다.  
  
 이스케이프 시퀀스는 드라이버에서 DBMS 관련 구문에 매핑되므로 응용 프로그램은 이스케이프 시퀀스 또는 DBMS 관련 구문을 사용할 수 있습니다. 그러나 DBMS 관련 구문을 사용하는 응용 프로그램은 상호 운용할 수 없습니다. 이스케이프 시퀀스를 사용하는 경우 응용 프로그램은 SQL_ATTR_NOSCAN 문 특성이 꺼져 있는지 확인해야 합니다. 그렇지 않으면 이스케이프 시퀀스가 데이터 원본으로 직접 전송되며 일반적으로 구문 오류가 발생합니다.  
  
 드라이버는 기본 언어 기능에 매핑할 수 있는 이스케이프 시퀀스만 지원합니다. 예를 들어 데이터 원본이 외부 조인을 지원하지 않는 경우 드라이버도 지원하지 않습니다. 지원되는 이스케이프 시퀀스를 결정하기 위해 응용 프로그램은 **SQLGetTypeInfo** 및 **SQLGetInfo**를 호출합니다. 자세한 내용은 다음 섹션, [날짜, 시간 및 타임스탬프 리터럴을](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [날짜, 시간, 타임스탬프 리터럴](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [스칼라 함수 호출](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 조건자 이스케이프 문자](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [외부 조인](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)
