---
title: 데이터베이스 스냅샷 만들기(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], creating
ms.assetid: 187fbba3-c555-4030-9bdf-0f01994c5230
author: stevestein
ms.author: sstein
ms.openlocfilehash: a0acec2dd2e4e7e9d08d979febf85cf98f883e77
ms.sourcegitcommit: 5a03dc2bba481c2e2f03d67f6ee9486fc9f8ba95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71066873"
---
# <a name="create-a-database-snapshot-transact-sql"></a>Create a Database Snapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 스냅샷은 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용해서만 만들 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 데이터베이스 스냅샷 만들기를 지원하지 않습니다.  
  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 복구 모델을 사용할 수 있는 원본 데이터베이스는 다음 사전 요구 사항을 충족해야 합니다.  
  
-   서버 인스턴스는 데이터베이스 스냅샷을 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 실행해야 합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 데이터베이스 스냅샷 지원에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
-   데이터베이스 미러링 세션의 미러 데이터베이스가 아닌 경우 원본 데이터베이스는 온라인 상태여야 합니다.  
  
-   미러 데이터베이스에서 데이터베이스 스냅샷을 만들려면 데이터베이스가 동기화된 [미러링 상태](../../database-engine/database-mirroring/mirroring-states-sql-server.md)여야 합니다.  
  
-   원본 데이터베이스는 확장 가능한 공유 데이터베이스로 구성할 수 없습니다.  

- 원본 데이터베이스에는 MEMORY_OPTIMIZED_DATA 파일 그룹이 포함될 수 없습니다. 자세한 내용은 [메모리 내 OLTP에 대한 지원되지 않는 SQL Server 기능](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)을 참조하세요.

> [!IMPORTANT]
> 다른 주요 고려 사항에 대한 자세한 내용은 [데이터베이스 스냅샷&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.  
  
##  <a name="Recommendations"></a> 권장 사항  
 이 섹션에서는 다음과 같은 최상의 방법에 대해 설명합니다.  
  
-   [최선의 구현 방법: 데이터베이스 스냅샷 명명](#Naming)  
  
-   [최선의 구현 방법: 데이터베이스 스냅샷 수 제한](#Limiting_Number)  
  
-   [최선의 구현 방법: 데이터베이스 스냅샷에 대한 클라이언트 연결](#Client_Connections)  
  
####  <a name="Naming"></a> 최선의 구현 방법: 데이터베이스 스냅샷 명명  
 스냅샷의 이름은 중요하므로 스냅샷을 만들기 전에 고려해야 합니다. 각 데이터베이스 스냅샷에는 고유한 데이터베이스 이름이 필요합니다. 쉬운 관리를 위해 데이터베이스를 식별하는 다음과 같은 정보를 스냅샷 이름에 첨가할 수 있습니다.  
  
-   원본 데이터베이스의 이름입니다.  
  
-   스냅샷 이름임을 나타내는 부분  
  
-   스냅샷을 만든 날짜 및 시간, 시퀀스 번호, 자정 이후의 시간 등 지정된 데이터베이스에 대한 스냅샷 순서를 구분하기 위한 정보  
  
 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 일련의 스냅샷을 만든다고 가정합니다. 24시간 표기법을 기준으로 오전 6시와 오후 6시 사이에 6시간 간격으로 세 개의 일일 스냅숏을 만듭니다. 각 일일 스냅샷은 삭제 전 24시간 동안 보존되며 이후에 같은 이름의 새 스냅샷으로 대체됩니다. 각 스냅샷 이름은 날짜가 아닌 시간만 나타냅니다.  
  
```  
AdventureWorks_snapshot_0600  
AdventureWorks_snapshot_1200  
AdventureWorks_snapshot_1800  
```  
  
 이러한 일일 스냅샷을 만드는 시간이 일정하지 않을 경우 보다 덜 정확한 명명 규칙을 사용하는 것이 좋습니다. 예를 들면 다음과 같습니다.  
  
```  
AdventureWorks_snapshot_morning  
AdventureWorks_snapshot_noon  
AdventureWorks_snapshot_evening  
```  
  
#### <a name="Limiting_Number"></a> 최선의 구현 방법: 데이터베이스 스냅샷 수 제한  
 원본 데이터베이스의 순차적 스냅샷을 캡처하기 위해 일정 기간 동안 일련의 스냅샷을 만들 수 있습니다. 각 스냅샷은 명시적으로 삭제할 때까지 유지됩니다. 원본 페이지를 업데이트함에 따라 각 스냅샷의 크기도 증가하므로 새 스냅샷을 만든 후에는 디스크 공간 유지를 위해 기존의 스냅샷을 지울 수 있습니다.  
  

**참고!** 데이터베이스 스냅샷으로 되돌리려면 해당 데이터베이스의 다른 스냅샷을 삭제해야 합니다.  
  
####  <a name="Client_Connections"></a> 최선의 구현 방법: 데이터베이스 스냅샷에 대한 클라이언트 연결  
 클라이언트가 데이터베이스 스냅샷을 사용하려면 그 위치를 알아야 합니다. 사용자가 데이터베이스 스냅샷을 읽는 동안 다른 스냅샷이 생성되거나 삭제될 수 있습니다. 따라서 기존의 스냅샷을 새 스냅샷으로 대체하면 클라이언트를 새 스냅샷으로 리디렉션해야 합니다. 사용자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 이용해 수동으로 데이터베이스 스냅샷에 연결할 수 있습니다. 하지만 프로덕션 환경을 지원하려면 보고 및 작성 클라이언트를 자동으로 데이터베이스의 최신 데이터베이스 스냅샷으로 리디렉션하는 프로그래밍 솔루션을 만들어야 합니다.  
  

  
####  <a name="Permissions"></a> 사용 권한  
 데이터베이스를 만들 수 있는 모든 사용자는 데이터베이스 스냅샷을 만들 수 있습니다. 그러나 미러 데이터베이스의 스냅샷을 만들려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
##  <a name="TsqlProcedure"></a> 데이터베이스 스냅샷을 만드는 방법(Transact-SQL 사용)  
 **데이터베이스 스냅샷을 만들려면**  
  
>  이 프로시저의 예는 이 섹션의 뒷부분에 나오는 [예제(Transact-SQL)](#TsqlExample)을 참조하세요.  
  
1.  원본 데이터베이스의 현재 크기를 기준으로 데이터베이스 스냅샷을 저장할 수 있는 충분한 디스크 공간이 있는지 확인합니다. 데이터베이스 스냅샷의 최대 크기는 스냅샷을 생성할 때의 원본 데이터베이스 크기입니다. 자세한 내용은 [데이터베이스 스냅샷 스파스 파일의 크기 보기&#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)를 참조하세요.  
  
2.  AS SNAPSHOT OF 절을 사용하여 파일에서 CREATE DATABASE 문을 실행합니다. 스냅샷을 만들려면 원본 데이터베이스를 구성하는 모든 데이터베이스 파일의 논리적 이름을 지정해야 합니다. 구문은 다음과 같습니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     CREATE DATABASE *database_snapshot_name*  
  
     ON  
  
     (  
  
     NAME =*logical_file_name*,  
  
     FILENAME ='*os_file_name*'  
  
     ) [ ,...*n* ]  
  
     AS SNAPSHOT OF *source_database_name*  
  
     [;]  
  
     Where *source_**database_name* is the source database, *logical_file_name i*s the logical name used in SQL Server when referencing the file, *os_file_name* is the path and file name used by the operating system when you create the file, and *database_snapshot_name* is the name of the snapshot to which you want to revert the database. For a full description of this syntax, see [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
    > [!NOTE]  
    >  When you create a database snapshot, log files, offline files, restoring files, and defunct files are not allowed in the CREATE DATABASE statement.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
  
> [!NOTE]  
>  이 예에서 사용된 `.ss` 확장명은 임의로 지정됩니다.  
  
 이 섹션에서는 다음과 같은 예를 보여 줍니다.  
  
-   1\. [AdventureWorks 데이터베이스에 대한 스냅샷 만들기](#Creating_on_AW)  
  
-   2\. [Sales 데이터베이스에 대한 스냅샷 만들기](#Creating_on_Sales)
  
####  <a name="Creating_on_AW"></a> 1. AdventureWorks 데이터베이스에 대한 스냅샷 만들기  
 이 예에서는 `AdventureWorks` 데이터베이스에 대한 데이터베이스 스냅샷을 만듭니다. 스냅샷 이름 `AdventureWorks_dbss_1800` 및 스파스 파일의 파일 이름 `AdventureWorks_data_1800.ss`는 생성 시간이 오후 6시(18:00시)임을 나타냅니다.  
  
```  
CREATE DATABASE AdventureWorks_dbss1800 ON  
( NAME = AdventureWorks, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks_data_1800.ss' )  
AS SNAPSHOT OF AdventureWorks;  
GO  
```  
  
####  <a name="Creating_on_Sales"></a> 2. Sales 데이터베이스에 대한 스냅샷 만들기  
 이 예에서는 `sales_snapshot1200`데이터베이스에 대한 데이터베이스 스냅샷 `Sales` 을 만듭니다. 이 데이터베이스는 [CREATE DATABASE(SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)의 "파일 그룹을 가진 데이터베이스 만들기" 예제에서 만들었습니다.  
  
```  
--Creating sales_snapshot1200 as snapshot of the  
--Sales database:  
CREATE DATABASE sales_snapshot1200 ON  
( NAME = SPri1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SPri1dat_1200.ss'),  
( NAME = SPri2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SPri2dt_1200.ss'),  
( NAME = SGrp1Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\data\SG1Fi1dt_1200.ss'),  
( NAME = SGrp1Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SG1Fi2dt_1200.ss'),  
( NAME = SGrp2Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SG2Fi1dt_1200.ss'),  
( NAME = SGrp2Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\data\SG2Fi2dt_1200.ss')  
AS SNAPSHOT OF Sales;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 스냅샷 보기&#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [데이터베이스를 데이터베이스 스냅샷으로 되돌리기](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
-   [데이터베이스 스냅샷 삭제&#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [데이터베이스 스냅샷&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  

