---
title: 데이터베이스 엔진 업그레이드 | Microsoft Docs
description: 이 문서에서는 SQL Server 데이터베이스 엔진을 SQL Server의 이전 릴리스에서 SQL Server 2019로 업그레이드하는 데 도움이 되는 리소스에 대한 링크를 제공합니다.
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: dd6c78880419b2330e109d4e1f1416c99f84963d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460706"
---
# <a name="upgrade-database-engine"></a>데이터베이스 엔진 업그레이드

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
  이 섹션의 문서에서는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진을 업그레이드하는 방법을 설명합니다.  
  
1.  [데이터베이스 엔진 업그레이드 방법 선택을 선택합니다](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md), 업그레이드를 시작하기 전에 다양한 업그레이드 방법을 파악해야 합니다. 이 문서에서는 업그레이드 방법 및 각 업그레이드 방법에서 수행하는 단계를 설명합니다.  
  
2.  [데이터베이스 엔진 업그레이드 계획 및 테스트를 수행합니다](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md). 업그레이드 방법을 검토하고 나면 환경에 적합한 업그레이드 방법을 개발하여 테스트한 후 기존 환경을 업그레이드할 수 있습니다. 이 문서에서는 업그레이드 계획을 개발하고 테스트하는 방법에 대해 설명합니다.  
  
3.  [데이터베이스 엔진 업그레이드를 완료합니다](../../database-engine/install-windows/complete-the-database-engine-upgrade.md). 데이터베이스 엔진이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 업그레이드 완료되고 데이터베이스가 온라인 상태가 된 후, 새 백업 만들기, 새 기능 사용을 위한 데이터베이스 기능 업그레이드, 전체 텍스트 카탈로그 다시 채우기 등의 추가 단계를 수행해야 합니다. 이 문서에서는 해당 단계에 대해 설명합니다.  
  
4.  [데이터베이스 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)을 업그레이드합니다(**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]). 데이터베이스가 온라인 상태가 된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 새 버전에서 수행해야 하는 단계 중 하나는 데이터베이스 호환성 수준을 변경하여 새 기능을 사용하도록 데이터베이스 기능 모드를 업그레이드하는 것입니다. 이러한 작업은 수동으로 또는 쿼리 튜닝 도우미를 통해 수행할 수 있습니다. 

    - [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용을 수행합니다](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md). 데이터베이스 호환성 수준을 수동으로 변경한 후 쿼리 저장소를 사용하여 성능을 모니터링하고 가능한 재발을 식별할 수 있습니다. 이 문서에서는 권장 프로세스에 대해 설명하고 권장 워크플로를 제공합니다.  

    - [쿼리 튜닝 도우미를 사용하여 데이터베이스 호환성 모드를 변경합니다](../../relational-databases/performance/upgrade-dbcompat-using-qta.md). 또는 수동 변경의 경우에는 데이터베이스 호환성 수준 변경의 권장 프로세스를 통해 안내되는 **QTA(쿼리 튜닝 도우미)** 를 사용합니다. 이 문서에서는 이 프로세스에 대해 설명하고 QTA 워크플로에 대한 지침을 제공합니다.  

    데이터베이스 호환성 수준을 변경한 후 사용할 수 있는 새 기능 및 향상된 동작에 대한 자세한 내용은 [호환성 수준 간의 차이점](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-stored-procedures)을 참조하세요.

5.  [새 SQL Server 기능을 활용하세요](https://www.microsoft.com/sql-server/sql-server-2019). 마지막으로 이전 단계를 모두 완료하고 나면 새 데이터베이스 엔진의 특정 향상 기능을 사용해 볼 수 있습니다. 이 문서에서는 이러한 향상 기능 중 몇 가지를 소개하고 자세한 정보를 확인할 수 있는 링크를 제공합니다.  
  
  
