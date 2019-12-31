---
title: 소프트웨어 서비스
description: AP (Analytics Platform System)의 소프트웨어 서비스입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4325dfa9c16edba12c2bba694b47c1b0875c7c6f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400310"
---
# <a name="software-servicing-in-analytics-platform-system"></a>분석 플랫폼 시스템의 소프트웨어 서비스
이 섹션에서는 WSUS 및 분석 플랫폼 시스템 핫픽스를 비롯 하 여 분석 플랫폼 시스템 어플라이언스에 대 한 소프트웨어 서비스 요구 사항을 요약 합니다.  
  
## <a name="Basics"></a>소프트웨어 서비스 기본 사항  
**WSUS:** Windows Server Update Services (WSUS)에서 업데이트를 받도록 분석 플랫폼 시스템 어플라이언스를 구성 해야 합니다. 이러한 업데이트에는 어플라이언스 소프트웨어에 대 한 중요 한 변경 내용이 포함 됩니다. 구성 된 후에는 많은 업데이트가 자동으로 설치 되며 실습 관리가 필요 하지 않습니다. 일반적으로 WSUS 업데이트는 새 어플라이언스를 설정 하는 동안 수행 되는 [Windows Server Update Services &#40;wsus&#41; &#40;분석 플랫폼&#41;시스템을 구성](configure-windows-server-update-services-wsus.md) 하는 단계를 구성 합니다. 그렇지 않은 경우이 구성 단계는 나중에 수행할 수 있습니다. WSUS에 대 한 자세한 내용은 [wsus 웹 사이트 가이드](https://go.microsoft.com/fwlink/?LinkId=202417)를 참조 하세요.  
  
**핫픽스:** 또한 분석 플랫폼 시스템 핫픽스를 적용 해야 할 수도 있습니다. *핫픽스* 는 분석 플랫폼 시스템 소프트웨어의 문제를 해결 하기 위해 특정 고객에 게 생성 되는 소프트웨어 업데이트입니다. 각 핫픽스는 고객 관련 문제에 대 한 픽스를 설치 하는 실행 파일입니다. 각 핫픽스에는 Windows, SQL Server 및 분석 플랫폼 시스템에 대해 이전에 릴리스된 모든 소프트웨어 업데이트가 누적 되어 있습니다. 핫픽스를 설치 해야 하는 경우 Microsoft 지원에서 핫픽스와 지침을 제공 합니다.  
  
**업데이트 범위:** 분석 플랫폼 시스템에 핫픽스 또는 Service Pack을 적용 하려면 전체 어플라이언스를 오프 라인으로 전환 해야 합니다.  
  
**SSIS 대상 어댑터 및 클라이언트 도구:** SSIS 대상 어댑터 MSI 또는 클라이언트 도구 MSI에 대 한 변경 내용이 포함 된 핫픽스를 적용 하는 경우 MSI 파일이 제어 노드의 **C:\PDWINST\ClientTools** 디렉터리에 업데이트 됩니다. 핫픽스는 업데이트 된 MSI 파일에서 구성 요소를 자동으로 설치 하지 않습니다. 이러한 구성 요소를 업데이트 하려면 고객이 이전 버전의 구성 요소를 제거 하 고 업데이트 된 MSI 파일에서 새 버전을 설치 해야 합니다. SSIS 대상 어댑터 MSI 또는 클라이언트 도구 MSI에 대 한 변경 내용이 포함 된 핫픽스를 제거 하는 경우 해당 구성 요소에 대 한 MSI 파일은 이전 버전으로 되돌려집니다. 이러한 구성 요소를 이전 버전으로 되돌리려면 고객이 기존 (최신) 버전의 구성 요소를 제거 하 고 되돌린 MSI 파일에서 이전 버전을 다시 설치 해야 합니다.  
  
## <a name="software-servicing-topics"></a>소프트웨어 서비스 항목  
다음 항목에서는 어플라이언스에서 소프트웨어 서비스를 관리 하는 방법을 설명 합니다.  
  
-   [Microsoft 업데이트 &#40;분석 플랫폼 시스템&#41;다운로드 및 적용](download-and-apply-microsoft-updates.md)  
  
-   [Microsoft 업데이트 &#40;분석 플랫폼 시스템을 제거&#41;](uninstall-microsoft-updates.md)  
  
-   [Analytics platform System 핫픽스 &#40;Analytics platform system&#41;적용](apply-analytics-platform-system-hotfixes.md)  
  
-   [분석 플랫폼 시스템 핫픽스 &#40;분석 플랫폼 시스템을 제거&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
