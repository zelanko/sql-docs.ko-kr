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
manager: craigg
ms.openlocfilehash: 697f70d4435213a991e55adecb51a98120d8df1b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091557"
---
# <a name="upgrade-advisor-progress"></a>업그레이드 관리자 진행률
  업그레이드 관리자 분석은 선택된 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소의 분석을 수행하는 전용 분석기를 통해 시작됩니다. 진행률을 보고 구성 요소가 분석 되는 **진행률** 대화 상자.  
  
## <a name="options"></a>변수  
 **동작**  
 분석할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 지정합니다.  
  
 **상태**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 진행률 인터페이스에서 반환된 상태 값을 표시합니다.  
  
 **메시지**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개별 분석기에서 반환된 오류, 실패 또는 성공 메시지를 표시합니다.  
  
> [!NOTE]  
>  분석이 너무 오래 걸리면 분석을 중지하고 업그레이드 관리자 분석 마법사를 종료한 다음 마법사를 다시 실행할 수 있습니다. 분석 시간을 줄이려면 분석할 구성 요소 수를 줄이십시오.  
  
 분석이 완료되면 보고서가 파일로 작성됩니다. 클릭 하 여 보고서를 볼 수 있습니다 **보고서 시작** 이 페이지에서 보고서 뷰어를 시작 합니다. 나중에 보고서를 보려는 경우 열 수 있습니다 합니다 **업그레이드 관리자 보고서 뷰어** 업그레이드 관리자 시작 페이지에서.  
  
> [!NOTE]  
>  이전 보고서는 서버를 분석할 때마다 저장됩니다. 보고서는 파일 이름에 타임스탬프를 사용하여 저장됩니다. 보고서 뷰어에는 가장 최근에 저장된 다섯 개의 보고서가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [방법: 업그레이드 관리자 시작](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [방법: 업그레이드 관리자 분석 마법사 실행](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [SQL Server 구성 요소](../../../2014/sql-server/install/sql-server-components.md)   
 [업그레이드 관리자 사용자 인터페이스 참조](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
