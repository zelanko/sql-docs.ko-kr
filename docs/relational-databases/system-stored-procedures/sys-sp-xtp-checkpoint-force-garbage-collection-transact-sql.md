---
title: sys.sp_xtp_checkpoint_force_garbage_collection (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection_TSQL
- sys.sp_xtp_checkpoint_force_garbage_collection
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection
ms.assetid: 82b35b2b-edbd-44ac-9fc8-80695f2fd1df
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c6d57012abbdf6a83587a1d3ffb5c4c9a610850
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysspxtpcheckpointforcegarbagecollection-transact-sql"></a>sys.sp_xtp_checkpoint_force_garbage_collection(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  병합 작업에서 사용되는 원본 파일을 원본 파일이 필요하지 않고 가비지 수집될 수 있기 전의 LSN(로그 시퀀스 번호)으로 표시합니다. 또한 연결된 LSN이 Filestream 가비지 수집에 대한 로그 잘림 지점보다 작은 파일을 이동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 
## <a name="syntax"></a>구문  
  
```  
sys.sp_xtp_checkpoint_force_garbage_collection [[ @dbname=database_name]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 가비지 수집을 실행할 데이터베이스입니다. 기본값은 현재 데이터베이스입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 성공의 경우 0이고, 실패의 경우 0이 아닙니다.  
  
## <a name="result-set"></a>결과 집합  
 반환된 행에는 다음 정보가 포함되어 있습니다.  
  
|열|Description|  
|------------|-----------------|  
|num_collected_items|Filestream 가비지 수집으로 이동한 파일 수를 나타냅니다. 이러한 파일의 LSN(로그 시퀀스 번호)은 로그 잘림 지점의 LSN보다 작습니다.|  
|num_marked_for_collection_items|LSN이 로그 끝 LSN의 로그 blockID로 업데이트된 데이터/델타 파일 수를 나타냅니다.|  
|last_collected_xact_seqno|파일이 Filestream 가비지 수집으로 이동한 마지막 해당 LSN을 반환합니다.|  
  
## <a name="permissions"></a>Permissions  
 데이터베이스 소유자 권한이 필요합니다.  
  
## <a name="sample"></a>예제  
  
```  
exec [sys].[sp_xtp_checkpoint_force_garbage_collection] hkdb1  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
