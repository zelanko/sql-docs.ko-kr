---
title: sp_addmergepartition (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a4f4743efbd0ee3b7a57cb4fab02c98a2680a870
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786264"
---
# <a name="sp_addmergepartition-transact-sql"></a>sp_addmergepartition(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  구독자에서 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 또는 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 값으로 필터링 되는 구독에 대해 동적으로 필터링 된 파티션을 만듭니다. 이 저장 프로시저는 게시된 데이터베이스의 게시자에서 실행되며 파티션을 수동으로 생성하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`파티션이 생성 되는 병합 게시입니다. *게시* 는 **sysname**이며 기본값은 없습니다. *Suser_sname* 지정 된 경우 *호스트 이름* 값은 NULL 이어야 합니다.  
  
`[ @suser_sname = ] 'suser_sname'`구독자에서 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 함수의 값으로 필터링 되는 구독에 대 한 파티션을 만들 때 사용 되는 값입니다. *suser_sname* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @host_name = ] 'host_name'`구독자에서 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 함수의 값으로 필터링 되는 구독에 대 한 파티션을 만들 때 사용 되는 값입니다. *host_name* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergepartition** 는 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addmergepartition**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [매개 변수가 있는 필터를 사용 하 여 병합 게시에 대 한 스냅숏 만들기](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
