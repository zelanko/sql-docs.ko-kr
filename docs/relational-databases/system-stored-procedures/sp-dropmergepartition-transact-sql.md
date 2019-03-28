---
title: sp_dropmergepartition (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepartition_TSQL
- sp_dropmergepartition
helpviewer_keywords:
- sp_dropmergepartition
ms.assetid: 1be511c1-79ff-4947-9379-78d83b7b8945
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74837390afe358d4f9a12d4f98ea9d2e4166e146
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536095"
---
# <a name="spdropmergepartition-transact-sql"></a>sp_dropmergepartition(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  게시에서 매개 변수가 있는 행 필터에 대한 파티션을 제거합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. 이 저장 프로시저는 해당 스냅숏 작업과 파티션에 대한 스냅숏 파일도 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication] = 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @suser_sname = ] 'suser_sname'` 값인 합니다 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 함수 구독자에서 파티션 정의에 사용 합니다. *suser_sname* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @host_name = ] 'host_name'` 값인 합니다 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 함수 구독자에서 파티션 정의에 사용 합니다. *host_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropmergepartition** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_dropmergepartition**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [매개 변수가 있는 필터로 병합 게시에 대한 파티션 관리](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
  
