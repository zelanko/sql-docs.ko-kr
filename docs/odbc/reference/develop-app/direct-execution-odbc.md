---
description: 직접 실행 ODBC
title: ODBC 직접 실행 | Microsoft Docs
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
ms.openlocfilehash: 9be03c4f20a82e134481f8fd9bb849ffd830567a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476705"
---
# <a name="direct-execution-odbc"></a>직접 실행 ODBC
직접 실행은 문을 실행 하는 가장 간단한 방법입니다. 실행을 위해 문이 전송 되 면 데이터 원본에서 액세스 계획으로 컴파일한 다음 해당 액세스 계획을 실행 합니다.  
  
 직접 실행은 일반적으로 런타임에 문을 빌드하고 실행 하는 제네릭 응용 프로그램에서 사용 됩니다. 예를 들어 다음 코드는 SQL 문을 작성 하 고 한 번 실행 합니다.  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 직접 실행은 한 번 실행 되는 문에 가장 적합 합니다. 주요 단점은 SQL 문이 실행 될 때마다 구문 분석 된다는 것입니다. 또한 문이 실행 될 때까지 응용 프로그램은 문 (있는 경우)에서 만든 결과 집합에 대 한 정보를 검색할 수 없습니다. 문을 준비 하 고 별도의 두 단계로 실행 하는 경우이 작업을 수행할 수 있습니다.  
  
 문을 직접 실행 하기 위해 응용 프로그램은 다음 작업을 수행 합니다.  
  
1.  매개 변수의 값을 설정 합니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.  
  
2.  **Sqlexecdirect** 를 호출 하 고 SQL 문을 포함 하는 문자열을 전달 합니다.  
  
3.  **Sqlexecdirect** 를 호출 하는 경우 드라이버는 다음과 같습니다.  
  
    -   문을 구문 분석 하지 않고 데이터 원본의 SQL 문법을 사용 하도록 SQL 문을 수정 합니다. 여기에는 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)에 설명 된 이스케이프 시퀀스 바꾸기가 포함 됩니다. 응용 프로그램은 **SQLNativeSql**를 호출 하 여 SQL 문의 수정 된 형태를 검색할 수 있습니다. SQL_ATTR_NOSCAN statement 특성이 설정 된 경우 이스케이프 시퀀스는 대체 되지 않습니다.  
  
    -   현재 매개 변수 값을 검색 하 고 필요에 따라 변환 합니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.  
  
    -   실행을 위해 문과 변환 된 매개 변수 값을 데이터 원본으로 보냅니다.  
  
    -   모든 오류를 반환 합니다. 여기에는 SQLSTATE 24000 (잘못 된 커서 상태)와 같은 시퀀싱 또는 상태 진단, SQLSTATE 42000 (구문 오류 또는 액세스 위반)와 같은 구문 오류 및 SQLSTATE 42S02 (기본 테이블 또는 뷰를 찾을 수 없음)와 같은 의미 오류가 포함 됩니다.
