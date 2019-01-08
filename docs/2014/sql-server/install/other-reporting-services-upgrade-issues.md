---
title: 다른 Reporting Services 업그레이드 문제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- command line setup [Reporting Services]
- Setup commands [Reporting Services]
- multivalued parameters [Reporting Services]
- WMI provider [Reporting Services]
- compile errors [Reporting Services]
- single-valued parameters [Reporting Services]
- data processing extensions [Reporting Services]
- report compilation errors [Reporting Services]
- authentication [Reporting Services]
ms.assetid: 42dd2f06-1de9-449e-ab9d-f4ef25f8b728
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: af30ed5d0e275353691e506dd49eeaebcea10d3e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353687"
---
# <a name="other-reporting-services-upgrade-issues"></a>기타 Reporting Services 업그레이드 문제
  이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 업그레이드할 때 발생할 수 있는 문제에 대해 설명합니다. **이러한 문제는 업그레이드 관리자가 검색 되지 않습니다.** 자세한 내용은 참조 하세요. [SQL Server 2014 릴리스 정보](https://go.microsoft.com/fwlink/?LinkID=296445)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
|문제점|Description|적용 대상|  
|-----------|-----------------|----------------|  
|SharePoint 팜 업그레이드|팜에서 다른 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소가 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 업그레이드된 다음에만 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 공유 서비스를 업그레이드합니다.<br /><br /> 업그레이드할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 다중 노드 SharePoint 팜을 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 모든 인스턴스를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능에 SharePoint 팜에서 업그레이드 해야 합니다는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 버전 업그레이드 하기 전에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스입니다.<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스가 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]로 업그레이드되었지만 팜에 있는 다른 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소가 여전히 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전인 경우 보고서 렌더링이 실패합니다.<br /><br /> <br /><br /> 자세한 내용은 [SQL Server 2014 Reporting Services 팁, 요령 및 문제 해결](https://go.microsoft.com/fwlink/?LinkID=391254)을 참조하십시오.|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|  
|함께 설치|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드는 다음 중 하나와 함께 실행될 수 없습니다.<br /><br /> SharePoint용 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스<br /><br /> <br /><br /> 나란히 설치를 방지 합니다 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 Windows 서비스가 시작 합니다. Windows 이벤트 로그에 다음과 비슷한 오류 메시지가 표시됩니다.<br /><br /> 설명: 보고서 서버 데이터베이스 버전이 잘못되었습니다.<br /><br /> 설명: 보고서 서버[서버 이름]에서 보고서 서버 데이터베이스에 연결할 수 없습니다.|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 기본 모드|  
|실패한 업그레이드를 복구하는 동안의 오류|**문제점:** 업그레이드에 실패한 후 복구를 실행하려고 했습니다. 복구 작업도 실패하고 설치 로그 파일에 다음과 유사한 메시지가 나타납니다.<br /><br /> `(01) 2011-10-27 12:23:15 Slp:` <br /> `(01) 2011-10-27 12:23:15 Slp: Exception type: System.Exception` <br /> `(01) 2011-10-27 12:23:15 Slp:     Message:`  <br /> `(01) 2011-10-27 12:23:15 Slp:         SQLPath element is missing` <br /> `(01) 2011-10-27 12:23:15 Slp:     Data:`  <br /> `(01) 2011-10-27 12:23:15 Slp:       SQL.Setup.FailureCategory = ConfigurationFailure`<br /><br /> 로그 파일에 대 한 자세한 내용은 참조 하세요. [뷰와 Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)합니다.<br /><br /> **해결 방법:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 제거한 후 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 다시 설치해야 합니다. 더 이상 업그레이드할 수 없습니다.|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|  
|대화형 작업 정보가 마지막 요청에 대해서만 저장됨|이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 스냅숏에 드릴스루 정보, 토글 선택과 같은 상호 작용 선택의 가능한 모든 조합이 저장되었습니다. 예를 들어 토글에 대한 올바른 ID를 추적하여 보고서의 5페이지를 보면서 프로그래밍 방식으로 1페이지의 항목을 토글할 수 있었습니다.<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서는 상호 작용 정보가 마지막 렌더링 요청에 대해서만 생성 및 저장됩니다. 한 페이지를 보면서 다른 페이지의 항목을 프로그래밍 방식으로 토글할 수 없습니다. 현재 보고서 페이지에 있는 드릴다운 항목만 토글할 수 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|렌더링 및 페이지 매김이 변경됨|개체 모델 (ROM (렌더링) 변경 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]합니다. 이전 버전의 렌더링 개체 모델은 더 이상 지원되지 않습니다. 다중 스레드 렌더링 확장 프로그램에서의 렌더링 개체 모델 액세스와 다중 스레드에서의 컨텍스트 전환은 지원되지 않습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|CSV 내보내기 형식이 다시 디자인됨|이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 보고서를 CSV 파일 형식으로 내보내면 데이터의 형식이 보고서 페이지에 데이터가 표시되는 방식을 그대로 유지하도록 지정되었습니다. 이러한 동작으로 인해 행렬 데이터 영역의 데이터 형식은 다른 응용 프로그램으로 가져오기가 불편했습니다.<br /><br /> 이 릴리스에서는 보고서를 CSV 파일로 내보낼 때 두 가지 지원되는 형식, 즉 기본 모드와 규격 모드 중에서 선택할 수 있습니다. 기본 모드는 Excel에, 규격 모드는 타사 애플리케이션에 사용할 수 있도록 최적화되어 있습니다.<br /><br /> 이전 형식의 CSV 파일은 더 이상 지원되지 않습니다. 그러나 행렬 데이터 영역을 사용하지 않는 보고서의 경우 규격 모드를 사용하면 이전 CSV 파일 형식에 최대한 가까운 파일 형식을 얻을 수 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|페이지 머리글과 바닥글의 조건부 표시 유형 집계|이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 다양한 렌더러가 다양한 규칙을 사용하여 보고서 페이지에 포함할 조건부 표시 유형 항목을 결정했습니다. 예를 들어 인쇄된 보고서의 숨겨진 항목에 대해서는 집계 계산이 수행되지 않았지만 브라우저 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel에서 보는 보고서의 숨겨진 항목에 대해서는 집계 계산이 수행되었습니다.<br /><br /> 이 릴리스에서는 모든 렌더러가 동일한 규칙 집합을 사용하여 페이지에 표시할 항목을 결정합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|Excel에서 수식이 지원되지 않음|이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 RDL 식을 Excel 수식으로 변환하는 기능이 제한적으로 제공되었습니다. 이 릴리스에서는 보고서를 Excel로 내보낼 때 RDL 식이 Excel 수식으로 변환되지 않습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|항목이 겹침|이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 보고서 디자인 화면에 겹치는 항목이 있는 경우 보고서를 게시할 때 경고("겹치는 보고서 항목은 일부 렌더러에서만 지원됩니다.")가 발생했지만 해당 보고서 항목은 디자인 화면에서 원래 위치를 유지했습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서는 겹치는 항목을 지원하지 않는 렌더러로 보고서를 내보내거나 보고서를 보는 경우 겹치는 경계를 수정하기 위해 보고서 항목을 이동할 수 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|보고서 개체 모델 네임스페이스가 변경됨|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], 보고서 개체 모델 네임 스페이스가 변경 되었습니다. 이 네임스페이스는 사용자 지정 코드에서 `Fields`, `Parameters`, `ReportItems` 등의 전역 컬렉션으로 읽기 전용 액세스를 제공합니다. 기존 사용자 지정 코드가 이전 네임스페이스에 대한 정규화된 참조를 명시적으로 사용하는 경우 이 변경 사항은 주요 변경 내용에 해당합니다.<br /><br /> 코드에서 정규화된 참조를 사용하여 기본 제공 컬렉션에 액세스하지 않는 것이 좋습니다. 네임스페이스를 명시적으로 지정하지 않으면 사용자 지정 코드 참조가 현재 설치된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전에 대한 보고서 개체 모델의 버전으로 확인됩니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005의 보고서 서버 WMI(Windows Management Instrumentation) 공급자가 지원되지 않음|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에는 보고서 서버가 실행되는 환경을 프로그래밍 방식으로 구성하는 데 사용할 수 있는 WMI 공급자가 포함되어 있습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 릴리스에는 이전 버전을 완전히 대체하는 새 버전의 WMI 공급자가 포함되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 및 2005 버전은 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 지원되지 않습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|업그레이드된 보고서 서버에서 SPN(서비스 사용자 이름)이 다시 생성되지 않음|보고서 서버 웹 서비스용 SPN을 만든 경우 업그레이드된 보고서 서버에 대해서도 제한된 위임이 계속 작동하는지 확인하십시오.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|사용자 지정 어셈블리는 새 설치 폴더에 수동으로 이동해야 함|사용자 지정 어셈블리는 업그레이드 관리자에 의해 검색되지 않으므로 보고서에 사용자 지정 기능을 사용하여 계속하려는 경우 새 설치 폴더에 수동으로 이동해야 합니다.<br /><br /> 이러한 어셈블리는 보고서 서버 설치 폴더에 설치되며 업그레이드가 완료된 후 새 설치 폴더에 이동해야 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 업그레이드 문제 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
