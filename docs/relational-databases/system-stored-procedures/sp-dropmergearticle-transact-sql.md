---
title: sp_dropmergearticle (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropmergearticle
- sp_dropmergearticle_TSQL
helpviewer_keywords:
- sp_dropmergearticle
ms.assetid: 5ef1fbf7-c03d-4488-9ab2-64aae296fa4f
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 83034ea0a9c14ee1e8efb8c3ea3ea6d604bb367a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spdropmergearticle-transact-sql"></a>sp_dropmergearticle(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시에서 아티클을 제거합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergearticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'   
    [ , [ @ignore_distributor= ] ignore_distributor   
    [ , [ @reserved= ] reserved   
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 아티클을 삭제할 게시의 이름입니다. *게시*은 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'***문서***'**  
 지정된 게시에서 삭제할 아티클의 이름입니다. *문서*은 **sysname**, 기본값은 없습니다. 경우 **모든**, 지정 된 병합 게시의 모든 기존 아티클을 제거 됩니다. 경우에 *문서* 은 **모든**, 게시 여전히에서 삭제 해야 별도로 문서.  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 이 저장 프로시저가 배포자에 연결되지 않고 실행되는지 여부를 표시합니다. *ignore_distributor* 은 **비트**, 기본값은 **0**합니다.  
  
 [  **@reserved=**] *예약*  
 나중에 사용하도록 예약되었습니다. *예약 된* 은 **nvarchar (20)**, 기본값은 NULL입니다.  
  
 [  **@force_invalidate_snapshot=**] *force_invalidate_snapshot*  
 스냅숏 무효화 기능을 설정하거나 해제합니다. *force_invalidate_snapshot* 는 **비트**, 기본값 **0**합니다.  
  
 **0** 병합 아티클의 변경이 스냅숏을 무효화 인해 되지 않도록 지정 합니다.  
  
 **1** 병합 아티클에 대 한 변경을 의미 유효 하려면 스냅숏을 무효화 되는 경우에는 값의 경우 **1** 새 스냅숏 발생에 대 한 사용 권한을 부여 합니다.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 아티클 삭제로 인해 기존 구독을 다시 초기화해야 할 수도 있습니다. *force_reinit_subscription* 는 **비트**, 기본값은 **0**합니다.  
  
 **0** 지정 아티클을 다시 초기화에 대 한 구독이 발생 하지 않습니다.  
  
 **1** 문서 인해 기존 구독이 다시 초기화 해야 하는 삭제 및 구독을 다시 초기화할 수 있는 권한이 부여 것을 의미 합니다.  
  
 [  **@ignore_merge_metadata=** ] *ignore_merge_metadata*  
 내부적으로만 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_dropmergearticle** 병합 복제에 사용 됩니다. 아티클을 삭제 하는 방법에 대 한 자세한 내용은 참조 [기사를 추가 하 고 기존 게시에서 아티클을 삭제](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)합니다.  
  
 실행 **sp_dropmergearticle** 게시에서 아티클을 삭제 하려면에서 제거 되지는 않습니다 개체 게시 데이터베이스나 구독 데이터베이스에서 해당 하는 개체입니다. 필요한 경우 `DROP <object>`를 사용하여 수동으로 이러한 개체를 제거하십시오.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_dropmergearticle**합니다.  
  
## <a name="example"></a>예제  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @table1 AS sysname;  
DECLARE @table2 AS sysname;  
DECLARE @table3 AS sysname;  
DECLARE @salesschema AS sysname;  
DECLARE @hrschema AS sysname;  
DECLARE @filterclause AS nvarchar(1000);  
SET @publication = N'AdvWorksSalesOrdersMerge';   
SET @table1 = N'Employee';   
SET @table2 = N'SalesOrderHeader';   
SET @table3 = N'SalesOrderDetail';   
SET @salesschema = N'Sales';  
SET @hrschema = N'HumanResources';  
SET @filterclause = N'Employee.LoginID = HOST_NAME()';  
  
-- Drop the merge join filter between SalesOrderHeader and SalesOrderDetail.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table3,   
  @filtername = N'SalesOrderDetail_SalesOrderHeader',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the merge join filter between Employee and SalesOrderHeader.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table2,   
  @filtername = N'SalesOrderHeader_Employee',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderDetail table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table3,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderHeader table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table2,   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the Employee table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table1,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [아티클 삭제](../../relational-databases/replication/publish/delete-an-article.md)   
 [기존 게시에 대한 아티클 추가 및 삭제](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
