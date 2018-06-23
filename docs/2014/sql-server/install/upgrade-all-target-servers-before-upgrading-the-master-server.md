---
title: 마스터 서버를 업그레이드 하기 전에 모든 대상 서버를 업그레이드 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fdd218b1d5bfaacaffbd50c50d55dd47d613d207
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180772"
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
  
 자세한 내용은 항목을 참조는 "자동화 기업 내 관리," "어떻게를:: 오류는 대상 서버에서 마스터 서버" 및 "방법:: 참여 정도 대상 서버에는 마스터에"에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 업그레이드 문제](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [SQL Server 에이전트 업그레이드 문제](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  