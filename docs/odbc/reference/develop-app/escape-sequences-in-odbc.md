---
title: ODBC의 이스케이프 시퀀스 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300423"
---
# <a name="escape-sequences-in-odbc"></a>ODBC의 이스케이프 시퀀스
외부 조인 및 스칼라 함수 호출과 같은 많은 언어 기능은 Dbms에서 일반적으로 구현 합니다. 그러나 이러한 기능에 대 한 구문은 표준 구문이 다양 한 표준 본문에서 정의 되는 경우에도 DBMS에 따라 달라 지는 경향이 있습니다. 따라서 ODBC는 다음과 같은 언어 기능에 대 한 표준 구문을 포함 하는 이스케이프 시퀀스를 정의 합니다.  
  
-   날짜, 시간, 타임 스탬프 및 날짜/시간 간격 리터럴  
  
-   숫자, 문자열 및 데이터 형식 변환 함수와 같은 스칼라 함수  
  
-   LIKE 조건자 이스케이프 문자  
  
-   외부 조인  
  
-   프로시저 호출  
  
 ODBC에 사용 되는 이스케이프 시퀀스는 다음과 같습니다.  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>설명  
 이스케이프 시퀀스는 드라이버에 의해 인식 되 고 구문 분석 되어 이스케이프 시퀀스를 DBMS 별 문법으로 바꿉니다. 이스케이프 시퀀스 구문에 대 한 자세한 내용은 부록 C: SQL 문법의 [ODBC 이스케이프 시퀀스](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 를 참조 하세요.  
  
> [!NOTE]  
>  ODBC 2. *x*는 이스케이프 시퀀스의 표준 구문입니다. **-\*-(공급**업체 _-이름_**), 제품 (**_제품 이름_**)**_확장_ ** \*)--**  
>   
>  이 구문 외에도 줄임 구문은 **{**_extension_**}** 형식으로 정의 되었습니다.  
>   
>  ODBC 3. *x*, 긴 형식의 이스케이프 시퀀스는 더 이상 사용 되지 않으며 줄임 형식은 독점적으로 사용 됩니다.  
  
 이스케이프 시퀀스는 드라이버에 의해 DBMS 별 구문에 매핑되므로 응용 프로그램은 이스케이프 시퀀스 또는 DBMS 관련 구문을 사용할 수 있습니다. 그러나 DBMS 관련 구문을 사용 하는 응용 프로그램은 상호 운용할 수 없습니다. 이스케이프 시퀀스를 사용 하는 경우 응용 프로그램은 기본적으로 SQL_ATTR_NOSCAN statement 특성이 해제 되어 있는지 확인 해야 합니다. 그렇지 않으면 이스케이프 시퀀스가 데이터 원본으로 직접 전송 되므로 일반적으로 구문 오류가 발생 합니다.  
  
 드라이버는 기본 언어 기능에 매핑할 수 있는 이스케이프 시퀀스만 지원 합니다. 예를 들어 데이터 원본에서 외부 조인을 지원 하지 않는 경우에는 둘 다 드라이버를 사용할 수 없습니다. 지원 되는 이스케이프 시퀀스를 확인 하기 위해 응용 프로그램은 **SQLGetTypeInfo** 및 **SQLGetInfo**를 호출 합니다. 자세한 내용은 다음 섹션인 [Date, Time 및 Timestamp 리터럴을](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [날짜, 시간, 타임스탬프 리터럴](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [스칼라 함수 호출](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 조건자 이스케이프 문자](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [외부 조인](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)
