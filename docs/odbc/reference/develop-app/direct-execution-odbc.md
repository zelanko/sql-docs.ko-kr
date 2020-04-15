---
title: 직접 실행 ODBC | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc5d942ac0c2af54168248d8e416ca233b2c69e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305164"
---
# <a name="direct-execution-odbc"></a>직접 실행 ODBC
직접 실행은 문을 실행하는 가장 간단한 방법입니다. 실행을 위해 명령문이 제출되면 데이터 원본은 이를 액세스 계획으로 컴파일한 다음 해당 액세스 계획을 실행합니다.  
  
 직접 실행은 런타임에 문을 빌드하고 실행하는 일반 응용 프로그램에서 일반적으로 사용됩니다. 예를 들어 다음 코드는 SQL 문을 작성하고 한 번 실행합니다.  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 직접 실행은 한 번 실행되는 문에 가장 적합합니다. 주요 단점은 SQL 문이 실행될 때마다 구문 분석된다는 것입니다. 또한 응용 프로그램은 명령문이 실행될 때까지 명령문에 의해 생성된 결과 집합에 대한 정보를 검색할 수 없습니다. 이 문제는 두 개의 별도 단계로 작성 되고 실행 되는 경우 가능 합니다.  
  
 문을 직접 실행하기 위해 응용 프로그램은 다음 작업을 수행합니다.  
  
1.  매개 변수의 값을 설정합니다. 자세한 내용은 이 섹션의 다음 부분의 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
2.  **SQLExecDirect를** 호출하고 SQL 문을 포함하는 문자열을 전달합니다.  
  
3.  **SQLExecDirect가** 호출되면 드라이버:  
  
    -   SQL 문을 구문 분석 하지 않고 데이터 원본의 SQL 문법을 사용 하 여 수정 합니다. 여기에는 [ODBC의 이스케이프 시퀀스에서 설명한 이스케이프 시퀀스 교체가 포함됩니다.](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 응용 프로그램은 **SQLNativeSql**을 호출하여 수정된 SQL 문의 형식을 검색할 수 있습니다. SQL_ATTR_NOSCAN 문 특성이 설정된 경우 이스케이프 시퀀스는 대체되지 않습니다.  
  
    -   현재 매개 변수 값을 검색하고 필요에 따라 변환합니다. 자세한 내용은 이 섹션의 다음 부분의 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
    -   실행을 위해 명령문 및 변환된 매개 변수 값을 데이터 원본으로 보냅니다.  
  
    -   오류를 반환합니다. 여기에는 SQLSTATE 24000(잘못된 커서 상태), SQLSTATE 42000(구문 오류 또는 액세스 위반)과 같은 구문 오류 및 SQLSTATE 42S02(기본 테이블 또는 뷰가 찾을 수 없는 경우)와 같은 시퀀싱 또는 상태 진단이 포함됩니다.
