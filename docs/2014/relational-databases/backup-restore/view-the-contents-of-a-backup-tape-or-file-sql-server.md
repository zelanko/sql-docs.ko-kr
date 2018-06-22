---
title: 백업 테이프 또는 파일의 내용 보기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- backup devices [SQL Server], tapes
- displaying backup content
- viewing backup content
- tape backup devices, viewing contents
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
ms.assetid: cd6674a2-ca55-4b5a-a971-878ba001821e
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2de426df5c39c005d6e723e9ef1a57a40796952b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081110"
---
# <a name="view-the-contents-of-a-backup-tape-or-file-sql-server"></a>백업 테이프 또는 파일의 내용 보기(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 백업 테이프 또는 파일의 내용을 보는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  테이프 백업 장치에 대한 지원은 나중 버전의 SQL Server에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 백업 테이프 또는 파일의 내용을 봅니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 보안에 대한 자세한 내용은 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)를 참조하세요.  
  
####  <a name="Permissions"></a> 사용 권한  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 백업 세트나 백업 장치에 대한 정보를 얻으려면 CREATE DATABASE 권한이 필요합니다. 자세한 내용은 [GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>백업 테이프 또는 파일의 내용을 보려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  백업하려는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  
  
4.  **일반** 페이지의 **대상** 섹션에서 **디스크** 또는 **테이프**를 클릭합니다. **백업할 위치** 목록 상자에서 디스크 파일 또는 테이프를 찾습니다.  
  
     목록 상자에 디스크 파일 또는 테이프가 표시되지 않으면 **추가**를 클릭합니다. 파일 이름 또는 테이프 드라이브를 선택합니다. **확인** 을 클릭하여 **백업할 위치**목록 상자에 추가합니다.  
  
5.  **백업할 위치** 목록 상자에서 보려는 디스크 또는 테이프 드라이브의 경로를 선택한 다음 **내용**을 클릭합니다. **장치 내용** 대화 상자가 열립니다.  
  
6.  선택한 테이프 또는 파일의 미디어 세트 및 백업 세트에 대한 정보가 오른쪽 창에 표시됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>백업 테이프 또는 파일의 내용을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) 문을 사용합니다. 이 예에서는 `AdventureWorks2012-FullBackup.bak`라는 파일에 대한 정보를 반환합니다.  
  
```tsql  
USE AdventureWorks2012;  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks2012-FullBackup.bak' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [backupfilegroup&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [backupset&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [디스크 파일에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [테이프 드라이브에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  
