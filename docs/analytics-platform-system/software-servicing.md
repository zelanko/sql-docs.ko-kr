---
title: 소프트웨어 설치-분석 플랫폼 시스템 | Microsoft Docs
description: Analytics Platform System (APS)에서 서비스 하는 소프트웨어입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7d9991dfb310e2cebc3c61bbd6f9f04a40a0f38e
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="software-servicing-in-analytics-platform-system"></a>분석 플랫폼 시스템에 소프트웨어 처리
이 섹션에는 소프트웨어 서비스 분석 플랫폼 시스템 기기, WSUS 및 분석 플랫폼 시스템 핫픽스를 포함 하 여에 대 한 요구 사항을 요약 합니다.  
  
## <a name="Basics"></a>소프트웨어 서비스 기본 사항  
**WSUS:** 분석 플랫폼 시스템 어플라이언스를 Windows Server Update Services (WSUS)에서 업데이트를 수신 하도록 구성 해야 합니다. 이러한 업데이트에는 원격 클라이언트 컴퓨터에 중요 한 변경이 포함 됩니다. 구성 된 후에 업데이트가 여러 번 수행 자동으로 설치 되 고 직접 관리가 필요 하지 않습니다. WSUS 업데이트 하는 동안 일반적으로 구성 되는 [Windows Server Update Services를 구성 &#40;WSUS&#41; &#40;분석 플랫폼 시스템&#41; ](configure-windows-server-update-services-wsus.md) 새 어플라이언스에 설치 하는 동안 단계를 수행 합니다. 그렇지 않은 경우이 구성 단계를 나중에 수행할 수 있습니다. WSUS에 대 한 자세한 내용은 참조는 [WSUS 웹 사이트 가이드](http://go.microsoft.com/fwlink/?LinkId=202417)합니다.  
  
**핫픽스:** 또한 분석 플랫폼 시스템 핫픽스를 적용 하려면 할 수 있습니다. A *핫픽스* 분석 플랫폼 시스템 소프트웨어로 문제를 해결 하려면 특정 고객에 대해 생성 하는 소프트웨어 업데이트 합니다. 각 핫픽스는 고객 관련 문제에 대 한 수정 프로그램을 설치 하는 실행 파일입니다. 각 핫픽스는 Windows, SQL Server 및 분석 플랫폼 시스템에 대 한 모든 이전에 릴리스된 소프트웨어 업데이트의 누적도 포함 됩니다. 핫픽스를 설치 해야 할 경우 Microsoft 지원으로 핫픽스 및 지침과 함께 제공 합니다.  
  
**업데이트의 범위:** 분석 플랫폼 시스템에는 서비스 팩 이나 핫픽스를 적용 전체 기기를 오프 라인으로 수행 해야 합니다. 즉, PDW와 HDInsight 영역 영향을 받을 수 있습니다.  
  
**SSIS 대상 어댑터 및 클라이언트 도구:** SSIS 대상 어댑터 MSI의 변경 내용이 포함 된 핫픽스를 적용 하는 경우 또는 클라이언트 도구 MSI에서 MSI 파일 업데이트 됩니다는 **C:\PDWINST\ClientTools** 에 제어 노드에 디렉터리입니다. 핫픽스 업데이트 된 MSI 파일에서 구성 요소를 자동으로 설치 되지 않습니다. 이러한 구성 요소를 업데이트 하려면 고객은 이전 버전의 구성 요소를 제거 하 고 업데이트 된 MSI 파일에서 새 버전을 설치 해야 합니다. SSIS 대상 어댑터 MSI의 변경 내용이 포함 된 핫픽스를 제거 하는 경우 또는 클라이언트 도구 MSI, 해당 구성 요소에 대 한 MSI 파일 이전 버전으로 되돌립니다. 이러한 구성 요소는 이전 버전으로 되돌리려면 고객의 구성 요소를 기존 (최신) 버전을 제거 하 고 되돌린된 MSI 파일에서 이전 버전을 다시 설치 해야 합니다.  
  
## <a name="software-servicing-topics"></a>소프트웨어 항목을 서비스  
다음 항목에는 소프트웨어 기기에서 서비스를 관리 하는 방법을 설명 합니다.  
  
-   [다운로드 하 여 Microsoft 업데이트 적용 &#40;분석 플랫폼 시스템&#41;](download-and-apply-microsoft-updates.md)  
  
-   [업데이트 제거 &#40;분석 플랫폼 시스템&#41;](uninstall-microsoft-updates.md)  
  
-   [분석 플랫폼 시스템 핫픽스를 적용 &#40;분석 플랫폼 시스템&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [분석 플랫폼 시스템 핫픽스 제거 &#40;분석 플랫폼 시스템&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
