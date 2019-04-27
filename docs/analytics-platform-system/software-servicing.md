---
title: 소프트웨어 서비스-Analytics Platform System | Microsoft Docs
description: Analytics Platform System (APS)에서 서비스 하는 소프트웨어입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 444d7f29e7f65da7e5d98dde310b2c1f8ad8dd4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678385"
---
# <a name="software-servicing-in-analytics-platform-system"></a>Analytics Platform System에서 소프트웨어 서비스
이 섹션에는 소프트웨어 서비스 분석 플랫폼 시스템 어플라이언스, WSUS 및 Analytics Platform System 핫픽스를 포함 하 여에 대 한 요구 사항을 요약 합니다.  
  
## <a name="Basics"></a>소프트웨어 서비스 기본 정보  
**WSUS:** 분석 플랫폼 시스템 어플라이언스 업데이트를 Windows Server Update Services (WSUS)에서 수신 하도록 구성 해야 합니다. 이러한 업데이트에는 어플라이언스 소프트웨어의 중요 한 변경 내용을 포함 합니다. 를 구성한 후 많은 업데이트는 자동으로 설치 됩니다 및 실습 관리가 필요 하지 않습니다. WSUS 업데이트 하는 동안 일반적으로 구성 되는 [구성 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41; ](configure-windows-server-update-services-wsus.md) 단계 새 어플라이언스 설치 중 수행 합니다. 그렇지 않은 경우이 구성 단계를 나중에 수행할 수 있습니다. WSUS에 대 한 내용은 참조는 [WSUS 웹 사이트 가이드](https://go.microsoft.com/fwlink/?LinkId=202417)합니다.  
  
**핫픽스:** 또한, Analytics Platform System 핫픽스를 적용 해야 합니다. A *핫픽스* Analytics Platform System 소프트웨어를 사용 하 여 문제를 해결 하는 특정 고객에 대해 만든 소프트웨어 업데이트입니다. 각 핫픽스는 고객 관련 문제에 대 한 수정 프로그램을 설치 하는 실행 파일. 또한 각 핫픽스는 Windows, SQL Server 및 Analytics Platform System에 대 한 모든 이전에 릴리스된 소프트웨어 업데이트의 누적 포함 되어 있습니다. 핫픽스를 설치 해야 할 경우 Microsoft 지원으로 핫픽스 및 지침을 사용 하 여 제공 합니다.  
  
**업데이트의 범위.** Analytics Platform System 핫픽스 또는 서비스 팩을 적용 전체 어플라이언스 오프 라인으로 수행 해야 합니다.  
  
**SSIS 대상 어댑터 및 클라이언트 도구:** SSIS 대상 어댑터 MSI의 변경 내용을 포함 하는 핫픽스를 적용 하는 경우 또는 클라이언트 도구 MSI에서 MSI 파일 업데이트 됩니다 합니다 **C:\PDWINST\ClientTools** 제어 노드에 디렉터리입니다. 핫픽스 업데이트 된 MSI 파일에서 구성 요소를 자동으로 설치 하지 않습니다. 이러한 구성 요소를 업데이트 하려면 고객 구성 요소의 이전 버전을 제거 하 고 업데이트 된 MSI 파일에서 새 버전을 설치 해야 합니다. SSIS 대상 어댑터 MSI의 변경 내용을 포함 하는 핫픽스를 제거 하는 경우 또는 클라이언트 도구 MSI에 해당 구성 요소에 대 한 MSI 파일을 이전 버전으로 되돌려집니다. 이러한 구성 요소를 이전 버전으로 되돌리려면 고객 기존 (최신) 버전의 구성 요소를 제거 하 고 되돌린된 MSI 파일에서 이전 버전을 다시 설치 해야 합니다.  
  
## <a name="software-servicing-topics"></a>소프트웨어 항목을 서비스  
다음 항목 어플라이언스에서 소프트웨어 서비스를 관리 하는 방법에 설명 합니다.  
  
-   [Microsoft 업데이트 다운로드 및 적용 &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [Microsoft 업데이트를 제거할 &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [Analytics Platform System 핫픽스 적용 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Analytics Platform System 핫픽스 제거 &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
