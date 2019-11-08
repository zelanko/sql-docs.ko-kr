---
title: SQL Server에 액세스 응용 프로그램 연결-Azure SQL DB | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, linking to SQL Azure
- Access databases, linking to SQL Server
- auto-increment columns
- data types, unsupported
- hyperlink columns
- linking tables
- migrating databases, post-migration issues
- post-migration issues
- reference, post-migration issues
- refreshing linked tables
- slow performance
- unlinking tables
ms.assetid: 82374ad2-7737-4164-a489-13261ba393d4
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 3bdd11580e1a7e57b72d2d8fe0ce5f54299555db
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632692"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>SQL Server에 액세스 응용 프로그램 연결-Azure SQL DB (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기존 Access 응용 프로그램을 사용 하려는 경우 마이그레이션된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블에 원래 액세스 테이블을 연결할 수 있습니다. 연결 하면 쿼리, 폼, 보고서 및 데이터 액세스 페이지에서 Access 데이터베이스의 데이터 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스의 데이터를 사용 하도록 Access 데이터베이스를 수정 합니다.  
  
> [!NOTE]  
> 액세스 테이블은 Access에 남아 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 업데이트와 함께 업데이트 되지 않습니다. 테이블을 연결 하 고 기능을 확인 한 후 액세스 테이블을 삭제할 수 있습니다.  
  
## <a name="linking-access-and-sql-server-tables"></a>액세스 및 SQL Server 테이블 연결  
Access 테이블을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블에 연결 하면 Jet 데이터베이스 엔진은 연결 정보와 테이블 메타 데이터를 저장 하지만 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure에 저장 됩니다. 이 링크를 사용 하면 실제 테이블과 데이터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 되거나 SQL Azure에도 불구 하 고 access 응용 프로그램이 Access 테이블에 대해 작동할 수 있습니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용 하는 경우 암호는 연결 된 Access 테이블에 일반 텍스트로 저장 됩니다. Windows 인증을 사용 하는 것이 좋습니다.  
  
**테이블을 연결 하려면**  
  
1.  액세스 메타 데이터 탐색기에서 연결 하려는 테이블을 선택 합니다.  
  
2.  **테이블**을 마우스 오른쪽 단추로 클릭 한 다음 **링크**를 선택 합니다.  
  
Access 용 SSMA ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant)는 원래 Access 테이블을 백업 하 고 연결 된 테이블을 만듭니다.  
  
테이블을 연결 하면 SSMA의 테이블에 작은 링크 아이콘이 표시 됩니다. Access에서 테이블은 "연결 됨" 아이콘이 표시 됩니다. 여기에는 화살표가 가리키는 화살표가 표시 됩니다.  
  
Access에서 테이블을 열면 키 집합 커서를 사용 하 여 데이터가 검색 됩니다. 결과적으로, 규모가 많은 테이블의 경우 한 번에 모든 데이터가 검색 되지 않습니다. 그러나 테이블을 탐색할 때 Access에서 필요에 따라 추가 데이터를 검색 합니다.  
  
> [!IMPORTANT]  
> Azure database를 사용 하 여 access 테이블을 연결 하려면 SQL Server Native Client (SNAC) 버전 10.5 이상이 필요 합니다.   
> [Microsoft® SQL Server® 2008 R2 기능 팩](https://www.microsoft.com/en-us/download/details.aspx?id=16978)에서 최신 버전의 SNAC를 가져올 수 있습니다.  
  
## <a name="unlinking-access-tables"></a>Access 테이블 연결 끊기  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블에서 액세스 테이블의 연결을 끊으면 SSMA에서 원래 액세스 테이블과 해당 데이터를 복원 합니다.  
  
**테이블의 연결을 끊으려면**  
  
1.  액세스 메타 데이터 탐색기에서 연결을 끊을 테이블을 선택 합니다.  
  
2.  **테이블**을 마우스 오른쪽 단추로 클릭 한 다음 **연결 끊기**를 선택 합니다.  
  
## <a name="linking-tables-to-a-different-server"></a>다른 서버에 테이블 연결  
하나 SQL Server 인스턴스에 액세스 테이블을 연결 하 고 나중에 다른 인스턴스로 링크를 변경 하려면 테이블을 다시 연결 해야 합니다.  
  
**다른 서버에 테이블을 연결 하려면**  
  
1.  액세스 메타 데이터 탐색기에서 연결을 끊을 테이블을 선택 합니다.  
  
2.  **테이블** 을 마우스 오른쪽 단추로 클릭 하 고 **연결 해제**를 선택 합니다.  
  
3.  **SQL Server에 다시 연결** 단추를 클릭 합니다.  
  
4.  액세스 테이블을 연결 하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 인스턴스에 연결 합니다.  
  
5.  액세스 메타 데이터 탐색기에서 연결 하려는 테이블을 선택 합니다.  
  
6.  **테이블**을 마우스 오른쪽 단추로 클릭 한 다음 **링크**를 선택 합니다.  
  
## <a name="updating-linked-tables"></a>연결 된 테이블 업데이트  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블 정의를 변경 하는 경우이 항목의 앞부분에 나와 있는 절차를 사용 하 여 SSMA에서 테이블의 연결을 끊은 다음 다시 연결할 수 있습니다. 액세스를 사용 하 여 테이블을 업데이트할 수도 있습니다.  
  
**액세스를 사용 하 여 연결 된 테이블을 업데이트 하려면**  
  
1.  Access 데이터베이스를 엽니다.  
  
2.  **개체** 목록에서 **테이블**을 클릭 합니다.  
  
3.  연결 된 테이블을 마우스 오른쪽 단추로 클릭 한 다음 **연결 된 테이블 관리자**를 선택 합니다.  
  
4.  업데이트 하려는 각 연결 된 테이블 옆의 확인란을 선택 하 고 **확인**을 클릭 합니다.  
  
## <a name="possible-post-migration-issues"></a>가능한 마이그레이션 후 문제  
다음 섹션에는 Access에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure로 데이터베이스를 마이그레이션한 후의 원인과 해결 방법으로 데이터베이스를 연결 하면 기존 Access 응용 프로그램에서 발생할 수 있는 문제가 나열 됩니다.  
  
### <a name="slow-performance-with-linked-tables"></a>연결 된 테이블을 사용 하 여 성능 저하  
**원인:** 일부 쿼리는 다음과 같은 이유로 업사이징 후 느릴 수 있습니다.  
  
-   응용 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure에 존재 하지 않는 함수에 따라 달라 지 며,이로 인해 Jet에서 테이블을 로컬로 끌어와 SELECT 쿼리를 실행 합니다.  
  
-   많은 행을 업데이트 하거나 삭제 하는 쿼리는 Jet에서 각 행에 대 한 매개 변수가 있는 쿼리로 전송 됩니다.  
  
**해결 방법:** 느리게 실행 되는 쿼리를 통과 쿼리, 저장 프로시저 또는 뷰로 변환 합니다. 통과 쿼리로 변환 하면 다음과 같은 문제가 발생 합니다.  
  
-   통과 쿼리는 수정할 수 없습니다. 쿼리 결과를 수정 하거나 새 레코드를 추가 하는 방법은 쿼리에 바인딩되는 폼에 명시적으로 **수정** 하거나 단추를 **추가** 하는 등의 방법으로 수행 해야 합니다.  
  
-   일부 쿼리에는 사용자 입력이 필요 하지만 통과 쿼리는 사용자 입력을 지원 하지 않습니다. 사용자 입력은 매개 변수를 요청 하는 Visual Basic for Applications (VBA) 코드 또는 입력 컨트롤로 사용 되는 형식으로 가져올 수 있습니다. 두 경우 모두 VBA 코드는 사용자 입력을 사용 하 여 쿼리를 서버에 제출 합니다.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>자동 증분 열은 레코드가 업데이트 될 때까지 업데이트 되지 않습니다.  
**원인:** Jet에서 레코드 집합 AddNew를 호출한 후 레코드가 업데이트 되기 전에 자동 증분 열을 사용할 수 있습니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure에는 적용 되지 않습니다. 새 레코드를 저장 한 후에만 새 값 id 열의 새 값을 사용할 수 있습니다.  
  
**해결 방법:** Id 필드에 액세스 하기 전에 다음 Visual Basic for Applications (VBA) 코드를 실행 합니다.  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>새 레코드를 사용할 수 없습니다.  
**원인:** VBA를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블에 레코드를 추가 하는 경우 테이블의 고유 인덱스 필드에 기본값이 있는 경우 해당 필드에 값을 할당 하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure에서 테이블을 다시 열 때까지 새 레코드가 표시 되지 않습니다. 새 레코드에서 값을 가져오려고 하면 다음과 같은 오류 메시지가 나타납니다.  
  
`Run-time error '3167' Record is deleted.`  
  
**해결 방법:** VBA 코드를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블을 열 때 다음 예제와 같이 `dbSeeChanges` 옵션을 포함 합니다.  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>마이그레이션 후에는 일부 쿼리에서 사용자가 새 레코드를 추가 하는 것을 허용 하지 않습니다.  
**원인:** 고유 인덱스에 포함 된 열이 쿼리에 포함 되지 않은 경우 쿼리를 사용 하 여 새 값을 추가할 수 없습니다.  
  
**해결 방법:** 하나 이상의 고유 인덱스에 포함 된 모든 열이 쿼리의 일부 인지 확인 합니다.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>액세스 권한이 있는 연결 된 테이블 스키마는 수정할 수 없습니다.  
**원인:** 데이터를 마이그레이션하고 테이블을 연결한 후에는 사용자가 액세스 중인 테이블의 스키마를 수정할 수 없습니다.  
  
**해결 방법:** [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용 하 여 테이블 스키마를 수정한 다음 Access에서 링크를 업데이트 합니다.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>데이터 마이그레이션 후 하이퍼링크 기능이 손실 됨  
**원인:** 데이터를 마이그레이션한 후에는 열의 하이퍼링크가 해당 기능을 상실 하 고 간단한 **nvarchar (max)** 열이 됩니다.  
  
**해결 방법:** 없음을.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>Access에서 일부 SQL Server 데이터 형식을 지원 하지 않습니다.  
**원인:** 나중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블을 업데이트 하 여 Access에서 지원 하지 않는 데이터 형식을 포함 하는 경우 Access에서 테이블을 열 수 없습니다.  
  
**해결 방법:** 지원 되는 데이터 형식의 행만 반환 하는 액세스 쿼리를 정의할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
