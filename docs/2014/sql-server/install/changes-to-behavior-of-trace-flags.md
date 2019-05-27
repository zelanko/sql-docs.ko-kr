---
title: 추적 플래그의 동작 변경 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 447e6d4d35fa77f71f1a7a1b90a5a782e0ccebcc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096617"
---
# <a name="changes-to-behavior-of-trace-flags"></a>추적 플래그의 동작에 대한 변경입니다.
  한 세션에서 설정한 전역 추적 플래그가 다른 세션에 즉시 적용됩니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 일부 추적 플래그는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드하기 전에 추적 플래그를 모두 해제하는 것이 좋습니다. 데이터베이스 가용성이 나 복구 모드를 수정 하는 추적 플래그 하지 못할 수 있습니다 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스를 성공적으로 업그레이드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이러한 추적 플래그는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 필요하고 여전히 유효하다는 것이 확인되면 설정할 수 있습니다. 추적 플래그를 다시 설정해야 하는 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 추가 테스트를 수행해야 합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 전역 및 세션 수준 추적 플래그를 지원합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 DBCC TRACEON 명령에 추가 인수 (-1)을 사용하여 추적 플래그를 로컬 또는 전역으로 지정할 수 있습니다. 이 인수를 지정하지 않으면 기본값은 로컬입니다.  
  
 또한 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서는 A 세션에서 설정한 추적 플래그가 기존 B 세션에서 자동으로 적용되지 않습니다. 대신 B 세션에서 처음으로 추적 플래그를 설정한 후에만 적용됩니다. 이 동작은 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서는 비결정적이지만, A 세션에서 설정한 전역 추적 플래그가 다른 동시 세션에서 즉시 설정되는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 결정적입니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
