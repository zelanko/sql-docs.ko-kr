---
title: sp_dbmmonitorchangemonitoring (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorchangemonitoring
- sp_dbmmonitorchangemonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorchangemonitoring
- database mirroring [SQL Server], monitoring
ms.assetid: 17be755b-673d-4cd4-9544-6ecb4220bed3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b876a7eefe1efd8150f587485ed13d0f0a3de23
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spdbmmonitorchangemonitoring-transact-sql"></a>sp_dbmmonitorchangemonitoring(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 미러링 모니터링 매개 변수의 값을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dbmmonitorchangemonitoring parameter  
    , value   
```  
  
## <a name="arguments"></a>인수  
 *parameter*  
 변경할 매개 변수의 식별자를 지정합니다. 현재 다음 매개 변수만 사용할 수 있습니다.  
  
 1 = 업데이트 기간  
  
 데이터베이스 미러링 상태 테이블에 대한 업데이트 간격(분)입니다. 기본 간격은 1분입니다.  
  
 *value*  
 변경할 매개 변수의 새 값을 지정합니다.  
  
|매개 변수|값 설명|  
|---------------|--------------------------|  
|1.|새 업데이트 기간(분)을 지정하는 1에서 120 범위의 정수입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 업데이트 기간을 5분으로 변경합니다.  
  
```  
EXEC sp_dbmmonitorchangemonitoring 1, 5 ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitoraddmonitoring&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
