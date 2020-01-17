---
title: 논리적 백업 디바이스 정의 - 디스크
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], disks
- disk backup devices [SQL Server]
- database backups [SQL Server], disks
- backing up databases [SQL Server], disks
ms.assetid: 86331d43-c738-4523-ae3d-7d6700348ed1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6f628da66345668768aae1fe2de29596082ae6fa
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255945"
---
# <a name="define-a-logical-backup-device-for-a-disk-file-sql-server"></a>Define a Logical Backup Device for a Disk File (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 디스크 파일에 대한 논리적 백업 디바이스를 정의하는 방법에 대해 설명합니다. 논리적 디바이스는 특정 물리적 백업 디바이스(디스크 파일 또는 테이프 드라이브)를 가리키는 사용자 정의 이름입니다.  물리적 디바이스의 초기화는 나중에 백업 디바이스에 백업이 기록될 때 수행됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 디스크 파일에 대해 논리적 백업 디바이스를 정의합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   논리적 디바이스 이름은 서버 인스턴스의 모든 논리적 백업 디바이스에서 고유해야 합니다. 기존의 논리적 디바이스 이름을 보려면 [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) 카탈로그 뷰를 쿼리합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   데이터베이스 데이터 및 로그 디스크가 아닌 다른 디스크를 백업 디스크로 사용하는 것이 좋습니다. 이렇게 하면 데이터 또는 로그 디스크가 실패할 경우 백업에 액세스할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 **diskadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
 디스크에 대한 쓰기 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-define-a-logical-backup-device-for-a-disk-file"></a>디스크 파일에 대해 논리적 백업 디바이스를 정의하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 후 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **서버 개체**를 확장한 다음 **백업 디바이스**를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **새 백업 디바이스**를 클릭합니다. **백업 디바이스** 대화 상자가 열립니다.  
  
4.  디바이스 이름을 입력합니다.  
  
5.  대상으로 **파일** 을 클릭하고 파일의 전체 경로를 지정합니다.  
  
6.  새 디바이스를 정의하려면 **확인**을 클릭합니다.  
  
 이 새 디바이스로 백업하려면 **데이터베이스 백업** 대화 상자의 **일반** 페이지에 있는**백업할 위치:** 필드에 디바이스를 추가합니다. 자세한 내용은 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)에서 차등 데이터베이스 백업을 만듭니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-define-a-logical-backup-for-a-disk-file"></a>디스크 파일에 대해 논리적 백업을 정의하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) 를 사용하여 디스크 파일의 논리적 백업 디바이스를 정의하는 방법을 보여 줍니다. 이 예에서는 `mydiskdump``c:\dump\dump1.bak`라는 디스크 백업 디바이스를 추가합니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sys.backup_devices&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [테이프 드라이브에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [논리적 백업 디바이스의 속성 및 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
