---
title: "준비 된 실행 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cedfb3926904af0a9d7393a1ff896c3c2f08a61f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="prepared-execution"></a>준비된 실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC API에서는 반복적인 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 실행과 관련한 구문 분석 및 컴파일 오버헤드를 줄이는 한 가지 방법으로 준비된 실행을 정의합니다. 응용 프로그램은 SQL 문이 포함된 문자열을 작성한 다음 두 단계로 실행합니다. 호출 [SQLPrepare 함수](http://go.microsoft.com/fwlink/?LinkId=59360) 를 문을 구문 분석 하 고 하 여 실행 계획으로 컴파일합니다를 한 번의 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]합니다. 그런 다음 연속 호출 **SQLExecute** 준비 된 실행 계획의 각 실행에 대 한 합니다. 이렇게 하면 각각의 실행에서 구문 분석 및 컴파일 오버헤드를 줄일 수 있습니다. 준비된 실행은 응용 프로그램에서 매개 변수가 있는 동일한 SQL 문을 반복적으로 실행하는 데 많이 사용됩니다.  
  
 대부분의 데이터베이스에서 준비된 실행은 문을 직접 실행하는 경우보다 3-4배 이상 빠릅니다. 가장 큰 이유는 직접 실행할 경우 매번 문이 컴파일되는 반면에 준비된 실행에서는 문이 한 번만 컴파일되기 때문입니다. 또한 준비된 실행을 사용할 경우 문을 실행할 때마다 드라이버가 전체 SQL 문 대신 실행 계획 식별자와 매개 변수 값만 데이터 원본에 보내면 되므로 네트워크 트래픽도 줄일 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]통해을 검색 하 고 실행 계획을 다시 사용 하는 알고리즘이 향상 되어 직접 실행과 준비 된 간의 성능 차이가 감소 **SQLExecDirect**합니다. 따라서 문을 직접 실행할 때도 준비된 실행을 사용할 때와 같이 몇 가지 성능상의 이점을 얻을 수 있습니다. 자세한 내용은 참조 [직접 실행](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 준비된 실행을 기본으로 지원합니다. 실행 계획은 기반 **SQLPrepare** 나중 될 때 실행 되 고 **SQLExecute** 호출 됩니다. 때문에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 임시 저장된 프로시저를 작성할 필요가 없습니다 **SQLPrepare**의 시스템 테이블에는 없는 추가 오버 헤드가 **tempdb**합니다.  
  
 성능상의 이유로 문 준비 될 때까지 지연 됩니다 **SQLExecute** 호출 되거나 메타 속성 작업 (같은 [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) 또는 [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) ODBC의) 수행 됩니다. 이것이 기본 동작입니다. 따라서 준비 중인 문에서 발생하는 모든 오류는 문이 실행되거나 메타 속성 작업이 수행될 때까지 알 수 없습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 관련 문 특성 SQL_SOPT_SS_DEFER_PREPARE를 SQL_DP_OFF로 설정하면 이 기본 동작을 해제할 수 있습니다.  
  
 지연 된 경우 준비, 호출 **SQLDescribeCol** 또는 **SQLDescribeParam** 호출 하기 전에 **SQLExecute** 서버에 대 한 추가 왕복을 생성 합니다. **SQLDescribeCol**, 드라이버는 쿼리에서 WHERE 절을 제거 하 고 쿼리에서 반환한 첫 번째 결과 집합의 열에 대 한 설명을 가져오려면 SET FMTONLY ON을 사용 하 여 서버에 보냅니다. **SQLDescribeParam**, 드라이버는 식 또는 쿼리에서 매개 변수 표식에 참조 되는 열에 대 한 설명을 가져오기 위해 서버를 호출 합니다. 이 메서드에는 하위 쿼리의 매개 변수는 확인할 수 없는 등의 몇 가지 제한이 있습니다.  
  
 과도 하 게 사용 **SQLPrepare** 와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 특히 이전 버전의 SQL Server에 연결 하는 경우 성능이 저하 됩니다. 한 번만 실행되는 문에는 준비된 실행을 사용하지 않아야 합니다. 준비된 실행에는 클라이언트에서 서버로의 추가 네트워크 왕복이 필요하므로 문을 한 번만 실행할 때는 준비된 실행이 직접 실행보다 속도가 느립니다. 또한 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 임시 저장 프로시저도 생성됩니다.  
  
 준비된 문은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 임시 개체를 만드는 데 사용할 수 없습니다.  
  
 사용 되는 일부 초기 ODBC 응용 프로그램 **SQLPrepare** 언제 든 지 [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 사용 되었습니다. **SQLBindParameter** 사용 하지 않아도 **SQLPrepare**를 함께 사용할 수 있습니다 **SQLExecDirect**합니다. 사용 예를 들어 **SQLExecDirect** 와 **SQLBindParameter** 출력은 한 번만 실행된 되는 저장된 프로시저의 매개 변수 또는 반환 코드를 검색 합니다. 사용 하지 마십시오 **SQLPrepare** 와 **SQLBindParameter** 동일한 문이 여러 번 실행 되는 경우가 아니면 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [실행 중인 문 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
