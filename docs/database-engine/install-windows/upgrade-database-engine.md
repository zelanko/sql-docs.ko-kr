---
title: 데이터베이스 엔진 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 99d1b87ac5584f05911ebfb16387babc408e26f5
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600933"
---
# <a name="upgrade-database-engine"></a>데이터베이스 엔진 업그레이드

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  이 섹션의 문서에서는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진을 업그레이드하는 방법을 설명합니다.  
  
1.  [데이터베이스 엔진 업그레이드 방법 선택](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md) 업그레이드를 시작하기 전에 다양한 업그레이드 방법을 이해해야 합니다. 이 문서에서는 업그레이드 방법 및 각 업그레이드 방법에서 수행하는 단계를 설명합니다.  
  
2.  [데이터베이스 엔진 업그레이드 계획 및 테스트](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md) 업그레이드 방법을 검토하고 나면 환경에 적합한 업그레이드 방법을 개발하여 테스트한 후 기존 환경을 업그레이드할 수 있습니다. 이 문서에서는 업그레이드 계획을 개발하고 테스트하는 방법에 대해 설명합니다.  
  
3.  [데이터베이스 엔진 업그레이드 완료](../../database-engine/install-windows/complete-the-database-engine-upgrade.md) 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 업그레이드한 후에는 새 백업 만들기, 새 기능 설정, 전체 텍스트 카탈로그 다시 채우기 등의 추가 단계를 수행해야 합니다. 이 문서에서는 해당 단계에 대해 설명합니다.  
  
4.  [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md) 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 으로 업그레이드한 후에 수행하는 단계 중 하나는 데이터베이스 호환성 모드를 변경한 다음 쿼리 저장소를 사용해 성능을 모니터링하여 새 기능을 사용하도록 설정하는 것입니다. 이 문서에서는 해당 프로세스에 대해 설명하고 권장 워크플로를 제공합니다.  
  
5.  [새 SQL Server 기능 활용](https://www.microsoft.com/sql-server/sql-server-2017) 마지막으로 이전 단계를 완료한 후에는 새 데이터베이스 엔진의 특정 향상 기능을 사용해 볼 수 있습니다. 이 문서에서는 이러한 향상 기능 중 몇 가지를 소개하고 자세한 정보를 확인할 수 있는 링크를 제공합니다.  
  
  
