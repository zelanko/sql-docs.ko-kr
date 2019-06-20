---
title: 다른 컴퓨터로 보고서 서버 데이터베이스 이동(SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 44a9854d-e333-44f6-bdc7-8837b9f34416
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a92fea73d84bc28f09951120e763b602586e7069
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103714"
---
# <a name="moving-the-report-server-databases-to-another-computer-ssrs-native-mode"></a>다른 컴퓨터로 보고서 서버 데이터베이스 이동(SSRS 기본 모드)
   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 설치에 사용되는 보고서 서버 데이터베이스를 다른 컴퓨터에 있는 인스턴스로 이동할 수 있습니다. reportserver 데이터베이스와 reportservertempdb 데이터베이스를 모두 이동하거나 함께 복사해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치하려면 두 데이터베이스가 모두 필요합니다. reportservertempdb 데이터베이스는 이동하는 주 reportserver 데이터베이스와 이름으로 관련되어야 합니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 데이터베이스를 이동해도 보고서 서버 항목에 대해 현재 정의되어 있는 예약된 작업에는 영향을 주지 않습니다.  
  
-   일정은 보고서 서버 서비스를 처음으로 다시 시작할 때 다시 만들어집니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 새 데이터베이스 인스턴스에서 다시 만들어집니다. 해당 작업을 새 컴퓨터로 이동하지 않아도 되지만 더 이상 사용되지 않을 컴퓨터 작업은 삭제할 수 있습니다.  
  
-   구독, 캐시된 보고서 및 스냅숏은 이동된 데이터베이스에 그대로 유지됩니다. 데이터베이스를 이동한 후 스냅숏이 새로 고친 데이터를 가져오지 않은 경우 보고서 관리자에서 스냅숏 옵션의 선택을 취소하고 **적용** 을 클릭하여 변경 내용을 저장합니다. 그런 다음 일정을 다시 만들고 **적용** 을 클릭하여 변경 내용을 저장합니다.  
  
-   reportservertempdb에 저장된 임시 보고서 및 사용자 세션 데이터는 해당 데이터베이스를 이동해도 그대로 유지됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 백업 및 복원, 연결 및 분리, 복사를 비롯한 여러 가지 방법으로 데이터베이스를 이동할 수 있습니다. 기존 데이터베이스 위치를 새 서버 인스턴스로 다시 지정하는 데 이러한 방법이 모두 적합한 것은 아닙니다. 보고서 서버 데이터베이스를 이동하는 데 사용해야 하는 방법은 시스템 가용성 요구 사항에 따라 달라집니다. 보고서 서버 데이터베이스를 이동하는 가장 쉬운 방법은 데이터베이스를 분리 후 연결하는 것입니다. 그러나 이 방법을 사용하려면 데이터베이스를 분리하는 동안 보고서 서버를 오프라인 상태로 설정해야 합니다. 서비스 장애를 최소화하려면 백업 및 복원을 사용하는 것이 낫지만 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행하여 작업을 수행해야 합니다. 데이터베이스 복사 마법사를 사용하여 데이터베이스를 복사할 경우 데이터베이스의 사용 권한 설정이 유지되지 않으므로 이 방법은 사용하지 않는 것이 좋습니다.  
  
> [!IMPORTANT]  
>  이 항목에 설명된 단계는 기존 설치에서 보고서 서버 데이터베이스를 재배치하는 작업만 수행하려는 경우에 사용하는 것이 좋습니다. 전체 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 마이그레이션하려면, 즉 데이터베이스를 이동하고 해당 데이터베이스를 사용하는 보고서 서버 Windows 서비스의 ID를 변경하려면 연결을 다시 구성하고 암호화 키를 다시 설정해야 합니다.  
  
## <a name="detaching-and-attaching-the-report-server-databases"></a>보고서 서버 데이터베이스 분리 및 연결  
 보고서 서버를 오프라인 상태로 만들 수 있는 경우 데이터베이스를 분리한 후 사용하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 이동할 수 있습니다. 이 방법을 사용하면 데이터베이스의 사용 권한이 유지됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스를 사용하는 경우 이를 다른 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스로 이동해야 합니다. 데이터베이스를 이동한 후에는 보고서 서버와 보고서 서버 데이터베이스의 연결을 다시 구성해야 합니다. 스케일 아웃 배포를 실행하려면 배포 환경의 각 보고서 서버에 대한 보고서 서버 데이터베이스 연결을 다시 구성해야 합니다.  
  
 다음 단계에 따라 데이터베이스를 이동하십시오.  
  
1.  이동하려는 보고서 서버 데이터베이스의 암호화 키를 백업합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 키를 백업할 수 있습니다.  
  
2.  보고서 서버 서비스를 중지합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 서비스를 중지할 수 있습니다.  
  
3.   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 시작하고 보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 엽니다.  
  
4.  보고서 서버 데이터베이스를 마우스 오른쪽 단추로 클릭하고 태스크를 가리킨 다음 **분리**를 클릭합니다. 보고서 서버 임시 데이터베이스에 대해 이 단계를 반복합니다.  
  
5.  사용하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터 폴더로 .mdf 및 .ldf 파일을 복사하거나 이동합니다. 두 개의 데이터베이스를 이동하고 있으므로 이동하거나 복사하는 파일이 모두 네 개인지 확인합니다.  
  
6.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 보고서 서버 데이터베이스를 호스팅할 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 엽니다.  
  
7.  데이터베이스 노드를 마우스 오른쪽 단추로 클릭한 다음 **연결**을 클릭합니다.  
  
8.  **추가** 를 클릭하고 연결할 보고서 서버 데이터베이스 .mdf 및 .ldf 파일을 선택합니다. 보고서 서버 임시 데이터베이스에 대해 이 단계를 반복합니다.  
  
9. 데이터베이스 연결 되 면 확인을 `RSExecRole` 은 보고서 서버 데이터베이스와 임시 데이터베이스의 데이터베이스 역할. `RSExecRole` select, insert, update, delete 및 참조 권한과 보고서 서버 데이터베이스 테이블에 있어야 하 고 저장된 프로시저에 대 한 실행 해야 합니다. 자세한 내용은 [RSExecRole 만들기](../security/create-the-rsexecrole.md)를 참조하세요.  
  
10. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작하고 보고서 서버에 대한 연결을 엽니다.  
  
11. 데이터베이스 페이지에서 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택한 다음 **연결**을 클릭합니다.  
  
12. 방금 이동한 보고서 서버 데이터베이스를 선택한 다음 **적용**을 클릭합니다.  
  
13. 암호화 키 페이지에서 복원을 클릭합니다. 키의 백업 복사본이 들어 있는 파일과 파일의 잠금을 해제하기 위한 암호를 지정합니다.  
  
14. 보고서 서버 서비스를 다시 시작합니다.  
  
## <a name="backing-up-and-restoring-the-report-server-databases"></a>보고서 서버 데이터베이스 백업 및 복원  
 보고서 서버를 오프라인으로 설정할 수 없는 경우 백업 후 복원 방법을 사용하여 보고서 서버 데이터베이스 위치를 다시 지정할 수 있습니다. 백업 및 복원을 수행하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용해야 합니다. 데이터베이스를 복원한 후에 새 서버 인스턴스의 데이터베이스를 사용하도록 보고서 서버를 구성해야 합니다. 자세한 내용은 이 항목의 마지막 부분에 있는 지침을 참조하십시오.  
  
### <a name="using-backup-and-copyonly-to-backup-the-report-server-databases"></a>BACKUP 및 COPY_ALL을 사용하여 보고서 서버 데이터베이스 백업  
 데이터베이스를 백업할 때는 COPY_ONLY 인수를 설정합니다. 두 데이터베이스와 로그 파일을 모두 백업해야 합니다.  
  
```  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServer  
   SET RECOVERY FULL  
  
-- If the ReportServerData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerData',   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\BACKUP\ReportServerData.bak'  
  
-- Create a logical backup device, ReportServerLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\BACKUP\ReportServerLog.bak'  
  
-- Back up the full ReportServer database.  
BACKUP DATABASE ReportServer  
   TO ReportServerData  
   WITH COPY_ONLY  
  
-- Back up the ReportServer log.  
BACKUP LOG ReportServer  
   TO ReportServerLog  
   WITH COPY_ONLY  
  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServerTempdb  
   SET RECOVERY FULL  
  
-- If the ReportServerTempDBData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBData',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBData.bak'  
  
-- Create a logical backup device, ReportServerTempDBLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBLog.bak'  
  
-- Back up the full ReportServerTempDB database.  
BACKUP DATABASE ReportServerTempDB  
   TO ReportServerTempDBData  
   WITH COPY_ONLY  
  
-- Back up the ReportServerTempDB log.  
BACKUP LOG ReportServerTempDB  
   TO ReportServerTempDBLog  
   WITH COPY_ONLY  
```  
  
### <a name="using-restore-and-move-to-relocate-the-report-server-databases"></a>RESTORE 및 MOVE를 사용하여 보고서 서버 데이터베이스 위치 다시 지정  
 데이터베이스를 복원할 때는 경로를 지정할 수 있도록 MOVE 인수를 포함해야 합니다. NORECOVERY 인수를 사용하여 초기 복원을 수행합니다. 이렇게 하면 데이터베이스의 상태가 RESTORING으로 유지되므로 로그 백업을 검토하여 복원할 사항을 결정할 수 있습니다. 마지막 단계는 RECOVERY 인수를 사용하여 RESTORE 작업을 반복하는 것입니다.  
  
 MOVE 인수에는 데이터 파일의 논리적 이름을 사용합니다. 논리적 이름을 찾으려면 `RESTORE FILELISTONLY FROM DISK='C:\ReportServerData.bak';`  
  
 다음 예에는 복원할 로그 파일의 위치를 지정할 수 있도록 FILE 인수가 포함되어 있습니다. 파일 위치를 찾으려면 `RESTORE HEADERONLY FROM DISK='C:\ReportServerData.bak';`  
  
 데이터베이스와 로그 파일을 복원할 때 RESTORE 작업을 각각 별도로 실행해야 합니다.  
  
```  
-- Restore the report server database and move to new instance folder   
RESTORE DATABASE ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore the report server log file to new instance folder   
RESTORE LOG ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore and move the report server temporary database  
RESTORE DATABASE ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Restore the temporary database log file to new instance folder   
RESTORE LOG ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServer  
   WITH RECOVERY  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServerTempDB  
   WITH RECOVERY  
GO  
```  
  
### <a name="how-to-configure-the-report-server-database-connection"></a>보고서 서버 데이터베이스 연결을 구성하는 방법  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작하고 보고서 서버에 대한 연결을 엽니다.  
  
2.  데이터베이스 페이지에서 **데이터베이스 변경**을 클릭합니다. **다음**을 클릭합니다.  
  
3.  **기존 보고서 서버 데이터베이스 선택**을 클릭합니다. **다음**을 클릭합니다.  
  
4.  이제 보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택하고 **연결 테스트**를 클릭합니다. **다음**을 클릭합니다.  
  
5.  데이터베이스 이름에서 사용하려는 보고서 서버 데이터베이스를 선택합니다. **다음**을 클릭합니다.  
  
6.  자격 증명에 보고서 서버가 보고서 서버 데이터베이스에 연결하는 데 사용할 자격 증명을 지정합니다. **다음**을 클릭합니다.  
  
7.  **다음** , **마침**을 차례로 클릭합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 설치하려면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 `RSExecRole` 역할을 포함해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 통해 보고서 서버 데이터베이스 연결을 설정하면 역할 만들기, 로그인 등록 및 역할 할당이 발생합니다. rsconfig.exe 명령 프롬프트 유틸리티를 사용하는 등 다른 방법을 사용하여 연결을 구성하면 보고서 서버가 작동 상태에 있지 않게 됩니다. 이 경우 WMI 코드를 작성하여 보고서 서버를 사용할 수 있게 만들어야 할 수 있습니다. 자세한 내용은 [Reporting Services WMI 공급자 액세스](../tools/access-the-reporting-services-wmi-provider.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [RSExecRole 만들기](../security/create-the-rsexecrole.md)   
 [보고서 서버 서비스 시작 및 중지](start-and-stop-the-report-server-service.md)   
 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [rsconfig 유틸리티&#40;SSRS&#41;](../tools/rsconfig-utility-ssrs.md)   
 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [보고서 서버 데이터베이스&#40;SSRS 기본 모드&#41;](report-server-database-ssrs-native-mode.md)  
  
  
