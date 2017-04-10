---
title: "스키마 변경 내용 복제 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "복제 [SQL Server], 스키마 변경 내용"
  - "스키마 [SQL Server 복제], 변경 내용 복제"
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# 스키마 변경 내용 복제
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 스키마 변경 내용을 복제하는 방법에 대해 설명합니다.  
  
 게시된 아티클에서 다음 스키마를 변경하면 기본적으로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구독자에 변경 내용이 전파됩니다.  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
-   **다음을 사용하여 스키마 변경을 복제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   ALTER TABLE … DROP COLUMN 문은 스키마 변경 내용 복제를 해제한 경우에도 항상 삭제된 열이 있는 구독이 포함된 모든 구독자에 복제됩니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 게시에 대 한 스키마 변경 내용을 복제 하지 않을 경우의 스키마 변경 복제를 사용 하지 않도록 설정 된 **게시 속성-\< 게시>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### 스키마 변경 내용 복제를 해제하려면  
  
1.  에 **구독 옵션** 의 페이지는 **게시 속성-\< 게시>** 대화 상자에서 값을 설정는 **스키마 변경을 복제** 속성을 **False**합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     특정 스키마 변경 내용만 전파하려면 스키마를 변경하기 전에 해당 속성을 **True** 로 설정한 다음 스키마 변경 후 **False** 로 설정합니다. 반대로 지정된 변경 내용을 제외한 대부분의 스키마 변경 내용을 전파하려면 스키마를 변경하기 전에 해당 속성을 **False** 로 설정한 다음 스키마 변경 후 **True** 로 설정합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 이러한 스키마 변경 내용을 복제할지 여부를 지정할 수 있습니다. 사용하는 저장 프로시저는 게시 유형에 따라 달라집니다.  
  
#### 스키마 변경 내용을 복제하지 않는 스냅숏 또는 트랜잭션 게시를 만들려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addpublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), 값을 지정 하면 **0** 에 대 한 **@replicate_ddl**합니다. 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
#### 스키마 변경 내용을 복제하지 않는 병합 게시를 만들려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), 값을 지정 하면 **0** 에 대 한 **@replicate_ddl**합니다. 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
#### 스냅숏 또는 트랜잭션 게시에 대해 스키마 변경 내용 복제를 일시적으로 해제하려면  
  
1.  스키마 변경 복제 게시의 경우 실행 [sp_changepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), 값을 지정 하면 **replicate_ddl** 에 대 한 **@property** 값 **0** 에 대 한 **@value**합니다.  
  
2.  게시된 개체에서 DDL 명령을 실행합니다.  
  
3.  (선택 사항) 다시 실행 하 여 스키마 변경 내용 복제를 사용 하도록 설정 [sp_changepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), 값을 지정 하면 **replicate_ddl** 에 대 한 **@property** 값 **1** 에 대 한 **@value**합니다.  
  
#### 병합 게시에 대한 스키마 변경 내용 복제를 일시적으로 해제하려면  
  
1.  스키마 변경 복제 게시의 경우 실행 [sp_changemergepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), 값을 지정 하면 **replicate_ddl** 에 대 한 **@property** 값 **0** 에 대 한 **@value**합니다.  
  
2.  게시된 개체에서 DDL 명령을 실행합니다.  
  
3.  (선택 사항) 다시 실행 하 여 스키마 변경 내용 복제를 사용 하도록 설정 [sp_changemergepublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), 값을 지정 하면 **replicate_ddl** 에 대 한 **@property** 값 **1** 에 대 한 **@value**합니다.  
  
## 참고 항목  
 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  