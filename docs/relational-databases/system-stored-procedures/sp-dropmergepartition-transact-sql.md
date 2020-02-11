---
title: sp_dropmergepartition (Transact-sql) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2c7ac88631c481bb98515c3b4753e02b9f66b151
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933943"
---
# <a name="sp_dropmergepartition-transact-sql"></a>sp_dropmergepartition(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  게시에서 매개 변수가 있는 행 필터에 대한 파티션을 제거합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. 이 저장 프로시저는 해당 스냅샷 작업과 파티션에 대한 스냅샷 파일도 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication] = 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @suser_sname = ] 'suser_sname'`파티션을 정의 하는 데 사용 되는 구독자에서 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 함수의 값입니다. *suser_sname* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @host_name = ] 'host_name'`파티션을 정의 하는 데 사용 되는 구독자에서 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 함수의 값입니다. *host_name* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropmergepartition** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_dropmergepartition**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [매개 변수가 있는 필터로 병합 게시에 대한 파티션 관리](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
  
