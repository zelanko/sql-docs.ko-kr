---
title: 데이터베이스 호환성 수준 변경 및 쿼리 저장소 사용 | Microsoft Docs
ms.custom: ''
ms.date: 07/21/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 7aceade515dad939723fd295893676c967ca91c5
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40406540"
---
# <a name="change-the-database-compatibility-level-and-use-the-query-store"></a>데이터베이스 호환성 수준 변경 및 쿼리 저장소 사용

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 [데이터베이스 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)이 변경된 경우에만 일부 변경 내용이 활성화됩니다. 이 작업은 여러 가지 이유로 수행되었습니다.  
  
- 업그레이드는 단방향 작업이므로(파일 형식을 다운그레이드할 수 없음) 데이터베이스 내에서 별도 작업에 대한 새로운 기능의 사용을 분리하는 값이 있습니다. 이전 데이터베이스 호환성 수준으로 설정을 되돌릴 수 있습니다.  새 모델은 중단 창 동안 발생해야 하는 것의 수를 줄입니다.  
  
- 쿼리 프로세서에 대한 변경 내용에는 복잡한 영향이 있을 수 있습니다. 시스템에 대한 "적절한" 변경이 대부분의 작업에 유용할 수도 있지만 다른 사용자에 대한 중요한 쿼리에서 허용되지 않는 회귀가 발생할 수 있습니다. 업그레이드 프로세스에서 이 논리를 분리하는 작업은 쿼리 저장소와 같은 기능이 계획 선택 회귀를 신속하게 완화하거나 프로덕션 서버에서 완전히 방지할 수 있도록 합니다.  
  
> [!IMPORTANT]  
> 데이터베이스가 연결 또는 복원된 경우, 그리고 현재 위치 업그레이드 이후에 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에서 아래 동작이 예상됩니다.
> - 사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이었다면 업그레이드 후에도 동일하게 유지됩니다.    
> - 업그레이드 이전에 사용자데 이터베이스의 호환성 수준이 90이었다면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다.    
> - 업그레이드 후에는 tempdb, 모델, msdb 및 리소스 데이터베이스의 호환성 수준이 현재 호환성 수준으로 설정됩니다.   
> - master 시스템 데이터베이스는 업그레이드 이전의 호환성 수준으로 유지됩니다.    
  
새 쿼리 프로세서 기능을 활성화하는 업그레이드 프로세스는 제품의 릴리스 이후 서비스 모델과 관련이 있습니다.  이러한 수정의 일부는 [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)에서 릴리스됩니다.  수정이 필요한 고객은 다른 고객에 대한 예기치 않은 회귀를 일으키지 않고 이러한 수정을 선택할 수 있습니다. 쿼리 프로세서 핫픽스에 대한 릴리스 이후 서비스 모델은 [여기](http://support.microsoft.com/kb/974006)에 설명되어 있습니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 새 호환성 수준으로 전환하면 이러한 수정이 이제 최신 호환성 수준에서 기본적으로 사용될 수 있으므로 추적 플래그 4199가 더 이상 필요하지 않습니다. 따라서 업그레이드 프로세스의 일부로 업그레이드 프로세스가 완료되면 4199가 활성화되지 않는 것을 확인하는 것이 중요합니다.  

> [!NOTE]
> 그러나 해당하는 경우 여전히 RTM 이후 출시된 새로운 쿼리 프로세서 수정을 활성화하는 데 추적 플래그 4199가 필요합니다.
  
쿼리 프로세서를 코드의 최신 버전으로 업그레이드하는 권장되는 워크플로는 [쿼리 저장소 사용 시나리오의 최신 SQL Server 섹션으로 업그레이드하는 동안 성능 안정성 유지](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)에서 문서화됩니다.  
  
![query-store-usage-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5") 
 
## <a name="see-also"></a>참고 항목  
[데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)     
[쿼리 저장소 사용 시나리오](../../relational-databases/performance/query-store-usage-scenarios.md)     
[ALTER DATABASE &#40;Transact-SQL&#41; 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
    
  
