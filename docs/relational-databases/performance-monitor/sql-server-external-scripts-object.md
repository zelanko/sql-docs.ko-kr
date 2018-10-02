---
title: SQL Server, External Scripts 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e6eb921d6ebee88ce14ad30b0d2071941ec5f007
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665551"
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, 외부 스크립트 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **의** SQLServer:외부 스크립트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체는 외부 스크립트를 실행하는 것과 연관된 동작을 모니터링하는 카운터를 제공합니다. 외부 스크립트를 실행하는 방법은 [sp_execute_external_script&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 참조하세요.  
  
 이 테이블은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **외부 스크립트** 카운터를 설명합니다.  
  
|SQL Server 외부 스크립트 카운터|설명|  
|------------------------------------------|-----------------|  
|**실행 오류**|외부 스크립트 실행 시 발생한 오류 수입니다.|  
|**묵시적 인증. Logins**|묵시적 인증을 사용하여 인증된 위성 프로세스의 로그인 수입니다.|  
|**병렬 실행**|@parallel = 1로 실행한 외부 스크립트의 수입니다.|  
|**SQL CC 실행**|SQL 계산 컨텍스트를 사용하여 실행한 외부 스크립트의 수입니다.|  
|**스트림 실행**|@r_rowsPerRead 매개 변수를 사용하여 실행한 외부 스크립트의 수입니다.|  
|**총 실행 시간(ms)**|외부 스크립트를 실행하는 데 소요된 총 시간입니다.|  
|**모든 실행**|실행한 외부 스크립트의 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
