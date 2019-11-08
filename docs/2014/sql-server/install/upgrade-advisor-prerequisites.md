---
title: 업그레이드 관리자 필수 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- requirements [Upgrade Advisor]
- software [Upgrade Advisor]
- system requirements [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, prerequisites
- prerequisites [Upgrade Advisor]
- Upgrade Advisor [SQL Server], prerequisites
ms.assetid: d21a39e5-5f81-4096-a7dd-f244e4779992
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5875ad2268e14d6bbe276ea437c5ee201867105e
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632778"
---
# <a name="upgrade-advisor-prerequisites"></a>업그레이드 관리자 필수 구성 요소
  이 항목에서는 업그레이드 관리자를 위한 소프트웨어 요구 사항에 대해 설명합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 업그레이드 관리자 설치 및 실행을 위한 필수 구성 요소는 다음과 같습니다.  
  
-   [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] SP1, [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2, Windows 7 또는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] R2  
  
-   Windows Installer 4.5. [Windows Installer 웹 사이트](https://www.microsoft.com/download/details.aspx?id=8483)에서 Windows Installer를 설치할 수 있습니다.  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)](.NET Framework 4부터 해당). [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 제품 미디어와 [SDK, 재배포 가능 및 Service Pack 다운로드 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=48882)에서 사용할 수 있습니다.  
  
    -   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 미디어에서 .NET  Framework  4를 설치하려면 디스크 드라이브의 루트를 찾습니다. 그런 다음 \redist 폴더와 DotNetFrameworks 폴더를 차례로 두 번 클릭하고 dotNetFx40_Full_x86_x64.exe(32비트 및 64비트 운영 체제 모두의 경우)를 실행합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자를 설치 하기 위한 필수 구성 요소 이며 업그레이드 관리자 설치 프로그램으로 설치 되지 않습니다. 설치 프로그램을 실행 하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능 팩에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom [!INCLUDE[msCoName](../../includes/msconame-md.md)]를 다운로드 하 여 설치 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [방법: 업그레이드 관리자 설치](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)  
  
  
