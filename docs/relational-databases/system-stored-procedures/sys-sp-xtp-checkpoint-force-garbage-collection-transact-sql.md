---
description: sys.sp_xtp_checkpoint_force_garbage_collection(Transact-SQL)
title: sys. sp_xtp_checkpoint_force_garbage_collection (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection_TSQL
- sys.sp_xtp_checkpoint_force_garbage_collection
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection
ms.assetid: 82b35b2b-edbd-44ac-9fc8-80695f2fd1df
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9073ebd53ea3b2bb87719b92132e2e4e1e38caf5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473423"
---
# <a name="syssp_xtp_checkpoint_force_garbage_collection-transact-sql"></a>sys.sp_xtp_checkpoint_force_garbage_collection(Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  병합 작업에서 사용되는 원본 파일을 원본 파일이 필요하지 않고 가비지 수집될 수 있기 전의 LSN(로그 시퀀스 번호)으로 표시합니다. 또한 연결된 LSN이 Filestream 가비지 수집에 대한 로그 잘림 지점보다 작은 파일을 이동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 
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
  
|열|설명|  
|------------|-----------------|  
|num_collected_items|Filestream 가비지 수집으로 이동한 파일 수를 나타냅니다. 이러한 파일의 LSN(로그 시퀀스 번호)은 로그 잘림 지점의 LSN보다 작습니다.|  
|num_marked_for_collection_items|LSN이 로그 끝 LSN의 로그 blockID로 업데이트된 데이터/델타 파일 수를 나타냅니다.|  
|last_collected_xact_seqno|파일이 Filestream 가비지 수집으로 이동한 마지막 해당 LSN을 반환합니다.|  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스 소유자 권한이 필요합니다.  
  
## <a name="sample"></a>샘플  
  
```  
exec [sys].[sp_xtp_checkpoint_force_garbage_collection] hkdb1  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
