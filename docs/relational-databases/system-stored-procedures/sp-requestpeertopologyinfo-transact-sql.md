---
title: sp_requestpeertopologyinfo (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeertopologyinfo
- sp_requestpeertopologyinfo_TSQL
helpviewer_keywords:
- sp_requestpeertopologyinfo
ms.assetid: 15cd28bd-5a72-41fb-ae1b-726baaa6fad5
author: stevestein
ms.author: sstein
ms.openlocfilehash: d137706da49f666ce66abea52249796a0094c7e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129655"
---
# <a name="sp_requestpeertopologyinfo-transact-sql"></a>sp_requestpeertopologyinfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 트랜잭션 복제 토폴로지에 대 한 정보로 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) 시스템 테이블을 채웁니다. [Sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md) 를 실행 하 여 테이블에서 XML 형식으로 정보를 가져옵니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_requestpeertopologyinfo [ @publication = ] 'publication'  
        [ ,[ @requestid=] request_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ @publication= ] '*게시*'  
 토폴로지 차원 상태 요청을 수행할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
 [ @request_id= ] *request_id*  
 토폴로지 상태 요청에 할당된 ID 번호입니다. *request_id* 은 **int**이며 기본값은 NULL입니다. 이 ID는 [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md)에서 사용할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_requestpeertopologyinfo는 피어 투 피어 트랜잭션 복제에 사용됩니다. [Sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md)을 실행 하기 전에 sp_requestpeertopologyinfo를 실행 합니다. 이러한 프로시저는 피어 투 피어 토폴로지 구성 마법사에서 사용되지만 XML 형식의 토폴로지 정보가 필요한 경우 직접 사용할 수도 있습니다. 테이블 형식 결과를 선호 하는 경우 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) 시스템 테이블을 쿼리 합니다.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
