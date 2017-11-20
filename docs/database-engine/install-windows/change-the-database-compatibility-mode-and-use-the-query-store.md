---
title: "데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용 | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 514fe566dd9a26d4a6244e8fb067f97678d2dbc7
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="change-the-database-compatibility-mode-and-use-the-query-store"></a>데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2016 및 SQL Server 2017에서는 데이터베이스에 대한 DATABASE_COMPATIBILITY 수준이 변경된 후에만 일부 변경 내용이 활성화됩니다. 이 작업은 여러 가지 이유로 수행되었습니다.  
  
- 업그레이드는 단방향 작업이므로(파일 형식을 다운그레이드할 수 없음) 데이터베이스 내에서 별도 작업에 대한 새로운 기능의 사용을 분리하는 값이 있습니다.  이전 DATABASE_COMPATIBILITY 수준으로 설정을 되돌릴 수는 있습니다.  새 모델은 중단 창 동안 발생해야 하는 것의 수를 줄입니다.  
  
- 쿼리 프로세서에 대한 변경 내용에는 복잡한 영향이 있을 수 있습니다.  시스템에 대한 "적절한" 변경이 대부분의 고객에게 유용할 수도 있지만 다른 사용자에 대한 중요한 쿼리에서 허용되지 않는 회귀가 발생할 수 있습니다.  업그레이드 프로세스에서 이 논리를 분리하는 작업은 쿼리 저장소와 같은 기능이 계획 선택 회귀를 신속하게 완화하거나 프로덕션 서버에서 완전히 방지할 수 있도록 합니다.  
  
> [!NOTE]  
>  사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이었다면 업그레이드 후에도 동일하게 유지됩니다. 업그레이드 이전에 호환성 수준이 90이었다면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다. 업그레이드 후에는 tempdb, 모델, msdb 및 리소스 데이터베이스의 호환성 수준이 현재 호환성 수준으로 설정됩니다. master 시스템 데이터베이스는 업그레이드 이전의 호환성 수준으로 유지됩니다. 
  
 새 쿼리 프로세서 기능을 활성화하는 업그레이드 프로세스는 제품의 릴리스 이후 서비스 모델과 관련이 있습니다.  이러한 수정의 일부는 추적 플래그 4199에서 릴리스됩니다.  수정이 필요한 고객은 다른 고객에 대한 예기치 않은 회귀를 일으키지 않고 이러한 수정을 선택할 수 있습니다.  쿼리 프로세서 핫픽스에 대한 릴리스 이후 서비스 모델은 [여기](https://support.microsoft.com/en-us/kb/974006)에 설명되어 있습니다. SQL Server 2016년부터 새 호환성 수준으로 전환하면 이러한 수정이 이제 최신 호환성 수준에서 기본적으로 사용될 수 있으므로 4199 추적 플래그가 더 이상 필요하지 않습니다.  따라서 업그레이드 프로세스의 일부로 업그레이드 프로세스가 완료되면 4199가 활성화되지 않는 것을 확인하는 것이 중요합니다.  
  
 쿼리 프로세서를 코드의 최신 버전으로 업그레이드하기 위해 권장되는 워크플로는 다음과 같습니다.  
  
1.  데이터베이스 호환성 수준을 변경하지 않고(이전 수준에서 유지) 데이터베이스를 SQL Server 2016으로 업그레이드  
  
2.  데이터베이스에서 쿼리 저장소를 활성화합니다. 쿼리 저장소 활성화 및 사용에 대한 자세한 내용은 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)을(를) 참조하세요.  
  
3.  작업의 대표 데이터를 수집할 수 있도록 충분한 시간을 기다립니다.  
  
4.  데이터베이스의 호환성 수준을 현재 호환성 수준으로 변경합니다. 

   >[!NOTE]
   >최신 호환성 수준은 SQL Server 버전에 따라 다릅니다.
   >- SQL Server 2016: 130
   >- SQL Server 2017: 140

5. 호환성 수준을 변경한 후에 SQL Server Management Studio를 사용하여 특정 쿼리에 성능 회귀가 있는지 평가합니다.
  
6.  회귀가 있는 경우 쿼리 저장소에서 이전 계획을 강제로 적용합니다.  
  
7.  강제 적용에 실패하는 쿼리 계획이 있는 경우 또는 성능이 여전히 충분하지 않은 경우 호환성 수준을 이전 설정으로 되돌린 다음 Microsoft 고객 지원 서비스에 연락하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
  
  

