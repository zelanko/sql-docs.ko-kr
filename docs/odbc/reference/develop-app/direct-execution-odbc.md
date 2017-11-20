---
title: "직접 실행 ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bdc332f2541fd8537fbd924e1da9ea631d8d3189
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="direct-execution-odbc"></a>ODBC 직접 실행
직접 실행은 문을 실행 하는 가장 간단한 방법은 합니다. 문이 실행을 위해 전송 되 면 데이터 원본 액세스 계획으로 컴파일합니다 하 고 해당 액세스 계획을 실행 합니다.  
  
 직접 실행은 작성 하 고 런타임 시 문을 실행 하는 일반 응용 프로그램에서 일반적으로 사용 됩니다. 예를 들어 다음 코드는 SQL 문을 작성 하 고 한 번 실행:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 직접 실행은 한 번 실행 될 문 적합 합니다. 주요 단점은 SQL 문이 실행 될 때마다를 구문 분석 되는 점입니다. 또한 응용 프로그램 문에 의해 생성 된 (있는 경우)까지 문이 실행 됩니다; 다음 결과 집합에 대 한 정보를 검색할 수 없습니다. 문을 준비 하 고 별도 두 단계로 실행 하는 경우 이것이 가능 합니다.  
  
 를 직접 문을 실행 하려면 응용 프로그램이 다음 작업을 수행 합니다.  
  
1.  매개 변수 값을 설정합니다. 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는 합니다.  
  
2.  호출 **SQLExecDirect** SQL 문을 포함 하는 문자열을 전달 합니다.  
  
3.  때 **SQLExecDirect** 호출 되는 드라이버:  
  
    -   데이터 소스의 SQL 문법을; 문을 구문 분석 하지 않고 사용 하도록 SQL 문을 수정 합니다. 여기에 이스케이프 시퀀스에 설명 된 바꿔 [odbc에서 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)합니다. 응용 프로그램 호출 하 여 수정 된 형식의 SQL 문 검색할 수 **SQLNativeSql**합니다. SQL_ATTR_NOSCAN 문 특성 설정 된 경우에 이스케이프 시퀀스 바뀌지 않습니다.  
  
    -   현재 매개 변수 값을 검색 하 고 필요에 따라 변환 합니다. 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는 합니다.  
  
    -   실행에 대 한 데이터 원본에 문과 변환 된 매개 변수 값을 보냅니다.  
  
    -   모든 오류를 반환 합니다. 여기에 시퀀싱 또는 (잘못 된 커서 상태) SQLSTATE 24000 같은 상태 진단, SQLSTATE 42000 (구문 오류 또는 액세스 위반), 예: 구문 오류 및 SQLSTATE 42S02 같은 의미 체계 오류 (기본 테이블 또는 뷰를 찾을 수 없음).

