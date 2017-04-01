---
title: "병합 게시에 대한 호환성 수준 설정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "호환성 [SQL Server], 복제"
  - "이전 버전과의 호환성 [SQL Server], 복제"
  - "게시 [SQL Server 복제], 이전 버전과의 호환성"
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 병합 게시에 대한 호환성 수준 설정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 게시의 호환성 수준을 설정하는 방법에 대해 설명합니다. 병합 복제는 게시 호환성 수준을 사용하여 지정된 데이터베이스에서 게시에 사용할 수 있는 기능을 확인합니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 병합 게시에 대한 호환성 수준을 설정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **구독자 유형** 페이지에서 호환성 수준을 설정합니다. 이 마법사의 액세스에 대 한 자세한 내용은 참조 하십시오. [발행물 만들기](../../../relational-databases/replication/publish/create-a-publication.md)합니다. 게시 스냅숏이 생성된 후 호환성 수준을 증가시킬 수는 있지만 감소시킬 수는 없습니다. 호환성 수준을 증가 **일반** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요. 게시 호환성 수준을 증가시키면 이전 버전의 호환성 수준을 실행하는 서버에 있는 기존 구독은 더 이상 동기화할 수 없게 됩니다.  
  
> [!NOTE]  
>  호환성 수준은 다른 게시 속성 및 유효한 아티클 속성을 결정하는 데에도 의미를 가지므로 대화 상자를 동일하게 사용할 때는 호환성 수준 및 다른 속성을 변경하지 마세요. 속성을 변경하면 게시를 위한 스냅숏을 다시 생성해야 합니다.  
  
#### 게시 호환성 수준을 설정하려면  
  
-   새 게시 마법사의 **구독자 유형** 페이지에서 게시가 지원해야 하는 구독자의 유형을 선택합니다.  
  
#### 게시 호환성 수준을 증가시키려면  
  
-   에 **일반** 의 페이지는 **게시 속성-\< 게시>** 대화 상자에 대 한 선택 **호환성 수준을**합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 병합 게시의 호환성 수준은 게시를 만들 때 설정하거나 이후에 프로그래밍 방식으로 수정할 수 있습니다. 병합 저장 프로시저를 사용하여 이 게시 속성을 설정 또는 변경할 수 있습니다.  
  
#### 병합 게시에 대한 게시 호환성 수준을 설정하려면  
  
1.  게시자에서 실행 [sp_addmergepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), 값을 지정 **@publication_compatibility_level** 게시의 이전 버전과 호환 되도록 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
#### 병합 게시의 게시 호환성 수준을 변경하려면  
  
1.  실행 [sp_changemergepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), 로 지정 하 여 **publication_compatibility_level** 에 대 한 **@property** 및에 대 한 적절 한 게시 호환성 수준은 **@value**합니다.  
  
#### 병합 게시의 게시 호환성 수준을 확인하려면  
  
1.  실행 [sp_helpmergepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), 원하는 게시를 지정 합니다.  
  
2.  게시 호환성 수준을 찾습니다는 **backward_comp_level** 결과 집합의 열입니다.  
  
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
>  게시에서 특정 호환성 수준이 필요한 기능을 사용하고 있는 경우에는 게시 호환성 수준 변경이 허용되지 않을 수 있습니다. 자세한 내용은 참조 [복제 이전 버전과 호환성](../../../relational-databases/replication/replication-backward-compatibility.md)합니다.  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
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
  
## 참고 항목  
 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  