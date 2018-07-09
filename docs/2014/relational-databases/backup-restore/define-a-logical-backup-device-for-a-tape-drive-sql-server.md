---
title: 테이프 드라이브에 대한 논리적 백업 장치 정의(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- tape backup devices, creating
ms.assetid: 66f36e1d-0287-4fac-8a51-71f9f0d7ad5b
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 72651488293d52f0702d7c368ab0a704f74f8d5c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229263"
---
# <a name="define-a-logical-backup-device-for-a-tape-drive-sql-server"></a>테이프 드라이브에 대한 논리적 백업 장치 정의(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이프 드라이브에 대한 논리적 백업 장치를 정의하는 방법에 대해 설명합니다. 논리적 장치는 특정 물리적 백업 장치(디스크 파일 또는 테이프 드라이브)를 가리키는 사용자 정의 이름입니다.  물리적 장치의 초기화는 나중에 백업 장치에 백업이 기록될 때 수행됩니다.  
  
> [!NOTE]  
>  테이프 백업 장치에 대한 지원은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 테이프 드라이브에 대한 논리적 백업 장치를 정의합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   테이프 드라이브 또는 드라이브는 Microsoft Windows 운영 체제에 의해 지원되어야 합니다.  
  
-   테이프 장치는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 실행하는 컴퓨터에 물리적으로 연결되어 있어야 하며 원격 테이프 장치로 백업할 수 없습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 **diskadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
 디스크에 대한 쓰기 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>테이프 드라이브에 대한 논리적 백업 장치를 정의하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **서버 개체**를 확장한 다음 마우스 오른쪽 단추로 **백업 장치**를 클릭합니다.  
  
3.  **새 백업 장치**를 클릭하면 **백업 장치** 대화 상자가 열립니다.  
  
4.  장치 이름을 입력합니다.  
  
5.  대상에 대해 **테이프** 를 클릭하고 다른 백업 장치에 연결되어 있지 않은 테이프 드라이브를 선택합니다. 사용 가능한 테이프 드라이브가 없으면 **테이프** 옵션은 비활성 상태로 표시됩니다.  
  
6.  새 장치를 정의하려면 **확인**을 클릭합니다.  
  
 이 새 장치로 백업하려면 **데이터베이스 백업** 대화 상자의 **일반** 페이지에 있는 **백업할 위치:** 필드에 장치를 추가합니다. 자세한 내용은 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)에서 차등 데이터베이스 백업을 만듭니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>테이프 드라이브에 대한 논리적 백업 장치를 정의하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql) 를 사용하여 테이프의 논리적 백업 장치를 정의하는 방법을 보여 줍니다. 이 예에서는 `tapedump1`라는 물리적 이름으로 `\\.\tape0`이라는 테이프 백업 장치를 추가합니다.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [sys.backup_devices&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [sp_dropdevice&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)   
 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [디스크 파일에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [논리적 백업 장치의 속성 및 내용 보기&#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
