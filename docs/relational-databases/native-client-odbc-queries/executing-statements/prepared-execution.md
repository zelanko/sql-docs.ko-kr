---
title: 준비 된 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f55b7a0b3197c05a27dd197147b8c1d38ca5eae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73779806"
---
# <a name="prepared-execution"></a>준비된 실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC API에서는 반복적인 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 실행과 관련한 구문 분석 및 컴파일 오버헤드를 줄이는 한 가지 방법으로 준비된 실행을 정의합니다. 애플리케이션은 SQL 문이 포함된 문자열을 작성한 다음 두 단계로 실행합니다. [Sqlprepare 함수](https://go.microsoft.com/fwlink/?LinkId=59360) 를 한 번 호출 하 여 문을 구문 분석 하 고에서 실행 계획으로 컴파일합니다 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. 그런 다음 준비 된 실행 계획을 실행할 때마다 **Sqlexecute** 를 호출 합니다. 이렇게 하면 각각의 실행에서 구문 분석 및 컴파일 오버헤드를 줄일 수 있습니다. 준비된 실행은 애플리케이션에서 매개 변수가 있는 동일한 SQL 문을 반복적으로 실행하는 데 많이 사용됩니다.  
  
 대부분의 데이터베이스에서 준비된 실행은 문을 직접 실행하는 경우보다 3-4배 이상 빠릅니다. 가장 큰 이유는 직접 실행할 경우 매번 문이 컴파일되는 반면에 준비된 실행에서는 문이 한 번만 컴파일되기 때문입니다. 또한 준비된 실행을 사용할 경우 문을 실행할 때마다 드라이버가 전체 SQL 문 대신 실행 계획 식별자와 매개 변수 값만 데이터 원본에 보내면 되므로 네트워크 트래픽도 줄일 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**Sqlexecdirect**에서 실행 계획을 검색 하 고 다시 사용 하기 위한 향상 된 알고리즘을 통해 직접 실행과 준비 된 실행 간의 성능 차이를 줄입니다. 따라서 문을 직접 실행할 때도 준비된 실행을 사용할 때와 같이 몇 가지 성능상의 이점을 얻을 수 있습니다. 자세한 내용은 [직접 실행](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)을 참조 하세요.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 준비된 실행을 기본으로 지원합니다. Sqlprepare가 호출 될 때 실행 계획은 **Sqlprepare** 이상 **** 에서 작성 됩니다. 는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sqlprepare**에서 임시 저장 프로시저를 작성할 필요가 없기 때문에 **tempdb**의 시스템 테이블에 추가 오버 헤드가 없습니다.  
  
 성능상의 이유로 문 준비는 **Sqlexecute** 가 호출 되거나 메타 속성 작업 (예: [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) 또는 ODBC의 [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) )이 수행 될 때까지 지연 됩니다. 기본 동작입니다. 따라서 준비 중인 문에서 발생하는 모든 오류는 문이 실행되거나 메타 속성 작업이 수행될 때까지 알 수 없습니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 관련 문 특성 SQL_SOPT_SS_DEFER_PREPARE를 SQL_DP_OFF로 설정하면 이 기본 동작을 해제할 수 있습니다.  
  
 지연 된 준비가 된 경우 **Sqlexecute** 를 호출 하기 전에 **SQLDescribeCol** 또는 **SQLDescribeParam** 를 호출 하면 서버에 대 한 추가 왕복이 생성 됩니다. **SQLDescribeCol**에서 드라이버는 쿼리에서 WHERE 절을 제거 하 고 SET FMTONLY ON으로 서버에 전송 하 여 쿼리에서 반환 된 첫 번째 결과 집합의 열에 대 한 설명을 가져옵니다. **SQLDescribeParam**에서 드라이버는 서버를 호출 하 여 쿼리의 매개 변수 표식에서 참조 하는 식 또는 열에 대 한 설명을 가져옵니다. 이 메서드에는 하위 쿼리의 매개 변수는 확인할 수 없는 등의 몇 가지 제한이 있습니다.  
  
 Native Client ODBC 드라이버를 사용 하 여 Sqlprepare를 과도 하 게 사용 하면 특히 이전 버전의 SQL Server에 연결 된 경우 성능이 저하 됩니다. **** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 한 번만 실행되는 문에는 준비된 실행을 사용하지 않아야 합니다. 준비된 실행에는 클라이언트에서 서버로의 추가 네트워크 왕복이 필요하므로 문을 한 번만 실행할 때는 준비된 실행이 직접 실행보다 속도가 느립니다. 또한 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 임시 저장 프로시저도 생성됩니다.  
  
 준비된 문은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 임시 개체를 만드는 데 사용할 수 없습니다.  
  
 일부 초기 ODBC 응용 프로그램에서는 [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 를 사용할 때마다 **sqlprepare** 를 사용 했습니다. **SQLBindParameter** 는 **sqlprepare**를 사용할 필요가 없습니다. **sqlexecdirect**에서 사용할 수 있습니다. 예를 들어 **SQLBindParameter** 와 함께 **sqlexecdirect** 를 사용 하 여 한 번만 실행 되는 저장 프로시저에서 반환 코드 또는 출력 매개 변수를 검색 합니다. 동일한 문이 여러 번 실행 되는 경우를 제외 하 고 **SQLBindParameter** 에서 **sqlprepare** 를 사용 하지 마세요.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;문을 실행 하는 중](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
