---
title: optimize for ad hoc workloads 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9fde6ede2a26d6f893ae39032cf1847e0daaed9b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157623"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>optimize for ad hoc workloads 서버 구성 옵션
  **optimize for ad hoc workloads** 옵션은 여러 개의 일회용 임시 일괄 처리를 포함하는 작업에서 계획 캐시의 효율성을 높이는 데 사용됩니다. 이 옵션을 1로 설정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 일괄 처리가 처음으로 컴파일되었을 때 전체 컴파일된 계획 대신 계획 캐시에 포함된 작은 컴파일된 계획 스텁을 저장합니다. 이렇게 하면 계획 캐시에 다시 사용할 수 없는 컴파일된 계획이 채워지지 않게 되므로 메모리 가중을 줄일 수 있습니다.  
  
 컴파일된 계획 스텁은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 이러한 임시 일괄 처리가 이전에 컴파일되었지만 컴파일된 계획 스텁만 저장했다는 것을 인식하게 함으로써 이 일괄 처리(컴파일 또는 실행된)가 다시 호출될 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 일괄 처리를 컴파일하고, 계획 캐시에서 컴파일된 계획 스텁을 제거하고, 계획 캐시에 전체 컴파일된 계획을 추가하도록 합니다.  
  
 **optimize for ad hoc workloads** 를 1로 설정하면 새 계획만 영향을 받으며, 이미 계획 캐시에 있던 계획은 영향을 받지 않습니다.  
  
 컴파일된 계획 스텁은 sys.dm_exec_cached_plans 카탈로그 뷰로 표시되는 cacheobjtype 중 하나입니다. 여기에는 고유한 SQL 핸들 및 계획 핸들이 포함됩니다. 컴파일된 계획 스텁에는 연결된 실행 계획이 없으며 계획 핸들을 쿼리해도 XML 실행 계획이 반환되지 않습니다.  
  
 추적 플래그 8032는 일반적으로 캐시가 더 커지도록 허용하는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM 설정으로 캐시 제한 매개 변수를 복구합니다. 자주 재사용되는 캐시 항목이 캐시에 맞지 않고 *optimize for ad hoc workloads Server Configuration Option* 으로 계획 캐시 관련 문제를 해결하지 못한 경우 이 설정을 사용합니다.  
  
> [!WARNING]  
>  추적 플래그 8032는 대형 캐시로 버퍼 풀과 같은 다른 메모리 소비자에 제공되는 메모리가 줄어들 수 있는 성능 문제를 일으킬 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_exec_cached_plans&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
