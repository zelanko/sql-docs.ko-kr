---
title: 마스터 서버를 업그레이드 하기 전에 모든 대상 서버 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 031fedc4af4b058704cef1da8df846397b235305
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065140"
---
# <a name="upgrade-all-target-servers-before-upgrading-the-master-server"></a>마스터 서버를 업그레이드하기 전에 모든 대상 서버를 업그레이드합니다.
  마스터 서버를 업그레이드하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있고 대상 서버로 구성된 모든 컴퓨터를 업그레이드합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트  
  
## <a name="description"></a>Description  
 다중 서버 환경에서 관리를 자동화하려면 마스터 서버와 대상 서버가 적어도 하나씩 있어야 합니다. 마스터 서버는 대상 서버에 작업을 배포하거나 대상 서버에서 이벤트를 받습니다. 또한 마스터 서버에서는 대상 서버에서 실행되는 작업에 대한 작업 정의의 중앙 복사본을 저장합니다.  
  
 현재 서버가 마스터 서버로 구성된 경우 마스터 서버를 업그레이드하기 전에 모든 대상 서버를 업그레이드합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 마스터 서버를 업그레이드하기 전에 모든 대상 서버를 업그레이드할 수 없는 경우 대상 서버를 모두 제거하고 업그레이드한 후 대상 서버를 모두 다시 등록해야 합니다.  
  
 자세한 내용은 온라인 설명서의 "엔터프라이즈에서 관리 자동화", "How to: 대상 서버에서 마스터 서버에서 대상 서버 제거" 및 "방법: 대상 서버를 마스터에 등록" 항목을 참조 하십시오 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 SQL Server 에이전트](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [SQL Server 에이전트 업그레이드 문제](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
