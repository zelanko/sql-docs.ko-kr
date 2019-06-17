---
title: 새 위치로 파일 복원(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring files [SQL Server], how-to topics
- restoring databases [SQL Server], moving
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
ms.assetid: b4f4791d-646e-4632-9980-baae9cb1aade
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b30322bb48cfff6e0bca092d72aa9d5ad0990948
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875068"
---
# <a name="restore-files-to-a-new-location-sql-server"></a>새 위치로 파일 복원(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 파일을 새 위치에 복원하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 새 위치로 파일을 복원합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   파일을 복원하는 시스템 관리자는 복원될 데이터베이스를 현재 사용하고 있는 유일한 사람이어야 합니다.  
  
-   RESTORE는 명시적 또는 암시적 트랜잭션에서 사용할 수 없습니다.  
  
-   전체 복구 모델 또는 대량 로그 복구 모델의 경우 파일을 복원하려면 먼저 활성 트랜잭션 로그(비상 로그라고도 함)를 백업해야 합니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)을 사용하여 파일 및 파일 그룹을 복원하는 방법에 대해 설명합니다.  
  
-   암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-restore-files-to-a-new-location"></a>새 위치로 파일을 복원하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결하고 해당 인스턴스를 확장한 다음 **데이터베이스**를 확장합니다.  
  
2.  원하는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**, **복원**을 차례로 가리킨 다음 **파일 및 파일 그룹**을 클릭합니다.  
  
3.  **일반** 페이지의 **데이터베이스** 목록 상자에 복원할 데이터베이스를 입력합니다. 새 데이터베이스를 입력하거나 드롭다운 목록에서 기존 데이터베이스를 선택할 수 있습니다. 이 목록에는 시스템 데이터베이스인 **master** 및 **tempdb**를 제외한 서버의 모든 데이터베이스가 포함되어 있습니다.  
  
4.  복원할 백업 세트의 원본 및 위치를 지정하려면 다음 옵션 중 하나를 클릭합니다.  
  
    -   **데이터베이스**  
  
         목록 상자에 데이터베이스 이름을 입력합니다. 이 목록에는 **msdb** 백업 기록에 따라 백업된 데이터베이스만 포함되어 있습니다.  
  
    -   **장치**  
  
         찾아보기 단추를 클릭합니다. **백업 장치 지정** 대화 상자에서 **백업 미디어 유형** 목록 상자에 나열된 장치 유형 중 하나를 선택합니다. **백업 미디어** 목록 상자에서 하나 이상의 장치를 선택하려면 **추가**를 클릭합니다.  
  
         원하는 디바이스를 **백업 미디어** 목록 상자에 추가한 후 **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.  
  
5.  **복원에 사용할 백업 세트 선택** 표에서 복원할 백업을 선택합니다. 이 표는 지정한 위치에서 사용 가능한 백업을 표시합니다. 기본적으로 복구 계획이 제안됩니다. 제안된 복구 계획을 재정의하려면 표에서 선택 항목을 변경합니다. 선택 취소된 백업에 의존하는 모든 백업은 자동으로 선택 취소됩니다.  
  
    |열 머리글|값|  
    |-----------------|------------|  
    |**복원**|확인란이 선택되어 있으면 백업 세트가 복원됩니다.|  
    |**이름**|백업 세트의 이름입니다.|  
    |**파일 유형**|백업에서 데이터의 형식을 지정합니다. **데이터**하십시오 **로그**, 또는 **Filestream 데이터**입니다. 테이블에 포함된 데이터는 **데이터** 파일에 있고, 트랜잭션 로그 데이터는 **로그** 파일에 있으며, 파일 시스템에 저장되는 BLOB(Binary Large Object) 데이터는 **Filestream 데이터** 파일에 있습니다.|  
    |**형식**|수행 된 백업 유형: **전체**, **차등** 또는 **트랜잭션 로그**가 될 수 있습니다.|  
    |**Server**|백업 작업을 수행한 데이터베이스 엔진 인스턴스의 이름입니다.|  
    |**논리적 파일 이름**|파일의 논리적 이름입니다.|  
    |**데이터베이스 백업**|백업 작업과 관련된 데이터베이스의 이름입니다.|  
    |**Start Date**|클라이언트의 국가별 설정으로 표시되는 백업 작업 시작 날짜 및 시간입니다.|  
    |**완료 날짜**|클라이언트의 국가별 설정으로 표시되는 백업 작업 완료 날짜 및 시간입니다.|  
    |**크기**|백업 세트의 크기를 바이트 단위로 표시한 것입니다.|  
    |**사용자 이름**|백업 작업을 수행한 사용자의 이름입니다.|  
  
6.  **페이지 선택** 창에서 **옵션** 페이지를 클릭합니다.  
  
7.  **데이터베이스 파일을 다음으로 복원** 표에서 이동하려는 파일의 새 위치를 지정합니다.  
  
    |열 머리글|값|  
    |-----------------|------------|  
    |**원래 파일 이름**|원본 백업 파일의 전체 경로입니다.|  
    |**파일 유형**|백업에서 데이터의 형식을 지정합니다. **데이터**하십시오 **로그**, 또는 **Filestream 데이터**입니다. 테이블에 포함된 데이터는 **데이터** 파일에 있고, 트랜잭션 로그 데이터는 **로그** 파일에 있으며, 파일 시스템에 저장되는 BLOB(Binary Large Object) 데이터는 **Filestream 데이터** 파일에 있습니다.|  
    |**다음으로 복원**|복원할 데이터베이스 파일의 전체 경로입니다. 새 복원 파일을 지정하려면 입력란을 클릭하고 제안된 경로와 파일 이름을 편집합니다. **다음으로 복원** 열에서 경로 또는 파일 이름을 변경하는 것은 [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE 문에서 MOVE 옵션을 사용하는 것과 같습니다.|  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-restore-files-to-a-new-location"></a>새 위치로 파일을 복원하려면  
  
1.  필요에 따라 RESTORE FILELISTONLY 문을 실행하여 전체 데이터베이스 백업에 포함된 파일의 개수와 이름을 확인합니다.  
  
2.  RESTORE DATABASE 문을 실행하여 전체 데이터베이스 백업을 복원합니다. 이때 다음을 지정합니다.  
  
    -   복원할 데이터베이스의 이름  
  
    -   복원할 전체 데이터베이스 백업이 있는 백업 디바이스  
  
    -   새 위치로 각 파일을 복원하기 위한 MOVE 절  
  
    -   NORECOVERY 절  
  
3.  파일 백업을 만든 후에 파일이 수정된 경우에는 RESTORE LOG 문을 실행하여 트랜잭션 로그 백업을 적용합니다. 이때 다음을 지정합니다.  
  
    -   트랜잭션 로그가 적용될 데이터베이스의 이름  
  
    -   트랜잭션 로그 백업이 복원될 원본 백업 디바이스  
  
    -   현재 트랜잭션 로그 백업 다음에 적용할 다른 트랜잭션 로그 백업이 있으면 NORECOVERY 절을 지정하고 없으면 RECOVERY 절을 지정합니다.  
  
         트랜잭션 로그 백업이 적용되는 경우 파일과 파일 그룹을 백업한 시점이 포함되어야 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 원래 드라이브 C에 있었던 `MyNwind` 데이터베이스의 두 파일을 드라이브 D의 새 위치로 복원합니다. 두 트랜잭션 로그도 적용되어 데이터베이스를 현재 시간으로 복원합니다. `RESTORE FILELISTONLY` 문은 복원할 데이터베이스에 있는 파일의 수와 논리적/물리적 이름을 확인하는 데 사용합니다.  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
RESTORE FILELISTONLY  
   FROM MyNwind_1;  
-- Restore the files for MyNwind.  
RESTORE DATABASE MyNwind  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   MOVE 'MyNwind_data_1' TO 'D:\MyData\MyNwind_data_1.mdf',   
   MOVE 'MyNwind_data_2' TO 'D:\MyData\MyNwind_data_2.ndf';  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [백업 및 복원으로 데이터베이스 복사](../databases/copy-databases-with-backup-and-restore.md)   
 [파일 및 파일 그룹 복원&#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
  
