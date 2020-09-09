---
description: sp_gettopologyinfo(Transact-SQL)
title: sp_gettopologyinfo (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0649d6f57ea5bb6f7a12c74e7dbec98053f2ea96
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549790"
---
# <a name="sp_gettopologyinfo-transact-sql"></a>sp_gettopologyinfo(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  피어 투 피어 트랜잭션 복제 토폴로지에 대한 정보를 반환합니다. 이 절차를 실행 하기 전에 [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) 를 실행 하 여 정보를 수집 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>인수  
 [ @request_id =] *request_id*  
 토폴로지 상태 요청 ID입니다. *request_id* 은 **int**이며 기본값은 NULL입니다. ID를 얻으려면 @request_id [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) 의 output 매개 변수를 사용 하거나 [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) 시스템 테이블을 쿼리 합니다.  
  
## <a name="result-sets"></a>결과 집합  
 sp_gettopologyinfo는 하나의 XML 열로 구성된 결과 집합을 반환합니다. XML 열의 데이터는 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) 시스템 테이블의 데이터와 동일 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_gettopologyinfo는 피어 투 피어 트랜잭션 복제에 사용됩니다. Sp_gettopologyinfo을 실행 하기 전에 [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) 를 실행 합니다. 이러한 프로시저는 피어 투 피어 토폴로지 구성 마법사에서 사용되지만 XML 형식의 토폴로지 정보가 필요한 경우 직접 사용할 수도 있습니다. 테이블 형식 결과를 선호 하는 경우 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) 시스템 테이블을 쿼리 합니다.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
