---
title: sp_addmergepartition (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5599370f892d174336411573883e2feffa27b886
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492655"
---
# <a name="spaddmergepartition-transact-sql"></a>sp_addmergepartition(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  값으로 필터링 되는 구독에 대 한 동적으로 필터링 된 파티션을 만듭니다 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 하거나 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 구독자의 합니다. 이 저장 프로시저는 게시된 데이터베이스의 게시자에서 실행되며 파티션을 수동으로 생성하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 파티션이 생성 되는 병합 게시가입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다. 하는 경우 *suser_sname* 지정 된 값 *hostname* NULL 이어야 합니다.  
  
`[ @suser_sname = ] 'suser_sname'` 값을 기준으로 필터링 되어에 구독에 대 한 파티션을 만들 때 사용 되는 값을 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 구독자 함수입니다. *suser_sname* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @host_name = ] 'host_name'` 값을 기준으로 필터링 되어에 구독에 대 한 파티션을 만들 때 사용 되는 값을 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 구독자 함수입니다. *host_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergepartition** 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addmergepartition**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [매개 변수가 있는 필터로 병합 게시에 대 한 스냅숏 만들기](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
