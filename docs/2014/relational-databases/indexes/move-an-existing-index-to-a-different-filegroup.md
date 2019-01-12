---
title: 다른 파일 그룹으로 기존 인덱스 이동 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- moving tables
- switching filegroups for index
- moving indexes
- indexes [SQL Server], moving
- filegroups [SQL Server], switching
ms.assetid: 167ebe77-487d-4ca8-9452-4b2c7d5cb96e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cd3c7f0bb394025581e4a2dffc8eb79a43acb498
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127923"
---
# <a name="move-an-existing-index-to-a-different-filegroup"></a>다른 파일 그룹으로 기존 인덱스 이동
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 현재 파일 그룹에서 다른 파일 그룹으로 기존 인덱스를 이동하는 방법을 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **기존 인덱스를 다른 파일 그룹으로 이동하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   테이블에 클러스터형 인덱스가 있는 경우 클러스터형 인덱스를 새 파일 그룹으로 이동하면 테이블도 해당 파일 그룹으로 이동합니다.  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 UNIQUE 또는 PRIMARY KEY 제약 조건을 사용하여 만든 인덱스를 이동할 수 없습니다. 이러한 인덱스를 이동하려면 [에서](/sql/t-sql/statements/create-index-transact-sql) CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)]문을 (DROP_EXISTING=ON) 옵션과 함께 사용합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-using-table-designer"></a>테이블 디자이너를 사용하여 기존 인덱스를 다른 파일 그룹으로 이동하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 이동할 인덱스가 포함된 테이블이 있는 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  이동할 인덱스가 포함된 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
4.  **테이블 디자이너** 메뉴에서 **인덱스/키**를 클릭합니다.  
  
5.  이동할 인덱스를 선택합니다.  
  
6.  주 표에서 **데이터 공간 사양**을 확장합니다.  
  
7.  **파일 그룹 또는 파티션 구성표 이름** 을 선택하고 목록에서 인덱스를 이동할 파일 그룹 또는 파티션 구성표를 선택합니다.  
  
8.  **닫기**를 클릭합니다.  
  
9. **파일** 메뉴에서 _table_name_ **저장**을 선택합니다.  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-in-object-explorer"></a>개체 탐색기에서 기존 인덱스를 다른 파일 그룹으로 이동하려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 이동할 인덱스가 포함된 테이블이 있는 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 이동할 인덱스가 포함된 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **인덱스** 폴더를 확장합니다.  
  
5.  이동할 인덱스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **페이지 선택**아래에서 **스토리지**를 선택합니다.  
  
7.  인덱스를 이동할 파일 그룹을 선택합니다.  
  
     테이블 또는 인덱스가 분할된 경우 인덱스를 이동할 파티션 구성표를 선택합니다. 분할된 인덱스에 대한 자세한 내용은 [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)를 참조하세요.  
  
     클러스터형 인덱스를 이동할 경우 온라인 처리를 사용할 수 있습니다. 온라인 처리는 인덱스 작업 중 기본 데이터 및 비클러스터형 인덱스에 대한 동시 사용자 액세스를 허용합니다. 자세한 내용은 [Perform Index Operations Online](perform-index-operations-online.md)을 참조하세요.  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 사용하는 다중 프로세서 컴퓨터에서는 최대 병렬 처리 값을 지정하여 인덱스 문 실행에 사용되는 프로세서 수를 구성할 수 있습니다. 병렬 인덱스 작업 기능은 일부 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다. 병렬 인덱스 작업에 대한 자세한 내용은 [병렬 인덱스 작업 구성](configure-parallel-index-operations.md)을 참조하세요.  
  
8.  **확인**을 클릭합니다.  
  
 **인덱스 속성 –** _index_name_ 대화 상자의 **스토리지** 페이지에서 다음 정보를 사용할 수 있습니다.  
  
 **파일 그룹**  
 지정한 파일 그룹에 인덱스를 저장합니다. 목록에는 표준(행) 파일 그룹만 표시됩니다. 목록에서는 기본적으로 데이터베이스의 PRIMARY 파일 그룹이 선택됩니다.  
  
 **Filestream 파일 그룹**  
 FILESTREAM 데이터의 파일 그룹을 지정합니다. 이 목록에는 FILESTREAM 파일 그룹만 표시됩니다. 목록에서는 기본적으로 PRIMARY FILESTREAM 파일 그룹이 선택됩니다.  
  
 **파티션 구성표**  
 파티션 구성표에 인덱스를 저장합니다. **파티션 구성표** 를 클릭하면 아래의 표가 활성화됩니다. 목록에서는 기본적으로 테이블 데이터를 저장하는 데 사용되는 파티션 구성표가 선택됩니다. 목록에서 다른 파티션 구성표를 선택하면 표의 정보가 업데이트됩니다.  
  
 데이터베이스에 파티션 구성표가 없으면 파티션 구성표 옵션을 사용할 수 없습니다.  
  
 **Filestream 파티션 구성표**  
 FILESTREAM 데이터의 파티션 구성표를 지정합니다. 이 파티션 구성표는 **파티션 구성표** 옵션에서 지정한 구성표와 대칭이어야 합니다.  
  
 테이블이 분할되지 않은 경우 이 필드가 비어 있습니다.  
  
 **파티션 구성표 매개 변수**  
 파티션 구성표에 포함되는 열의 이름을 표시합니다.  
  
 **테이블 열**  
 파티션 구성표에 매핑할 테이블 또는 뷰를 선택합니다.  
  
 **열 데이터 형식**  
 열의 데이터 형식을 표시합니다.  
  
> [!NOTE]  
>  테이블 열이 계산 열이면 **열 데이터 형식** 에 "계산 열"이 표시됩니다.  
  
 **인덱스를 이동하는 동안 DML 문의 온라인 처리 허용**  
 이 옵션을 사용하면 사용자는 인덱스 작업 중에 기본 테이블이나 클러스터형 인덱스 데이터 및 연관된 모든 비클러스터형 인덱스에 액세스할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 XML 인덱스에 대해서는 사용할 수 없으며 인덱스가 비활성화된 클러스터형 인덱스인 경우에도 사용할 수 없습니다.  
  
 **최대 병렬 처리 수준 설정**  
 병렬 계획 실행 중 사용할 프로세서 수를 제한합니다. 기본값인 0으로 설정하면 사용 가능한 실제 CPU 수를 사용합니다. 값을 1로 설정하면 병렬 계획이 생성되지 않습니다. 값을 1보다 큰 값으로 설정하면 단일 쿼리 실행에서 사용하는 최대 프로세서 수가 제한됩니다. 이 옵션은 대화 상자가 **다시 작성** 또는 **다시 만들기** 상태에 있을 때만 사용할 수 있습니다.  
  
> [!NOTE]  
>  사용 가능한 CPU 수보다 더 큰 수를 지정하면 사용 가능한 실제 CPU 수가 사용됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup"></a>기존 인덱스를 다른 파일 그룹으로 이동하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the TransactionsFG1 filegroup on the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP TransactionsFG1;  
    GO  
    /* Adds the TransactionsFG1dat3 file to the TransactionsFG1 filegroup. Please note that you will have to change the filename parameter in this statement to execute it without errors.  
    */  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = TransactionsFG1dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\TransactionsFG1dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP TransactionsFG1;  
    GO  
    /*Creates the IX_Employee_OrganizationLevel_OrganizationNode index  
      on the TransactionsPS1 filegroup and drops the original IX_Employee_OrganizationLevel_OrganizationNode index.  
    */  
    CREATE NONCLUSTERED INDEX IX_Employee_OrganizationLevel_OrganizationNode  
        ON HumanResources.Employee (OrganizationLevel, OrganizationNode)  
        WITH (DROP_EXISTING = ON)  
        ON TransactionsFG1;  
    GO  
    ```  
  
 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)를 참조하세요.  
  
  
