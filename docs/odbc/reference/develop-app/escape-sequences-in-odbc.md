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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33259a56faa19dda2403996b6d6d8930ec2a87be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706001"
---
# <a name="escape-sequences-in-odbc"></a>ODBC의 이스케이프 시퀀스
언어 등의 기능, 외부 조인 및 스칼라 함수 호출 수는 일반적으로 Dbms에 의해 구현 됩니다. 그러나 이러한 기능에 대 한 구문은 경향이 DBMS 관련 표준 구문을 다양 한 표준 기관에서 정의 된 경우에 있습니다. 이 인해 ODBC는 다음 언어 기능에 대 한 표준 구문을 포함 하는 이스케이프 시퀀스를 정의 합니다.  
  
-   날짜, 시간, 타임 스탬프 및 날짜/시간 간격 리터럴  
  
-   숫자와 같이 스칼라 함수, 문자열 및 데이터 형식 변환 함수  
  
-   같은 조건자 이스케이프 문자  
  
-   외부 조인  
  
-   프로시저 호출  
  
 ODBC에서 사용 된 이스케이프 시퀀스는 다음과 같습니다.  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Remarks  
 이스케이프 시퀀스를 인식 하 고 드라이버 특정 DBMS 문법 이스케이프 시퀀스를 대체 하 여 구문 분석 합니다. 이스케이프 시퀀스 구문에 대 한 자세한 내용은 참조 하세요. [ODBC 이스케이프 시퀀스](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 부록 c: SQL 문법에서입니다.  
  
> [!NOTE]  
>  Odbc 2. *x*,이 이스케이프 시퀀스의 표준 구문을: **-(\*공급 업체 (***공급 업체 이름***), 제품 (***제품 이름***) * * * 확장*  **\*)--**  
>   
>  이 구문은 외에도 축약형 구문 형식의 정의 된: **{0}***확장***}**  
>   
>  Odbc 3. *x*, 긴 형식의 이스케이프 시퀀스는 더 이상 사용 되지 않습니다, 및 약식 형태는 단독으로 사용 해야 합니다.  
  
 드라이버 DBMS 관련 구문에서 이스케이프 시퀀스는 매핑되므로 이스케이프 시퀀스 또는 DBMS 관련 구문을 응용 프로그램이 사용할 수 있습니다. 그러나 DBMS 특정 구문을 사용 하는 응용 프로그램은 상호 운용 되지 않습니다. 이스케이프 시퀀스를 사용 하면 응용 프로그램 SQL_ATTR_NOSCAN 문 특성 설정 되어 있는지, 기본적으로는 확인 해야 합니다. 그렇지 않은 경우 이스케이프 시퀀스는 일반적으로 하면 구문 오류가 데이터 원본에 직접 전송 됩니다.  
  
 드라이버 지원만 이러한 이스케이프 시퀀스는 기본 언어 기능에 매핑할 수 있습니다. 예를 들어, 데이터 원본 외부 조인을 지원 하지 않으면, 드라이버도 됩니다. 이스케이프 시퀀스는 지를 확인 하려면 응용 프로그램 호출 **SQLGetTypeInfo** 하 고 **SQLGetInfo**합니다. 자세한 내용은 다음 섹션을 참조 하세요 [날짜, 시간 및 타임 스탬프 리터럴](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [날짜, 시간, 타임스탬프 리터럴](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [스칼라 함수 호출](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 조건자 이스케이프 문자](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [외부 조인](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)
