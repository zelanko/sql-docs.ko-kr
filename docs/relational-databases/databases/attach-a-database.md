---
title: 데이터베이스 연결 | Microsoft 문서
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql13.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d915c790d506fbc2b9290ece5b9d03f7666c4ee
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850951"
---
# <a name="attach-a-database"></a>데이터베이스 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 데이터베이스를 연결하는 방법에 대해 설명합니다. 이 기능을 사용하여 SQL Server 데이터베이스를 복사, 이동 또는 업그레이드할 수 있습니다.  
  
 
  
##  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   먼저 데이터베이스를 분리해야 합니다. 분리되지 않은 데이터베이스를 연결하려고 하면 오류가 반환됩니다. 자세한 내용은 [데이터베이스 분리](../../relational-databases/databases/detach-a-database.md)를 참조하세요.  
  
-   데이터베이스를 연결할 경우 모든 데이터 파일(MDF 및 LDF 파일)이 사용 가능해야 합니다. 데이터베이스가 처음 생성되었을 때 또는 마지막으로 연결되었을 때와 경로가 다른 데이터 파일이 있으면 해당 파일의 현재 경로를 지정해야 합니다.  
  
-   데이터베이스를 분리하는 경우 MDF 및 LDF 파일이 서로 다른 디렉터리에 있고 경로 중 하나에 \\\\?\GlobalRoot가 포함되어 있으면 작업이 실패합니다.  
  
###  <a name="Recommendations"></a> 연결하는 게 가장 좋은 방법일까요?  
 같은 인스턴스에서 데이터베이스 파일을 옮길 때는 분리와 연결 작업을 하는 대신 계획된 ALTER DATABASE 재배치 프로시저를 사용하여 데이터베이스를 옮기는 것이 좋습니다. 자세한 내용은 [Move User Databases](../../relational-databases/databases/move-user-databases.md)을 참조하세요. 
 
백업 및 복구에는 분리 및 연결 작업을 하지 않는 것이 좋습니다. 트랜잭션 로그 백업이 없으며 실수로 파일을 삭제할 수 있습니다.
  
###  <a name="Security"></a> 보안  
 파일 액세스 권한은 데이터베이스 분리, 연결 등의 여러 데이터베이스 작업 중에 설정됩니다. 데이터베이스를 분리 및 연결할 때마다 설정되는 파일 사용 권한에 대한 자세한 내용은 [온라인 설명서에서](http://technet.microsoft.com/library/ms189128.aspx) 데이터 및 로그 파일 보안 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 을 참조하세요(현재도 제공됨). 
  
 알 수 없거나 신뢰할 수 없는 출처의 데이터베이스는 연결 또는 복원하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요. 데이터베이스 연결에 대한 자세한 내용 및 데이터베이스를 연결할 때 메타데이터에 대해 이루어지는 변경에 대한 자세한 내용은 [데이터베이스 분리 및 연결(SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)을 참조하세요.  
  
####  <a name="Permissions"></a> Permissions  
 CREATE DATABASE, CREATE ANY DATABASE 또는 ALTER ANY DATABASE 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-attach-a-database"></a>데이터베이스를 연결하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 SSMS에서 해당 인스턴스 뷰를 클릭하여 확장합니다.  
  
2.  마우스 오른쪽 단추로 **데이터베이스** 를 클릭하고 **연결**을 클릭합니다.  
  
3.  **데이터베이스 연결** 대화 상자에서 연결할 데이터베이스를 지정하려면 **추가**를 클릭하고 **데이터베이스 파일 찾기** 대화 상자에서 데이터베이스가 있는 디스크 드라이브를 선택한 다음 디렉터리 트리를 확장하여 데이터베이스의 .mdf 파일을 선택합니다. 파일의 경로를 예로 들면 다음과 같습니다.  
  
     `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    >  이미 연결된 데이터베이스를 선택하려고 하면 오류가 발생합니다.  
  
     **연결할 데이터베이스**  
     선택한 데이터베이스에 대한 정보를 표시합니다.  
  
     \<열 머리글 없음>  
     연결 작업의 상태를 나타내는 아이콘을 표시합니다. 가능한 아이콘은 아래의 **상태** 에 대한 설명에 설명되어 있습니다.  
  
     **MDF 파일 위치**  
     선택한 MDF 파일의 경로와 파일 이름을 표시합니다.  
  
     **Database Name**  
     데이터베이스 이름을 표시합니다.  
  
     **다른 이름으로 연결**  
     필요에 따라 연결할 데이터베이스의 이름을 다른 이름으로 지정합니다.  
  
     **소유자**  
     필요에 따라 다른 소유자를 선택할 수 있도록 가능한 데이터베이스 소유자의 드롭다운 목록을 제공합니다.  
  
     **상태**  
     다음 표에 설명된 내용과 같이 데이터베이스의 상태를 표시합니다.  
  
    |아이콘|상태 텍스트|설명|  
    |----------|-----------------|-----------------|  
    |(아이콘 없음)|(텍스트 없음)|연결 작업이 시작되지 않았거나 이 개체에 대해 보류 중입니다. 대화 상자가 열려 있는 경우에 표시되는 기본 설정입니다.|  
    |녹색, 오른쪽 방향 삼각형|진행 중|연결 작업이 시작되었지만 아직 완료되지 않았습니다.|  
    |녹색 확인 표시|성공|개체가 성공적으로 연결되었습니다.|  
    |흰색 십자 표시가 있는 빨강 원|Error|연결 작업을 수행하는 동안 오류가 발생하여 완료하지 못했습니다.|  
    |오른쪽과 왼쪽에 두 개의 검정 사분면이 있고 위쪽과 아래쪽에 두 개의 흰색 사분면이 있는 원|중지됨|사용자가 작업을 중지하여 연결 작업이 완료되지 않았습니다.|  
    |시계 반대 방향을 가리키는 곡선 모양의 화살표가 있는 원|롤백됨|연결 작업이 성공적으로 완료되었지만 다른 개체를 연결하는 동안 발생한 오류로 인해 롤백되었습니다.|  
  
     **메시지**  
     빈 메시지 또는 "파일을 찾을 수 없습니다"라는 하이퍼링크를 표시합니다.  
  
     **추가**  
     필요한 기본 데이터베이스 파일을 찾습니다. 사용자가 .mdf 파일을 선택하면 **연결할 데이터베이스** 표의 각 필드에 적절한 정보가 자동으로 입력됩니다.  
  
     **제거**  
     선택한 파일을 **연결할 데이터베이스** 표에서 제거합니다.  
  
     **"** *<database_name>* **" 데이터베이스 정보**  
     연결할 파일의 이름을 표시합니다. 파일의 경로 이름을 확인하거나 변경하려면 **찾아보기** 단추(**…**)를 클릭합니다.  
  
    > [!NOTE]  
    >  파일이 없으면 **메시지** 열에 "찾을 수 없음"이 표시됩니다. 로그 파일을 찾을 수 없는 경우 다른 디렉터리에 있거나 삭제된 것입니다. 올바른 위치를 가리키도록 **데이터베이스 정보** 표의 파일 경로를 업데이트하거나 표에서 로그 파일을 제거해야 합니다. .ndf 데이터 파일을 찾을 수 없는 경우 올바른 위치를 가리키도록 표에서 해당 파일의 경로를 업데이트해야 합니다.  
  
     **원래 파일 이름**  
     데이터베이스에 속한 연결된 파일의 이름을 표시합니다.  
  
     **파일 유형**  
     파일의 형식( **데이터** 또는 **로그**)을 나타냅니다.  
  
     **현재 파일 경로**  
     선택한 데이터베이스 파일의 경로를 표시합니다. 이 경로는 직접 편집할 수 있습니다.  
  
     **메시지**  
     빈 메시지 또는 "**파일을 찾을 수 없습니다**"라는 하이퍼링크를 표시합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-attach-a-database"></a>데이터베이스를 연결하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  FOR ATTACH 절과 함께 [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) 문을 사용합니다.  
  
     다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 파일을 연결하고 데이터베이스 이름을 `MyAdventureWorks`로 바꿉니다.  
  
    ```  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
  
    ```  
  
    > [!NOTE]  
    >  또는 [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) 또는 [sp_attach_single_file_db](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md) 저장 프로시저를 사용할 수 있습니다. 그러나 이 프로시저는 이후 버전의 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. CREATE DATABASE를 사용하는 것이 좋습니다. FOR ATTACH 대신.  
  
##  <a name="FollowUp"></a> 후속 작업: SQL Server 데이터베이스를 업그레이드한 후  
 연결 방법을 사용하여 데이터베이스를 업그레이드하면 데이터베이스를 바로 사용할 수 있으며 자동으로 업그레이드됩니다. 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는 **전체 텍스트 업그레이드 옵션** 서버 속성의 설정에 따라 인덱스를 가져오거나, 다시 설정하거나, 다시 작성합니다. 업그레이드 옵션이 **가져오기** 또는 **다시 작성**으로 설정되어 있는 경우 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 **가져오기**로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다.  
  
 사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이면 업그레이드 후에도 동일하게 유지됩니다. 업그레이드 이전에 호환성 수준이 90이면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
  > [!NOTE]
  > CDC(변경 데이터 캡처)가 사용하도록 설정된 SQL Server 2014 이하를 실행하는 인스턴스에서 데이터베이스를 연결하는 경우 아래 명령을 실행하여 CDC(변경 데이터 캡처) 메타데이터도 업그레이드해야 합니다.
  ```
  USE <database name>
  EXEC sys.sp_cdc_vupgrade  
  ``` 
  
## <a name="see-also"></a>참고 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) 
 <br>[다른 서버에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리](manage-metadata-when-making-a-database-available-on-another-server.md)  
 [데이터베이스 분리](../../relational-databases/databases/detach-a-database.md)  
  
  
