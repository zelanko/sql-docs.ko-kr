---
title: "논리적 백업 장치의 속성 및 내용 보기(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying backup content
- viewing backup content
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
- backing up databases [SQL Server], properties
- displaying backup properties
- backup devices [SQL Server], viewing information
- viewing backup properties
- database backups [SQL Server], properties
ms.assetid: 3a309074-e816-454d-b6c3-fcfdde0cbf74
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1e0a3fad1cc54f9367d95ac36c903deeede0814b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>논리적 백업 장치의 속성 및 내용 보기(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 논리적 백업 장치의 속성과 내용을 보는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **논리적 백업 장치의 속성과 내용을 보려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
 보안에 대한 자세한 내용은 [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)를 참조하세요.  
  
####  <a name="Permissions"></a> 사용 권한  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 백업 세트나 백업 장치에 대한 정보를 얻으려면 CREATE DATABASE 권한이 필요합니다. 자세한 내용은 [GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>논리적 백업 장치의 속성과 내용을 보려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **서버 개체**를 확장한 다음 **백업 장치**를 확장합니다.  
  
3.  장치를 클릭하고 **속성**을 마우스 오른쪽 단추로 클릭하면 **백업 장치** 대화 상자가 열립니다.  
  
4.  **일반** 페이지에 장치 이름과 대상이 표시됩니다. 대상은 테이프 장치이거나 파일 경로입니다.  
  
5.  **페이지 선택** 페이지에서 **미디어 내용**을 클릭합니다.  
  
6.  다음과 같은 속성 패널에 오른쪽 창이 표시됩니다.  
  
    -   **미디어**  
  
         미디어 시퀀스 번호, 패밀리 시퀀스 번호, 미러 ID(있는 경우) 등의 미디어 시퀀스 정보 및 미디어를 만든 날짜와 시간  
  
    -   **미디어 세트**  
  
         미디어 세트 정보: 미디어 세트 이름과 설명(있는 경우) 및 미디어 세트에 있는 패밀리 수  
  
7.  **백업 세트** 표에는 미디어 세트 내용에 대한 정보가 표시됩니다.  
  
> [!NOTE]  
>  자세한 내용은 [미디어 내용 페이지](../../relational-databases/backup-restore/backup-device-media-contents-page.md)를 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>논리적 백업 장치의 속성과 내용을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 문을 사용합니다. 이 예에서는 `AdvWrks2008R2Backup` 논리적 백업 장치에 대한 정보를 반환합니다.  
  
```tsql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [backupfilegroup&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
