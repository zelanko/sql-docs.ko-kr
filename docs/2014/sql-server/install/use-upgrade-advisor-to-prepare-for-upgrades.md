---
title: 업그레이드 관리자를 사용 하 여 업그레이드 준비 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server]
- upgrading SQL Server, Upgrade Advisor
- upgrading SQL Server, preparing to upgrade
- SQL Server Upgrade Advisor
- analyzing installations for upgrading [SQL Server]
ms.assetid: d85b0833-ddeb-42e3-9397-97ea60d521b7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce60db3b720b046c44d7507d3164c2f2e6c9173f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091263"
---
# <a name="use-upgrade-advisor-to-prepare-for-upgrades"></a>업그레이드 관리자를 사용하여 업그레이드 준비
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 관리자는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로의 업그레이드를 준비할 수 있도록 도와 줍니다. 업그레이드 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전에서 설치된 구성 요소를 분석한 다음 업그레이드 전이나 후에 해결해야 할 문제를 보여 주는 보고서를 생성합니다.  
  
## <a name="how-upgrade-advisor-works"></a>업그레이드 관리자 작동 방식  
 업그레이드 관리자를 실행하면 업그레이드 관리자 홈 페이지가 나타납니다. 홈 페이지에서 다음 도구를 실행할 수 있습니다.  
  
-   업그레이드 관리자 분석 마법사  
  
-   업그레이드 관리자 보고서 뷰어  
  
-   업그레이드 관리자 도움말  
  
 처음 업그레이드 관리자를 사용할 때 업그레이드 관리자 분석 마법사를 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 분석합니다. 마법사가 분석을 완료하면 업그레이드 관리자 보고서 뷰어에서 결과 보고서를 볼 수 있습니다. 각 보고서에는 알려진 문제를 해결하거나 그 영향을 줄이는 데 도움이 되는 업그레이드 관리자 도움말의 정보에 대한 링크가 들어 있습니다.  
  
## <a name="upgrade-advisor-analysis"></a>업그레이드 관리자 분석  
 업그레이드 관리자는 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 분석합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
 분석 작업은 스크립트,  저장 프로시저,  트리거,  추적 파일 등 액세스할 수 있는 개체를 검사합니다. 업그레이드 관리자는 데스크톱 애플리케이션 또는 암호화된 저장 프로시저를 분석할 수 없습니다.  
  
 출력 형식은 XML  보고서입니다. XML  보고서를 보려면 업그레이드 관리자 보고서 뷰어를 사용하십시오.  
  
> [!NOTE]  
>  보고서에는 "기타 업그레이드 문제"  항목이 들어 있을 수 있습니다. 이 항목은 업그레이드 관리자에 의해 감지되지는 않았지만 서버 또는 애플리케이션에 있을 수 있는 문제 목록에 대한 링크를 제공합니다. 발견할 수 없는 문제 목록을 검토하고 이런 문제로 인해 서버 또는 애플리케이션을 변경해야 하는지 여부를 결정해야 합니다.  
  
## <a name="how-to-install-and-run-upgrade-advisor"></a>업그레이드 관리자 설치 및 실행 방법  
 설치 위치 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 관리자는 분석 대상에 따라 달라 집니다. 업그레이드 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 제외하고 지원되는 모든 구성 요소의 원격 분석을 지원합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 검색하지 않는 경우 사용자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있거나 업그레이드 관리자의 필수 구성 요소가 있는 모든 컴퓨터에 업그레이드 관리자를 설치할 수 있습니다. 자세한 내용은 [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하세요. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 인스턴스를 검색하는 경우에는 보고서 서버에 업그레이드 관리자를 설치해야 합니다.  
  
 업그레이드 관리자는 기능 팩으로 제공됩니다.  
  
 업그레이드 관리자 설치 및 실행을 위한 필수 구성 요소는 다음과 같습니다.  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2, Windows 7 SP1 및 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1.  
  
-   Windows  Installer  4.5  버전 이상 Windows Installer를 설치할 수는 [Windows Installer 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=49112)합니다.  
  
-   Microsoft .NET Framework 4 .NET framework 4에서 사용할 수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 제품 미디어 및 합니다 [.NET Framework 4 다운로드 페이지](https://go.microsoft.com/fwlink/?LinkId=209895)합니다.  
  
    -   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 미디어에서 .NET  Framework  4를 설치하려면 디스크 드라이브의 루트를 찾습니다. 그런 다음 \redist  폴더와 DotNetFrameworks  폴더를 차례로 두 번 클릭하고 dotNetFx40_Full_x86_x64.exe(32비트 운영 체제 및 64비트 운영 체제용)를 실행합니다.  
  
 웹에서 업그레이드 관리자를 설치하려면 다운로드 페이지에서 다운로드 단추를 클릭합니다. 그러면 설치를 바로 실행할 수 있으며 나중에 설치하기 위해 SQLUA.msi  파일을 저장할 수도 있습니다. 제품 디스크를 사용해서 설치하는 경우에는 제품 디스크에서 SQLUA.msi  파일을 직접 실행합니다.  
  
 업그레이드 관리자를 설치한 후에서 열 수 있습니다 합니다 **시작** 메뉴:  
  
-   클릭 **시작**, 가리킨 **모든 프로그램**를 가리킨 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]를 클릭 하 고  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자**.  
  
 자세한 내용은 업그레이드 관리자 다운로드에 포함된 업그레이드 관리자 설명서 및 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 릴리스 정보를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [여러 버전 및 인스턴스의 SQL Server 작업](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [이전 버전과의 호환성](../../../2014/getting-started/backward-compatibility.md)  
  
  
