---
title: 업그레이드 관리자 개요 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- SQL Server Upgrade Advisor, components
- tools [Upgrade Advisor]
- Upgrade Advisor [SQL Server], components
- components [Upgrade Advisor]
- Upgrade Advisor Analysis Wizard
- limitations [Upgrade Advisor]
- analyzing system [Upgrade Advisor]
- analyzing system [Upgrade Advisor], about analysis
ms.assetid: f5c56f63-4478-40af-abb9-642f58a0026c
caps.latest.revision: 47
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b30fddb6ce8570b438c869d72c2d3d0ac48036e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315963"
---
# <a name="upgrade-advisor-overview"></a>업그레이드 관리자 개요
  업그레이드 관리자는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 구성 요소를 분석하고 분석 결과에 대한 정보가 포함된 보고서를 볼 수 있는 중앙 콘솔을 제공합니다.  
  
## <a name="how-upgrade-advisor-works"></a>업그레이드 관리자 작동 방식  
 업그레이드 관리자를 실행하면 업그레이드 관리자 시작 페이지가 나타납니다. 업그레이드 관리자 시작 페이지에서 다음을 실행할 수 있습니다.  
  
-   업그레이드 관리자 분석 마법사  
  
-   업그레이드 관리자 보고서 뷰어  
  
-   업그레이드 관리자 도움말  
  
 처음 업그레이드 관리자를 사용할 때 업그레이드 관리자 분석 마법사를 실행하여 서버를 분석합니다. 마법사에 분석이 완료 되 면 클릭 **보고서 시작** 마법사 또는 업그레이드 관리자 시작 페이지를 반환 합니다. 그런 다음 업그레이드 관리자 보고서 뷰어를 실행하여 보고서를 봅니다. 보고서는 알려진 문제를 해결하는 데 도움이 되는 정보에 대한 링크를 제공합니다.  
  
## <a name="upgrade-advisor-analysis-wizard"></a>업그레이드 관리자 분석 마법사  
 분석을 수행 하려면 **업그레이드 관리자 분석 마법사 시작** 업그레이드 관리자 시작 페이지입니다. 업그레이드 관리자 분석 마법사는 컴퓨터, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 및 분석할 추적 파일에 대한 정보를 수집합니다. 모든 정보가 수집되고 확인되고 나면 업그레이드 관리자 분석 마법사는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 분석합니다.  
  
> [!NOTE]  
>  업그레이드 관리자 분석 마법사를 실행할 때마다 별도의 보고서가 생성되고 선택한 구성 요소에 대한 기존 보고서는 덮어쓰여지지 않습니다. 그러나 보고서 뷰어에는 가장 최근의 다섯 개 보고서만 표시됩니다.  
  
 업그레이드 관리자 분석 마법사는 분석 작업을 마치면 분석에 포함된 각 구성 요소에 대해 XML 파일을 만듭니다. XML 파일에는 각 구성 요소에서 발견된 항목 및 문제가 포함됩니다.  
  
### <a name="what-upgrade-advisor-analyzes"></a>업그레이드 관리자의 분석 대상  
 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에 대해 업그레이드 관리자의 컨텍스트에서 전용 분석기가 실행됩니다. 각 분석기의 출력은 해당 구성 요소에 대한 XML 보고서입니다.  
  
 업그레이드 관리자는 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 쿼리합니다.  
  
-   복제, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에이전트, 전체 텍스트 검색 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 포함된 데이터베이스 서버([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이라고도 함)  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
> [!NOTE]  
>  분석 중에 각 분석기는 로그 파일을 작성합니다. 이러한 로그 파일을 사용하여 분석 문제를 해결할 수 있습니다. 예를 들어 업그레이드 관리자의 실행 속도가 느린 경우 로그 파일을 통해 속도 지연의 원인을 파악할 수 있습니다.  
  
### <a name="upgrade-advisor-limitations"></a>업그레이드 관리자 제한 사항  
 업그레이드 관리자는 업그레이드에 영향을 미칠 수 있는 문제를 모두 검색하지는 못합니다. 예를 들어 최종 사용자 데스크톱에서 실행되는 클라이언트 응용 프로그램에 SQL 코드를 삽입한 경우 업그레이드 관리자는 이 응용 프로그램을 분석할 수 없습니다. 이러한 항목에 대해서도 문제를 고려하여 각자 설치 기반의 필요에 따라 정보를 업그레이드, 마이그레이션 또는 수정해야 합니다.  
  
 업그레이드 관리자는 암호화된 저장 프로시저, 확장 저장 프로시저의 코드, 그리고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이외의 다른 언어로 된 소스 코드를 분석하지 않습니다.  
  
## <a name="upgrade-advisor-report-viewer"></a>업그레이드 관리자 보고서 뷰어  
 업그레이드 관리자 보고서를 보려면 클릭 **업그레이드 관리자 보고서 뷰어 시작** 업그레이드 관리자 시작 페이지입니다. 업그레이드 관리자 보고서 뷰어를 시작하면 기본 디렉터리의 보고서가 로드됩니다. 업그레이드 관리자 보고서 뷰어가 기본 디렉터리에서 보고서를 찾지 못한 경우 보고서는 표시되지 않습니다. 기본 디렉터리에 보고서가 없는 경우에는 업그레이드 관리자 분석 마법사를 실행하여 보고서를 작성하거나 다른 서버 또는 하위 디렉터리에서 기존 보고서를 로드할 수 있습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자는 기존 보고서를 덮어쓰지 않습니다. 그러나 보고서 뷰어에는 가장 최근의 다섯 개 보고서만 표시됩니다. 이전 보고서를 보려면 보고서를 선택 합니다 **보고서** 드롭다운 목록 상자입니다. 타임스탬프는 보고서가 생성된 날짜와 시간을 나타냅니다.  
  
 업그레이드 관리자 분석 마법사를 통해 작성된 XML 파일이 업그레이드 관리자 보고서 뷰어에 로드되면 각 구성 요소에 대한 보고서가 표시됩니다. 이 보고서에는 처리해야 할 모든 알려진 문제가 포함됩니다(검색 가능한 문제와 검색 불가능한 문제 모두). 각 문제에는 중요도를 나타내는 아이콘, 문제를 처리해야 하는 시기를 알려 주는 레이블, 그리고 간단한 설명이 표시됩니다. 문제를 확장하면 보다 자세한 설명, 문제 세부 정보로 연결되는 링크, 도움말 파일로 연결되는 링크가 표시됩니다. 각 문제에 대한 정보는 문제 해결을 위해 필요한 정보를 충분히 제공하도록 고안되었습니다.  
  
 대부분의 구성 요소에는 검색되지 않는 문제가 있습니다. 이러한 문제를 보려면 확장 합니다 **기타 업그레이드 문제** 구성 요소에 대 한 항목 및 설명서에서 문제에 대 한 추가 정보를 보려면 링크를 클릭 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전과의 호환성 문제에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
