---
title: "병합 게시에 대한 호환성 수준 설정 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [SQL Server], replication
- backward compatibility [SQL Server], replication
- publications [SQL Server replication], backward compatibility
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b9bed3d2a282b0078e31ab150165a4ffd3e07f7f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="set-the-compatibility-level-for-merge-publications"></a>병합 게시에 대한 호환성 수준 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 병합 게시의 호환성 수준을 설정하는 방법에 대해 설명합니다. 병합 복제는 게시 호환성 수준을 사용하여 지정된 데이터베이스에서 게시에 사용할 수 있는 기능을 확인합니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 병합 게시에 대한 호환성 수준을 설정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **구독자 유형** 페이지에서 호환성 수준을 설정합니다. 이 마법사에 액세스하는 방법은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)에서 병합 게시의 호환성 수준을 설정하는 방법에 대해 설명합니다. 게시 스냅숏이 생성된 후 호환성 수준을 증가시킬 수는 있지만 감소시킬 수는 없습니다. **게시 속성 - \<Publication>** 대화 상자의 **일반** 페이지에서 호환성 수준을 늘립니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요. 게시 호환성 수준을 증가시키면 이전 버전의 호환성 수준을 실행하는 서버에 있는 기존 구독은 더 이상 동기화할 수 없게 됩니다.  
  
> [!NOTE]  
>  호환성 수준은 다른 게시 속성 및 유효한 아티클 속성을 결정하는 데에도 의미를 가지므로 대화 상자를 동일하게 사용할 때는 호환성 수준 및 다른 속성을 변경하지 마세요. 속성을 변경하면 게시를 위한 스냅숏을 다시 생성해야 합니다.  
  
#### <a name="to-set-the-publication-compatibility-level"></a>게시 호환성 수준을 설정하려면  
  
-   새 게시 마법사의 **구독자 유형** 페이지에서 게시가 지원해야 하는 구독자의 유형을 선택합니다.  
  
#### <a name="to-increase-the-publication-compatibility-level"></a>게시 호환성 수준을 증가시키려면  
  
-   **게시 속성 - \<게시>** 대화 상자의 **일반** 페이지에서 **호환성 수준**을 선택합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 병합 게시의 호환성 수준은 게시를 만들 때 설정하거나 이후에 프로그래밍 방식으로 수정할 수 있습니다. 병합 저장 프로시저를 사용하여 이 게시 속성을 설정 또는 변경할 수 있습니다.  
  
#### <a name="to-set-the-publication-compatibility-level-for-a-merge-publication"></a>병합 게시에 대한 게시 호환성 수준을 설정하려면  
  
1.  게시가 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전과 호환되도록 하려면 **@publication_compatibility_level**에 값을 지정하여 게시자에서 [sp_addmergepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을 실행합니다. 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
#### <a name="to-change-the-publication-compatibility-level-of-a-merge-publication"></a>병합 게시의 게시 호환성 수준을 변경하려면  
  
1.  **@property**에 **publication_compatibility_level**, **@value**에 적절한 게시 호환성 수준을 지정하여 [sp_changemergepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)을 실행합니다.  
  
#### <a name="to-determine-the-publication-compatibility-level-of-a-merge-publication"></a>병합 게시의 게시 호환성 수준을 확인하려면  
  
1.  원하는 게시를 지정하여 [sp_helpmergepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)을 실행합니다.  
  
2.  결과 집합의 **backward_comp_level** 열에서 게시 호환성 수준을 찾습니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 병합 게시를 만들고 게시 호환성 수준을 설정합니다.  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 다음 예에서는 병합 게시에 대한 게시 호환성 수준을 변경합니다.  
  
> [!NOTE]  
>  게시에서 특정 호환성 수준이 필요한 기능을 사용하고 있는 경우에는 게시 호환성 수준 변경이 허용되지 않을 수 있습니다. 자세한 내용은 [복제의 이전 버전과의 호환성](../../../relational-databases/replication/replication-backward-compatibility.md)을 참조하세요.  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2008 or later.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'100RTM';  
GO  
  
```  
  
 다음 예에서는 병합 게시에 대한 현재 게시 호환성 수준을 반환합니다.  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  
