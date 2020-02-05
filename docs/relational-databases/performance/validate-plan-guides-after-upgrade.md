---
title: 업그레이드 후 계획 지침의 유효성 검사 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 35f02764a62d780819ba0ee4549d3f307df72af4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67986740"
---
# <a name="validate-plan-guides-after-upgrade"></a>업그레이드 후 계획 지침의 유효성 검사
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  새로운 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 애플리케이션을 업그레이드할 때는 계획 지침 정의를 다시 평가하고 테스트하는 것이 좋습니다. 성능 조정 요구 사항과 계획 지침 일치 동작은 변경될 수 있습니다. 잘못된 계획 지침으로 인해 쿼리가 실패하지는 않지만 이 경우 계획 지침을 사용하지 않은 채 계획이 컴파일되므로 최상의 선택이 아닐 수 있습니다. 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후에는 다음 태스크를 수행하는 것이 좋습니다.  
  
-   [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md) 함수를 사용하여 기존 계획 지침의 유효성을 검사합니다.  
  
-   확장 이벤트에서 [Plan Guide Unsuccessful](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md) 이벤트를 사용하여 일정 기간 동안 잘못된 계획 지침이 있는지 모니터링합니다.  
  
  
