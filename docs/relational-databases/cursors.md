---
description: 커서(SQL Server)
title: 커서(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- results [SQL Server], cursors
- Transact-SQL cursors, about cursors
- cursors [SQL Server]
- data access [SQL Server], cursors
- result sets [SQL Server], cursors
- requesting cursors
- cursors [SQL Server], about cursors
ms.assetid: e668b40c-bd4d-4415-850d-20fc4872ee72
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a209c033a9218423e298b54bb04809355c9d0507
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485535"
---
# <a name="sql-server-cursors"></a>SQL Server 커서
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
  관계형 데이터베이스에서의 연산은 전체 행 집합에 적용됩니다. 예를 들어 `SELECT` 문에 의해 반환된 행 세트는 명령문의 `WHERE` 절 조건을 만족하는 모든 행으로 구성됩니다. SELECT 문에 의해 반환된 전체 행 집합을 결과 집합이라고 합니다. 애플리케이션, 특히 대화형 온라인 애플리케이션에서는 전체 결과 집합을 한 단위로 사용하므로 항상 효과적으로 작업할 수는 없습니다. 이러한 애플리케이션에는 한 번에 한 행이나 적은 행 블록을 사용하여 작업하는 메커니즘이 필요합니다. 커서는 이러한 메커니즘을 제공하는 결과 집합에 대한 확장입니다.  
  
 커서는 다음과 같이 결과 처리를 확장합니다.  
  
-   결과 집합의 특정 행에 위치를 정할 수 있습니다.  
  
-   결과 집합의 현재 위치에서 한 행 또는 행 블록을 검색합니다.  
  
-   결과 집합의 현재 위치에 있는 행 데이터를 수정할 수 있습니다.  
  
-   결과 집합에 나타난 데이터베이스 데이터에 대해 다른 사용자가 변경한 내용을 여러 가지 수준으로 볼 수 있습니다.  
  
-   스크립트, 저장 프로시저 및 트리거의 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 결과 집합의 데이터에 액세스할 수 있도록 합니다.  
  
> [!TIP]
> 일부 시나리오에서는 테이블에 기본 키가 있는 경우 커서의 오버헤드를 발생시키지 않고 `WHILE` 루프를 커서 대신 사용할 수 있습니다.
> 하지만 커서를 사용하지 않을 방법이 없을 뿐 아니라 실제로 커서가 필요한 시나리오도 있습니다. 이 경우 커서를 기반으로 테이블을 업데이트하기 위한 요구 사항이 없는 경우 *firehose* 커서, 즉, [빠른 정방향 및 읽기 전용](#forward-only) 커서를 사용합니다.
  
## <a name="cursor-implementations"></a>커서 구현  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 세 가지 커서 구현을 지원합니다.  
  
### <a name="transact-sql-cursors"></a>Transact-SQL 커서  
[!INCLUDE[tsql](../includes/tsql-md.md)] 커서는 `DECLARE CURSOR` 구문을 기반으로 하며 주로 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트, 저장 프로시저 및 트리거에 사용됩니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 커서는 서버에 구현되며 클라이언트가 서버로 보내는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문으로 관리됩니다. 또한 일괄 처리, 저장 프로시저 또는 트리거에 포함될 수 있습니다.  
  
### <a name="application-programming-interface-api-server-cursors"></a>API(애플리케이션 프로그래밍 인터페이스) 서버 커서  
API 커서는 OLE DB와 ODBC의 API 커서 함수를 지원합니다. API 서버 커서는 서버에 구현됩니다. 클라이언트 애플리케이션에서 API 커서 함수를 호출할 때마다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client OLE DB 공급자나 ODBC 드라이버가 API 서버 커서에 대한 동작 요청을 서버에 전송합니다.  
  
### <a name="client-cursors"></a>클라이언트 커서  
클라이언트 커서는 ADO API를 구현하는 DLL과 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 내부적으로 구현됩니다. 클라이언트 커서는 모든 결과 집합 행을 클라이언트에 캐시하여 구현됩니다. 클라이언트 애플리케이션에서 API 커서 함수를 호출할 때마다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ODBC 드라이버나 ADO DLL이 클라이언트에 캐시된 결과 집합 행에 대해 커서 작업을 수행합니다.  
  
## <a name="type-of-cursors"></a>커서 유형  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]은 네 가지 커서 유형을 지원합니다. 

> [!NOTE]
> 커서는 tempdb 작업 테이블을 활용할 수 있습니다. 분산되는 집계 또는 정렬 작업과 마찬가지로, I/O에서 발생하며 성능 병목 가능성이 있습니다. `STATIC` 커서는 처음부터 작업 테이블을 사용합니다. 자세한 내용은 [쿼리 처리 아키텍처의 작업 테이블 가이드](../relational-databases/query-processing-architecture-guide.md#worktables)를 참조하세요.

### <a name="forward-only"></a>정방향 전용  
정방향 전용 커서는 `FORWARD_ONLY` 및 `READ_ONLY`로 지정되며 스크롤을 지원하지 않습니다. 이러한 커서를 *firehose* 라고도 하며 커서의 시작부터 끝까지 행을 순차적으로 인출하는 것만 지원합니다. 행은 인출될 때까지 데이터베이스에서 검색되지 않습니다. 현재 사용자가 만들거나 다른 사용자가 커밋하여 결과 세트의 행에 영향을 주는 모든 `INSERT`, `UPDATE` 및 `DELETE` 문의 결과는 행이 커서에서 인출될 때 표시됩니다.  
  
 이 커서는 뒤로 스크롤할 수 없기 때문에 행이 인출된 후 데이터베이스 행의 변경 내용은 대부분 커서를 통해 표시되지 않습니다. 클러스터형 인덱스가 적용되는 열을 업데이트하는 경우와 같이 결과 집합 내의 행 위치를 결정하는 데 사용되는 값이 수정되면 커서를 통해 수정된 값이 표시됩니다.  
  
 데이터베이스 API 커서 모델에서는 정방향 전용 커서가 고유한 커서 유형으로 간주되지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 그렇지 않습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 정방향 전용과 스크롤이 모두 정적, 키 집합 및 동적 커서에 적용할 수 있는 옵션으로 간주됩니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 커서는 정방향 전용 정적, 키 집합 및 동적 커서를 지원합니다. 데이터베이스 API 커서 모델은 정적, 키 집합 및 동적 커서가 항상 스크롤 가능하다고 가정합니다. 데이터베이스 API 커서 특성 또는 속성을 정방향 전용으로 설정하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 이를 정방향 전용 동적 커서로 구현합니다.  
  
### <a name="static"></a>정적  
 정적 커서의 전체 결과 집합은 커서가 열릴 때 **tempdb** 에 작성됩니다. 정적 커서는 항상 커서가 열렸을 당시의 결과 집합을 표시합니다. 정적 커서는 변경 내용을 거의 검색하지 못하는 반면 스크롤 시 리소스를 거의 소비하지 않습니다.  
  
커서는 결과 집합의 멤버 자격이나 결과 집합을 구성하는 행의 열 값 변경에 영향을 주는 데이터베이스 변경 내용을 반영하지 않습니다. 정적 커서는 커서가 열린 후 데이터베이스에 삽입된 새 행이 커서 `SELECT` 문의 검색 조건과 일치하는 경우에도 이러한 행을 표시하지 않습니다. 또한 결과 집합을 구성하는 행을 다른 사용자가 업데이트할 경우 새 데이터 값이 정적 커서에 표시되지 않습니다. 정적 커서는 커서가 열린 후 데이터베이스에서 삭제된 행을 표시합니다. 커서를 닫았다가 다시 열지 않는 한 `UPDATE`, `INSERT` 또는 `DELETE` 작업은 정적 커서에 반영되지 않으며 이는 커서를 연 동일한 연결을 사용하여 수정한 경우에도 마찬가지입니다.  
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 정적 커서는 항상 읽기 전용입니다.  
  
> [!NOTE]
> 정적 커서의 결과 세트는 **tempdb** 의 작업 테이블에 저장되므로 결과 세트의 행 크기가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블의 최대 행 크기를 초과할 수 없습니다.  
> 자세한 내용은 [쿼리 처리 아키텍처의 작업 테이블 가이드](../relational-databases/query-processing-architecture-guide.md#worktables)를 참조하세요. 자세한 내용은 [SQL Server의 최대 용량 사양](../sql-server/maximum-capacity-specifications-for-sql-server.md)을 참조하세요.  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] 에서는 정적 커서와 무관한 용어를 사용합니다. 일부 데이터베이스 API에서는 정적 커서를 스냅샷 커서로 식별합니다.  
  
### <a name="keyset"></a>Keyset  
키 집합 커서의 멤버 자격과 행 순서는 커서가 열릴 때 고정됩니다. 키 집합 커서는 키 집합이라는 고유 식별자 집합으로 제어되며 키는 결과 집합에서 행을 고유하게 식별하는 열 집합으로 작성됩니다. 키 세트는 커서가 열려 있을 때 `SELECT` 문의 조건에 맞는 모든 행의 키 값 세트입니다. 키 집합 커서의 키 집합은 커서가 열려 있을 때 **tempdb** 에 작성됩니다.  
  
### <a name="dynamic"></a>동적  
동적 커서는 정적 커서의 반대 개념입니다. 커서를 통해 스크롤할 때 동적 커서는 행의 모든 변경 내용을 결과 집합에 반영합니다. 따라서 인출할 때마다 결과 집합에서 행의 데이터 값, 순서 및 멤버 자격이 변경될 수 있습니다. 모든 사용자가 실행한 모든 `UPDATE`, `INSERT` 및 `DELETE` 문은 커서를 통해 볼 수 있습니다. **SQLSetPos** 같은 API 함수 또는 [!INCLUDE[tsql](../includes/tsql-md.md)] `WHERE CURRENT OF` 절을 사용하여 커서를 통해 업데이트한 경우 즉시 그 결과를 볼 수 있습니다. 커서 트랜잭션 격리 수준을 커밋되지 않은 읽기로 설정한 경우를 제외하고는 커서 외부에서 수행된 업데이트는 커밋될 때까지 볼 수 없습니다. 격리 수준에 대한 자세한 내용은 [트랜잭션 격리 수준 설정&#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요. 
 
> [!NOTE]
> 동적 커서 계획은 공간 인덱스를 사용하지 않습니다.  
  
## <a name="requesting-a-cursor"></a>커서 요청  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 두 가지 방법으로 커서를 요청할 수 있습니다.  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]  
  
     [!INCLUDE[tsql](../includes/tsql-md.md)] 언어는 ISO 커서 구문을 본뜬 커서 사용 구문을 지원합니다.  
  
-   데이터베이스 API(애플리케이션 프로그래밍 인터페이스) 커서 함수  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 다음과 같은 데이터베이스 API의 커서 기능을 지원합니다.  
  
    -   ADO([!INCLUDE[msCoName](../includes/msconame-md.md)] ActiveX Data Object)  
  
    -   OLE DB  
  
    -   ODBC(Open Database Connectivity)  
  
애플리케이션에서 이러한 두 가지 커서 요청 방법을 혼합하여 사용할 수 없습니다. API를 사용하여 커서 동작을 지정한 애플리케이션은 또한 [!INCLUDE[tsql](../includes/tsql-md.md)] DECLARE CURSOR 문을 실행하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 커서를 요청할 수 없습니다. 모든 API 커서 특성을 기본값으로 설정한 경우에만 DECLARE CURSOR를 실행해야 합니다.  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] 및 API 커서 모두 요청되지 않은 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 기본적으로 기본 결과 집합이라고 하는 전체 결과 집합을 애플리케이션에 반환합니다.  
  
## <a name="cursor-process"></a>커서 프로세스  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 커서와 API 커서는 구문이 서로 다르지만 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 커서에 대해 다음과 같은 일반 프로세스를 사용합니다.  
  
1.  커서와 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 결과 집합을 연결하고 커서 행의 업데이트 가능 여부 등 커서의 특성을 정의합니다.  
  
2.  [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행하여 커서를 채웁니다.  
  
3.  보려는 커서의 행을 검색합니다. 커서에서 한 행이나 한 행 블록을 검색하는 작업을 인출이라고 합니다. 일련의 인출 작업을 수행하여 행을 앞으로 또는 뒤로 검색하는 것을 스크롤이라고 합니다.  
  
4.  또는 커서의 현재 위치에 있는 행에 대해 수정 작업(업데이트 또는 삭제)을 수행합니다.  
  
5.  커서를 닫습니다.  
  
## <a name="related-content"></a>관련 내용  
[커서 동작](../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)    
[커서 구현 방법](../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
## <a name="see-also"></a>참고 항목  
[DECLARE CURSOR&#40;Transact-SQL&#41;](../t-sql/language-elements/declare-cursor-transact-sql.md)   
[커서&#40;Transact-SQL&#41;](../t-sql/language-elements/cursors-transact-sql.md)   
[커서 함수&#40;Transact-SQL&#41;](../t-sql/functions/cursor-functions-transact-sql.md)   
[커서 저장 프로시저&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)    

  
