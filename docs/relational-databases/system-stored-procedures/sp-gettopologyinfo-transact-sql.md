---
title: sp_gettopologyinfo (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7b05bcc47673bba1cad4cbf5cf936f3f7b9dca80
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spgettopologyinfo-transact-sql"></a>sp_gettopologyinfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 트랜잭션 복제 토폴로지에 대한 정보를 반환합니다. 실행 [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) 이 절차를 실행 하기 전에 정보를 수집 하도록 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>인수  
 [ @request_id=] *request_id*  
 토폴로지 상태 요청 ID입니다. *request_id* 은 **int**, 기본값은 NULL입니다. ID를 가져오려면는 @request_id 출력 매개 변수에서 [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) 또는 쿼리는 [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) 시스템 테이블입니다.  
  
## <a name="result-sets"></a>결과 집합  
 sp_gettopologyinfo는 하나의 XML 열로 구성된 결과 집합을 반환합니다. XML 열에 데이터의 데이터와 같은지는 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) 시스템 테이블입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_gettopologyinfo는 피어 투 피어 트랜잭션 복제에 사용됩니다. 실행 [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) sp_gettopologyinfo를 실행 하기 전에. 이러한 프로시저는 피어 투 피어 토폴로지 구성 마법사에서 사용되지만 XML 형식의 토폴로지 정보가 필요한 경우 직접 사용할 수도 있습니다. 테이블 형식 결과 선호 하는 경우 쿼리는 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) 시스템 테이블입니다.  
  
## <a name="permissions"></a>Permissions  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [피어 투 피어 트랜잭션 복제](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
