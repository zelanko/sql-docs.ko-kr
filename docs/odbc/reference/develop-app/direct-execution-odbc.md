---
title: 직접 실행 ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73c061718dc326e43f72be369a28ad12726a3cab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603051"
---
# <a name="direct-execution-odbc"></a>직접 실행 ODBC
직접 실행은 문을 실행에 대 한 가장 간단한 방법입니다. 문 실행에 대 한 전송 되 면 데이터 원본 액세스 계획으로 컴파일합니다 하 고 그런 다음 해당 액세스 계획을 실행 합니다.  
  
 직접 실행 빌드 및 런타임 시 문을 실행 하는 일반 응용 프로그램에서 흔히 사용 됩니다. 예를 들어, 다음 코드는 SQL 문을 작성 하 고 한 번 실행:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 직접 실행은 한 번 실행 될 문이 적합 합니다. 주요 단점은 해당 실행 될 때마다 SQL 문을 구문 분석을 보여 줍니다. 또한 응용 프로그램 문에 의해 생성 된 (있는 경우) 될 때까지 문을 실행 한 후 결과 집합에 대 한 정보를 검색할 수 없습니다. 문이 준비 되어 별도 두 단계에서 실행 하는 경우 이것이 가능 합니다.  
  
 직접 문을 실행 하려면 응용 프로그램이 다음 작업을 수행 합니다.  
  
1.  매개 변수의 값을 설정합니다. 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는.  
  
2.  호출 **SQLExecDirect** SQL 문을 포함 하는 문자열을 전달 합니다.  
  
3.  때 **SQLExecDirect** 호출 되는 드라이버:  
  
    -   문이; 구문 분석 하지 않고 데이터 원본의 SQL 문법을 사용 하는 SQL 문을 수정 합니다. 여기에 나오는 이스케이프 시퀀스가 교체 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)합니다. 응용 프로그램 호출 하 여 수정 된 형식의 SQL 문 검색할 수 있습니다 **SQLNativeSql**합니다. SQL_ATTR_NOSCAN 문 특성 설정 된 경우에 이스케이프 시퀀스 바뀌지 않습니다.  
  
    -   현재 매개 변수 값을 검색 하 고 필요에 따라 변환 합니다. 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는.  
  
    -   실행에 대 한 데이터 소스에 문 및 변환 된 매개 변수 값을 보냅니다.  
  
    -   오류를 반환합니다. 여기에 시퀀싱 또는 (잘못 된 커서 상태) SQLSTATE 24000 같은 상태 진단, SQLSTATE 42000 (구문 오류 또는 액세스 위반)와 같은 구문 오류 및 SQLSTATE 42S02 같은 의미 체계 오류가 포함 됩니다 (기본 테이블 또는 뷰를 찾을 수 없음).
