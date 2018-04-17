---
title: sp_addmergepartition (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
applies_to:
- SQL Server
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a169b85f0ae207f72ba0f142633aa323403745c3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spaddmergepartition-transact-sql"></a>sp_addmergepartition(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  값에 따라 필터링 된 구독에 대 한 동적으로 필터링 된 파티션을 만들고 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 또는 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 구독자에 있습니다. 이 저장 프로시저는 게시된 데이터베이스의 게시자에서 실행되며 파티션을 수동으로 생성하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication**=] **'***게시***'**  
 파티션을 생성할 병합 게시입니다. *게시* 은 **sysname**, 기본값은 없습니다. 경우 *suser_sname* 지정 된 값의 *hostname* NULL 이어야 합니다.  
  
 [ **@suser_sname**=] **'***suser_sname***'**  
 값으로 필터링 되는 구독에 대 한 파티션을 만들 때 사용 되는 값은는 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 구독자에는 함수입니다. *suser_sname* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@host_name**=] **'***host_name***'**  
 값으로 필터링 되는 구독에 대 한 파티션을 만들 때 사용 되는 값은는 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 구독자에는 함수입니다. *host_name* 은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_addmergepartition** 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_addmergepartition**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [매개 변수가 있는 필터로 병합 게시에 대 한 스냅숏 만들기](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
