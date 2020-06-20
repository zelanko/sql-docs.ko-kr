---
title: 업그레이드 관리자 진행률 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 692b06051872084ff5e1b16dfaf1f8198a649d62
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062338"
---
# <a name="upgrade-advisor-progress"></a>업그레이드 관리자 진행률
  업그레이드 관리자 분석은 선택된 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소의 분석을 수행하는 전용 분석기를 통해 시작됩니다. 구성 요소가 분석 되 면 **진행률 대화 상자에 진행률이 보고** 됩니다.  
  
## <a name="options"></a>옵션  
 **동작**  
 분석할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 지정합니다.  
  
 **상태**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 진행률 인터페이스에서 반환된 상태 값을 표시합니다.  
  
 **Message**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개별 분석기에서 반환된 오류, 실패 또는 성공 메시지를 표시합니다.  
  
> [!NOTE]  
>  분석이 너무 오래 걸리면 분석을 중지하고 업그레이드 관리자 분석 마법사를 종료한 다음 마법사를 다시 실행할 수 있습니다. 분석 시간을 줄이려면 분석할 구성 요소 수를 줄이십시오.  
  
 분석이 완료되면 보고서가 파일로 작성됩니다. 보고서 **시작** 을 클릭 하 여이 페이지에서 보고서 뷰어를 시작 하 여 보고서를 볼 수 있습니다. 나중에 보고서를 보려면 업그레이드 관리자 시작 페이지에서 **업그레이드 관리자 보고서 뷰어** 를 열 수 있습니다.  
  
> [!NOTE]  
>  이전 보고서는 서버를 분석할 때마다 저장됩니다. 보고서는 파일 이름에 타임스탬프를 사용하여 저장됩니다. 보고서 뷰어에는 가장 최근에 저장된 다섯 개의 보고서가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [방법: 업그레이드 관리자 시작](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [방법: 업그레이드 관리자 분석 마법사 실행](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [SQL Server 구성 요소](../../../2014/sql-server/install/sql-server-components.md)   
 [업그레이드 관리자 사용자 인터페이스 참조](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
