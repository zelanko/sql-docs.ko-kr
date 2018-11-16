---
title: SQL Server-Azure SQL DB로 응용 프로그램에 액세스할 링크 | Microsoft Docs
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
ms.openlocfilehash: 20efdf681baa8305b3b2be08b2e9f3efe999d3fa
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668532"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>SQL Server-Azure SQL DB (AccessToSQL)에 대 한 액세스 응용 프로그램 연결
사용 하 여 기존의 Access 응용 프로그램을 사용 하려는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 마이그레이션된에 원래 Access 테이블을 연결할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블입니다. 연결을 수정 하 Access 데이터베이스에서 데이터를 사용 하는 쿼리, 폼, 보고서 및 데이터 액세스 페이지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Access 데이터베이스의 데이터 대신 SQL Azure 데이터베이스.  
  
> [!NOTE]  
> Access 테이블 액세스에 남아 있지만 함께 업데이트 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 업데이트 합니다. 테이블을 연결 하 고 기능을 확인 한 후에 액세스 테이블을 삭제 하는 것이 좋습니다.  
  
## <a name="linking-access-and-sql-server-tables"></a>Access 및 SQL Server 테이블 연결  
액세스 테이블을 연결 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블, Jet 데이터베이스 엔진 연결 정보 및 테이블 메타 데이터를 저장 하지만 데이터에 저장 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 이 연결을 선택 하면 실제 테이블 및 데이터에도 액세스 응용 프로그램 액세스 테이블에 대해 작동 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
> [!NOTE]  
> 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증, 암호는 연결 된 테이블 액세스에서 일반 텍스트로 저장 됩니다. Windows 인증을 사용 하는 것이 좋습니다.  
  
**테이블을 연결 하려면**  
  
1.  액세스 메타 데이터 탐색기에서 연결 하려는 테이블을 선택 합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **테이블**를 선택한 후 **링크**합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) 액세스를 위해 원래 Access 테이블을 백업 하 고 연결된 된 테이블을 만듭니다.  
  
테이블에 연결 하면 SSMA의 테이블은 작은 링크 아이콘을 사용 하 여 표시 합니다. 액세스 테이블을 가리키는 화살표를 사용 하 여 구형 "연결된" 아이콘을 사용 하 여 표시 합니다.  
  
테이블에 대 한 액세스를 열 때 데이터는 키 집합 커서를 사용 하 여 검색 됩니다. 따라서 대형 테이블에 대 한 모든 데이터 검색 되지 않습니다 번. 그러나 테이블 검색 한 후에 액세스 필요에 따라 추가 데이터를 검색 합니다.  
  
> [!IMPORTANT]  
> Azure database 사용 하 여 테이블 액세스 링크를 하려면 SQL Server Native Client(SNAC) 버전 10.5 이상.   
> SNAC의 최신 버전을 가져올 수 있습니다 [Microsoft® SQL Server® 2008 R2 기능 팩](https://go.microsoft.com/fwlink/?LinkId=196940)합니다.  
  
## <a name="unlinking-access-tables"></a>테이블 액세스 링크 끊기  
Access 테이블에서 연결을 해제할 때를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 SQL Azure 테이블에 SSMA 원래 Access 테이블 및 해당 데이터를 복원 합니다.  
  
**테이블 연결을 해제 하려면**  
  
1.  액세스 메타 데이터 탐색기에서 연결을 해제 하려는 테이블을 선택 합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **테이블**를 선택한 후 **연결 끊기**합니다.  
  
## <a name="linking-tables-to-a-different-server"></a>테이블을 다른 서버에 연결  
테이블 액세스 한 SQL Server 인스턴스에 연결한 경우 나중에 다른 인스턴스에 링크를 변경 하려면 테이블을 다시 링크 해야 있습니다.  
  
**다른 서버에 연결 하는 테이블**  
  
1.  액세스 메타 데이터 탐색기에서 연결을 해제 하려는 테이블을 선택 합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **테이블** 선택한 후 **연결 끊기**합니다.  
  
3.  클릭 합니다 **SQL Server에 다시 연결** 단추입니다.  
  
4.  인스턴스에 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 액세스 테이블을 연결 하려고 합니다.  
  
5.  액세스 메타 데이터 탐색기에서 연결 하려는 테이블을 선택 합니다.  
  
6.  마우스 오른쪽 단추로 클릭 **테이블**를 선택한 후 **링크**합니다.  
  
## <a name="updating-linked-tables"></a>연결 된 테이블을 업데이트합니다.  
경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블 정의 변경 되를 연결 해제 하 고 다음이 항목의 앞에 나온 절차를 사용 하 여 SSMA의 테이블을 다시 연결할 수 있습니다. 또한 액세스를 사용 하 여 테이블을 업데이트할 수 있습니다.  
  
**액세스를 사용 하 여 연결 된 테이블을 업데이트 하려면**  
  
1.  Access 데이터베이스를 엽니다.  
  
2.  에 **개체** 목록에서 클릭 **테이블**합니다.  
  
3.  연결된 된 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택한 **연결 된 테이블 관리자**합니다.  
  
4.  업데이트 하 고 클릭 하려는 각 연결 된 테이블 옆의 확인란을 선택 **확인**합니다.  
  
## <a name="possible-post-migration-issues"></a>가능한 마이그레이션 후 문제  
다음 섹션에 대 한 액세스에서 데이터베이스를 마이그레이션한 후 기존 Access 응용 프로그램에서 발생할 수 있는 목록 문제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 다음 원인 및 해결 방법을 함께 테이블에 연결 합니다.  
  
### <a name="slow-performance-with-linked-tables"></a>연결 된 테이블을 사용 하 여 성능 저하  
**원인:** 일부 쿼리 속도가 느릴 업사이징 후 다음과 같은 이유로:  
  
-   응용 프로그램에 존재 하지 않는 함수에 따라 달라 집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SELECT 쿼리를 실행 하는 로컬 테이블 아래로 Jet는 SQL Azure입니다.  
  
-   업데이트 또는 여러 행을 삭제 하는 쿼리는 각 행에 대해 매개 변수가 있는 쿼리로 Jet가 전송 됩니다.  
  
**해결 방법:** 통과 쿼리, 저장된 프로시저 또는 뷰를 실행 속도가 느린 쿼리를 변환 합니다. 통과 쿼리를 변환에 다음과 같은 문제가 있습니다.  
  
-   통과 쿼리를 수정할 수 없습니다. 쿼리 결과 수정 하거나 새 레코드를 추가 해야 대체 방식으로 같은 명시적 함으로써 **수정** 하거나 **추가** 쿼리에 바인딩되는 양식에 단추입니다.  
  
-   일부 쿼리 사용자 입력이 필요 하지만 통과 쿼리는 사용자 입력을 지원 하지 않습니다. Visual Basic for Applications (VBA) 코드 매개 변수를 요구 하는 또는 입력 컨트롤로 사용 되는 폼에서 사용자 입력을 얻을 수 있습니다. 두 경우 모두 VBA 코드를 서버에 대 한 사용자 입력을 사용 하 여 쿼리를 제출합니다.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>자동 증분 열에는 레코드가 업데이트 될 때까지 업데이트 되지 않습니다.  
**원인:** RecordSet.AddNew Jet에서를 호출한 후 자동 증분 열이 사용 가능한 레코드를 업데이트 하기 전에 합니다. 사실 이것이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. Id 열의 새 값의 새 값은 새 레코드를 저장 한 후에 사용할 수 있습니다.  
  
**해결 방법:** id 필드에 액세스 하기 전에 다음 Visual Basic for Applications (VBA) 코드를 실행 합니다.  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>새 레코드를 사용할 수 없는 경우  
**원인:** 레코드를 추가 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 고유 인덱스 필드에 기본값을 할당 하지 않으면 값을 해당 필드에 새 레코드에 나타나지 않으면에서 테이블을 다시 열 때까지 경우 VBA를 사용 하 여 SQL Azure 테이블 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 S QL Azure입니다. 새 레코드의 값을 가져오려고 시도 하면 다음 오류 메시지가 나타납니다.  
  
`Run-time error '3167' Record is deleted.`  
  
**해결 방법:** 열면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 VBA 코드를 사용 하 여 테이블을 포함 하는 SQL Azure `dbSeeChanges` 다음 예제와 같이 옵션:  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>마이그레이션 후 일부 쿼리는 사용자가 수 없는 새 레코드를 추가 하려면  
**원인:** 쿼리를 사용 하 여 새 값 쿼리는 고유 인덱스에 포함 된 모든 열이 없는 경우 추가할 수 없습니다.  
  
**해결 방법:** 하나 이상의 고유 인덱스에 포함 된 모든 열 쿼리에 포함 되도록 합니다.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>액세스를 사용 하 여 연결 된 테이블 스키마를 수정할 수 없습니다.  
**원인:** 사용자 데이터 마이그레이션 후 연결 테이블 액세스에서는 테이블의 스키마를 수정할 수 없습니다.  
  
**해결 방법:** 사용 하 여 테이블 스키마를 수정할 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 액세스의 링크를 업데이트 합니다.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>마이그레이션한 후 하이퍼링크 기능 손실은 데이터  
**원인:** 마이그레이션한 후 데이터 열에서 하이퍼링크 해당 기능이 손실 및 간단 하 게 **nvarchar (max)** 열입니다.  
  
**해결 방법:** 없음.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>액세스 하 여 일부 SQL Server 데이터 형식은 지원 되지 않습니다.  
**원인:** 나중에 업데이트 하는 경우에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Access에서 지원 되지 않는 데이터 형식을 포함 하는 SQL Azure 테이블 액세스에서 테이블을 열 수 없습니다.  
  
**해결 방법:** 지원 되는 데이터 형식 행만 반환 하는 액세스 쿼리를 정의할 수 있습니다.  
  
## <a name="see-also"></a>참고자료  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
