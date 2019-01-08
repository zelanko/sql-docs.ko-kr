---
title: 데이터베이스 스냅숏 만들기(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], creating
ms.assetid: 187fbba3-c555-4030-9bdf-0f01994c5230
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f577f7798da2ba7b7ee4259ecc98994f713cfc5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52768335"
---
# <a name="create-a-database-snapshot-transact-sql"></a>데이터베이스 스냅숏 만들기(Transact-SQL)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 스냅숏은 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용해서만 만들 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 데이터베이스 스냅숏 만들기를 지원하지 않습니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
     [최선의 구현 방법: 데이터베이스 스냅숏 명명](#Naming)  
  
-   **스냅숏을 사용 하 여 데이터베이스를 만들려면:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 복구 모델을 사용할 수 있는 원본 데이터베이스는 다음 사전 요구 사항을 충족해야 합니다.  
  
-   서버 인스턴스는 데이터베이스 스냅숏을 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 실행해야 합니다. 데이터베이스 스냅숏 지원에 대 한 자세한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
-   데이터베이스 미러링 세션의 미러 데이터베이스가 아닌 경우 원본 데이터베이스는 온라인 상태여야 합니다.  
  
-   미러 데이터베이스에서 데이터베이스 스냅숏을 만들려면 데이터베이스가 동기화된[미러링 상태](../../database-engine/database-mirroring/mirroring-states-sql-server.md)여야 합니다.  
  
-   원본 데이터베이스는 확장 가능한 공유 데이터베이스로 구성할 수 없습니다.  
  
> [!IMPORTANT]  
>  다른 주요 고려 사항에 대한 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](database-snapshots-sql-server.md)을 사용해서만 만들 수 있습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
 이 섹션에서는 다음과 같은 최상의 방법에 대해 설명합니다.  
  
-   [최선의 구현 방법: 데이터베이스 스냅숏 명명](#Naming)  
  
-   [최선의 구현 방법: 데이터베이스 스냅숏 수 제한](#Limiting_Number)  
  
-   [최선의 구현 방법: 데이터베이스 스냅숏에 대 한 클라이언트 연결](#Client_Connections)  
  
####  <a name="Naming"></a> 최선의 구현 방법: 데이터베이스 스냅숏 명명  
 스냅숏의 이름은 중요하므로 스냅숏을 만들기 전에 고려해야 합니다. 각 데이터베이스 스냅숏에는 고유한 데이터베이스 이름이 필요합니다. 쉬운 관리를 위해 데이터베이스를 식별하는 다음과 같은 정보를 스냅숏 이름에 첨가할 수 있습니다.  
  
-   원본 데이터베이스의 이름입니다.  
  
-   스냅숏 이름임을 나타내는 부분  
  
-   스냅숏을 만든 날짜 및 시간, 시퀀스 번호, 자정 이후의 시간 등 지정된 데이터베이스에 대한 스냅숏 순서를 구분하기 위한 정보  
  
 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 일련의 스냅숏을 만든다고 가정합니다. 24시간 표기법을 기준으로 오전 6시와 오후 6시 사이에 6시간 간격으로 세 개의 일일 스냅숏을 만듭니다. 각 일일 스냅숏은 삭제 전 24시간 동안 보존되며 이후에 같은 이름의 새 스냅숏으로 대체됩니다. 각 스냅숏 이름은 날짜가 아닌 시간만 나타냅니다.  
  
```  
AdventureWorks_snapshot_0600  
AdventureWorks_snapshot_1200  
AdventureWorks_snapshot_1800  
```  
  
 이러한 일일 스냅숏을 만드는 시간이 일정하지 않을 경우 보다 덜 정확한 명명 규칙을 사용하는 것이 좋습니다. 예를 들면 다음과 같습니다.  
  
```  
AdventureWorks_snapshot_morning  
AdventureWorks_snapshot_noon  
AdventureWorks_snapshot_evening  
```  
  
####  <a name="Limiting_Number"></a> 최선의 구현 방법: 데이터베이스 스냅숏 수 제한  
 원본 데이터베이스의 순차적 스냅숏을 캡처하기 위해 일정 기간 동안 일련의 스냅숏을 만들 수 있습니다. 각 스냅숏은 명시적으로 삭제할 때까지 유지됩니다. 원본 페이지를 업데이트함에 따라 각 스냅숏의 크기도 증가하므로 새 스냅숏을 만든 후에는 디스크 공간 유지를 위해 기존의 스냅숏을 지울 수 있습니다.  
  
> [!NOTE]  
>  데이터베이스를 스냅숏으로 되돌리기 위해서는 해당 데이터베이스의 다른 스냅숏을 삭제해야 합니다.  
  
####  <a name="Client_Connections"></a> 최선의 구현 방법: 데이터베이스 스냅숏에 대한 클라이언트 연결  
 클라이언트가 데이터베이스 스냅숏을 사용하려면 그 위치를 알아야 합니다. 사용자가 데이터베이스 스냅숏을 읽는 동안 다른 스냅숏이 생성되거나 삭제될 수 있습니다. 따라서 기존의 스냅숏을 새 스냅숏으로 대체하면 클라이언트를 새 스냅숏으로 리디렉션해야 합니다. 사용자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 이용해 수동으로 데이터베이스 스냅숏에 연결할 수 있습니다. 하지만 프로덕션 환경을 지원하려면 보고 및 작성 클라이언트를 자동으로 데이터베이스의 최신 데이터베이스 스냅숏으로 리디렉션하는 프로그래밍 솔루션을 만들어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스를 만들 수 있는 모든 사용자는 데이터베이스 스냅숏을 만들 수 있습니다. 그러나 미러 데이터베이스의 스냅숏을 만들려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
##  <a name="TsqlProcedure"></a> 데이터베이스 스냅숏을 만드는 방법(Transact-SQL 사용)  
 **데이터베이스 스냅숏을 만들려면**  
  
> [!NOTE]  
>  이 프로시저의 예는 이 섹션의 뒷부분에 나오는 [예제(Transact-SQL)](#TsqlExample)을 참조하세요.  
  
1.  원본 데이터베이스의 현재 크기를 기준으로 데이터베이스 스냅숏을 저장할 수 있는 충분한 디스크 공간이 있는지 확인합니다. 데이터베이스 스냅숏의 최대 크기는 스냅숏을 생성할 때의 원본 데이터베이스 크기입니다. 자세한 내용은 [데이터베이스 스냅숏 스파스 파일의 크기 보기&#40;Transact-SQL&#41;](view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)를 참조하세요.  
  
2.  AS SNAPSHOT OF 절을 사용하여 파일에서 CREATE DATABASE 문을 실행합니다. 스냅숏을 만들려면 원본 데이터베이스를 구성하는 모든 데이터베이스 파일의 논리적 이름을 지정해야 합니다. 구문은 다음과 같습니다.  
  
     CREATE DATABASE *database_snapshot_name*  
  
     ON  
  
     (  
  
     NAME =*logical_file_name*,  
  
     FILENAME ='*os_file_name*'  
  
     ) [ ,...*n* ]  
  
     AS SNAPSHOT OF *source_database_name*  
  
     [;]  
  
     여기서 *source_**database_name*은 원본 데이터베이스이고, *logical_file_name*은 SQL Server에서 파일을 참조할 때 사용되는 논리적 이름이고, *os_file_name*은 운영 체제에서 파일을 만드는 데 사용되는 경로 및 파일 이름이고, *database_snapshot_name*은 데이터베이스를 되돌릴 스냅숏의 이름입니다. 이 구문에 대한 자세한 내용은 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)을 사용해서만 만들 수 있습니다.  
  
    > [!NOTE]  
    >  데이터베이스 스냅숏을 만들 때 로그 파일, 오프라인 파일, 복원 파일 및 존재하지 않는 파일은 CREATE DATABASE 문에 사용할 수 없습니다.  
  
###  <a name="TsqlExample"></a> 예제(Transact-SQL)  
  
> [!NOTE]  
>  이 예에서 사용된 `.ss` 확장명은 임의로 지정됩니다.  
  
 이 섹션에서는 다음과 같은 예를 보여 줍니다.  
  
-   1. [AdventureWorks 데이터베이스에 대한 스냅숏 만들기](#Creating_on_AW)  
  
-   2. [Sales 데이터베이스에 대한 스냅숏 만들기](#Creating_on_Sales)  
  
####  <a name="Creating_on_AW"></a> 1. AdventureWorks 데이터베이스에 대한 스냅숏 만들기  
 이 예에서는 `AdventureWorks` 데이터베이스에 대한 데이터베이스 스냅숏을 만듭니다. 스냅숏 이름 `AdventureWorks_dbss_1800`및 스파스 파일의 파일 이름 `AdventureWorks_data_1800.ss`는 생성 시간이 오후 6시(18:00시)임을 나타냅니다.  
  
```  
CREATE DATABASE AdventureWorks_dbss1800 ON  
( NAME = AdventureWorks_Data, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data\AdventureWorks_data_1800.ss' )  
AS SNAPSHOT OF AdventureWorks;  
GO  
```  
  
####  <a name="Creating_on_Sales"></a> 2. Sales 데이터베이스에 대한 스냅숏 만들기  
 이 예에서는 `sales_snapshot1200`데이터베이스에 대한 데이터베이스 스냅숏 `Sales` 을 만듭니다. 이 데이터베이스에서 "파일 그룹을 가진 데이터베이스 만들기" 예에서 만들었습니다 [데이터베이스 만들기 &#40;SQL Server TRANSACT-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)합니다.  
  
```  
--Creating sales_snapshot1200 as snapshot of the  
--Sales database:  
CREATE DATABASE sales_snapshot1200 ON  
( NAME = SPri1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SPri1dat_1200.ss'),  
( NAME = SPri2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SPri2dt_1200.ss'),  
( NAME = SGrp1Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\mssql\data\SG1Fi1dt_1200.ss'),  
( NAME = SGrp1Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG1Fi2dt_1200.ss'),  
( NAME = SGrp2Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG2Fi1dt_1200.ss'),  
( NAME = SGrp2Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG2Fi2dt_1200.ss')  
AS SNAPSHOT OF Sales;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [데이터베이스 스냅숏 보기&#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [데이터베이스를 데이터베이스 스냅숏으로 되돌리기](revert-a-database-to-a-database-snapshot.md)  
  
-   [데이터베이스 스냅숏 삭제&#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [데이터베이스 스냅숏&#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
