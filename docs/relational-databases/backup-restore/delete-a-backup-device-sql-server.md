---
title: 백업 디바이스 삭제(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], deleting devices
- backup devices [SQL Server], deleting
- deleting backup devices
- removing backup devices
- backing up databases [SQL Server], backup devices
ms.assetid: 7be62480-ed6a-4262-a071-1feba73b1c02
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: be32e40cdba72ebd544758b395cb125deb05297b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68075912"
---
# <a name="delete-a-backup-device-sql-server"></a>백업 디바이스 삭제(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 백업 디바이스를 삭제하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 백업 디바이스를 삭제합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 **diskadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-backup-device"></a>백업 디바이스를 삭제하려면  
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **서버 개체**를 확장한 다음 **백업 디바이스**를 확장합니다.  
  
3.  원하는 디바이스를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
4.  **개체 삭제** 대화 상자에서 올바른 디바이스 이름이 **개체 이름** 열에 표시되는지 확인합니다.  
  
5.  **확인**을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-backup-device"></a>백업 디바이스를 삭제하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리에 붙여 넣습니다. 이 예에서는 [sp_dropdevice](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md) 를 사용하여 백업 디바이스를 삭제하는 방법에 대해 설명합니다. `mybackupdisk` 백업 디바이스와 실제 이름 `c:\backup\backup1.bak`를 만들려면 첫 번째 예를 실행합니다. **백업 디바이스를 삭제하려면** sp_dropdevice `mybackupdisk` 를 실행합니다. `delfile` 매개 변수는 물리적 이름을 삭제합니다.  
  
```sql  
--Define a backup device and physical name.   
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'disk', 'mybackupdisk', 'c:\backup\backup1.bak' ;  
GO  
--Delete the backup device and the physical name.  
USE AdventureWorks2012 ;  
GO  
EXEC sp_dropdevice ' mybackupdisk ', 'delfile' ;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [논리적 백업 디바이스의 속성 및 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [sys.backup_devices&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)  
  
  
