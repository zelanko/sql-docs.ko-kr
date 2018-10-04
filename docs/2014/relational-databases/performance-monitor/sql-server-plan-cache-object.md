---
title: SQL Server, Plan Cache 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Plan Cache object
- SQLServer:Plan Cache
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e24c072897a46d8a5b3add713f94a84e12a642b7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190793"
---
# <a name="sql-server-plan-cache-object"></a>SQL Server, Plan Cache 개체
  **Plan Cache** 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 저장 프로시저, 임시 및 준비된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 트리거와 같은 개체를 저장하기 위해 메모리를 사용하는 방법을 모니터링하는 카운터를 제공합니다. **Plan Cache** 개체의 여러 인스턴스를 한 번에 모니터링할 수 있으며 각 인스턴스는 모니터링할 다양한 유형의 계획을 나타냅니다.  
  
 다음 표에서는 **SQLServer:Plan Cache**카운터에 대해 설명합니다.  
  
|SQL Server Plan Cache 카운터|Description|  
|------------------------------------|-----------------|  
|**Cache Hit Ratio**|캐시 적중 횟수와 조회 간 비율입니다.|  
|**Cache Object Counts**|캐시에 있는 캐시 개체 수입니다.|  
|**Cache Pages**|캐시 개체에 의해 사용되는 8KB 페이지 수입니다.|  
|**Cache Objects in use**|사용 중인 캐시 개체의 수입니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|Plan Cache 인스턴스|Description|  
|-------------------------|-----------------|  
|**_Total**|모든 유형의 캐시 인스턴스에 대한 정보입니다.|  
|**Sql Plans**|자동으로 매개 변수가 있는 쿼리를 포함하여 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리에서 생성되는 쿼리 계획이거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_prepare **또는** sp_cursorprepare **를 사용하여 준비된**문으로 생성되는 쿼리 계획입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 동일한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 나중에 실행되는 경우 다시 사용하기 위해 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 대한 계획을 캐시합니다. 사용자가 매개 변수가 있는 쿼리(명시적으로 준비하지 않은 경우 포함)도 Prepared SQL Plans로 모니터링됩니다.|  
|**Object Plans**|저장 프로시저, 함수 또는 트리거를 만들 때 생성되는 쿼리 계획입니다.|  
|**Bound Trees**|뷰, 규칙, 계산 열 및 CHECK 제약 조건에 대한 정규화된 트리입니다.|  
|**확장 저장 프로시저**|확장 저장 프로시저에 대한 카탈로그 정보입니다.|  
|**Temporary Tables & Table Variables**|임시 테이블 및 테이블 변수와 관련된 캐시 정보입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server, Buffer Manager 개체](sql-server-buffer-manager-object.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
