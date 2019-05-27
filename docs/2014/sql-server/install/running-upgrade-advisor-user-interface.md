---
title: 업그레이드 관리자 (사용자 인터페이스)를 실행 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5aecaea9bef359ad24aebbd20dd5e9547497043b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092453"
---
# <a name="running-upgrade-advisor-user-interface"></a>업그레이드 관리자 실행(사용자 인터페이스)
  업그레이드를 계획하는 동안 업그레이드 관리자를 실행하여 로컬 또는 원격 구성 요소를 분석할 수 있습니다. 업그레이드 관리자는 분석되는 각 구성 요소와 인스턴스에 대한 보고서를 생성합니다.  
  
> [!IMPORTANT]  
>  업그레이드 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 원격 인스턴스를 분석하지 않습니다. [!INCLUDE[ssRS](../../includes/ssrs.md)] 인스턴스를 분석하려면 [!INCLUDE[ssRS](../../includes/ssrs.md)]가 설치된 컴퓨터에 업그레이드 관리자를 설치해야 합니다.  
>   
>  분석할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해야 Integration Services를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 설치 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 동일한 컴퓨터에 설치 합니다.  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>업그레이드 관리자 분석 마법사 실행  
 업그레이드 관리자 분석 마법사는 다음과 같은 여섯 단계로 실행됩니다.  
  
1.  업그레이드 관리자 시작 페이지에서 마법사를 시작합니다.  
  
2.  분석할 서버 및 구성 요소를 식별합니다.  
  
3.  인증 정보를 수집합니다.  
  
4.  구성 요소 유형에 따라 추가 매개 변수를 수집합니다.  
  
5.  선택한 구성 요소를 분석합니다.  
  
6.  업그레이드 문제에 대한 보고서를 생성합니다.  
  
 업그레이드 관리자 분석 마법사에 대 한 자세한 내용은 참조 하세요. [방법: 업그레이드 관리자 분석 마법사 실행](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)합니다.  
  
 각 단계에 필요한 특정 정보를 참조 하세요 [업그레이드 관리자 사용자 인터페이스 참조](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)합니다.  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>업그레이드 관리자 보고서 뷰어 실행  
 업그레이드 관리자 분석 마법사에서 생성된 보고서를 보려면 업그레이드 관리자 보고서 뷰어를 사용합니다. 보고서가 로드되면 다음 요인을 기준으로 보고서의 구성 요소를 필터링할 수 있습니다.  
  
-   모든 문제  
  
-   모든 업그레이드 문제  
  
-   업그레이드 이전 문제  
  
-   모든 마이그레이션 문제  
  
-   해결된 문제  
  
-   해결되지 않은 문제  
  
 보고서 뷰어를 사용하는 방법에 대한 단계별 지침은 다음 항목을 참조하십시오.  
  
-   [방법: 업그레이드 관리자 보고서를 보려면](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [방법: 보고서 필터링](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [방법: 보고서 내보내기](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>관련 항목  
 [방법: 업그레이드 관리자 분석 마법사 실행](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [업그레이드 관리자 사용자 인터페이스 참조](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [업그레이드 문제 해결](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
