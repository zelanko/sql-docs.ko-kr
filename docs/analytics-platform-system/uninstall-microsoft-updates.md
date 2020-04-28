---
title: Microsoft Update 제거
description: Microsoft 업데이트를 APS (Analytics Platform System)에서 제거 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a5ebe1ee911f7500505cdbd1962d28c35461a635
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399462"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 Microsoft 업데이트 제거
이 문서에서는 분석 플랫폼 시스템 어플라이언스에서 이전에 설치 된 Microsoft 업데이트를 제거 하는 방법을 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>사전 요구 사항  
이러한 단계를 수행 하려면 다음이 필요 합니다.  
  
-   어플라이언스를 모니터링 하기 위해 관리 콘솔에 액세스할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인입니다.  
  
-   <em> <Fabric Domain> </em> **-HST01** 노드에 로그인 하기 위한 패브릭 도메인 관리자 계정에 대 한 정보입니다.  
  
## <a name="to-uninstall-microsoft-updates"></a><a name="HowToUninstallMSFT"></a>Microsoft 업데이트를 제거 하려면  
  
1.  -HST01 노드에 패브릭 도메인 관리자로 로그인 합니다. **-HST01** <em> <Fabric Domain> </em>  
  
2.  WSUS를 제거 하도록 승인 된 모든 업데이트를 제거 하려면 명령 프롬프트 창을 열고 다음 명령을 입력 합니다. 자리 표시자 항목 *<  >* 를 적절 한 정보로 바꿉니다.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>다음 단계
자세한 내용은 다음을 참조하세요.
- [Microsoft 업데이트 &#40;분석 플랫폼 시스템&#41;다운로드 및 적용](download-and-apply-microsoft-updates.md) 
- [Analytics platform System 핫픽스 &#40;Analytics platform system&#41;적용](apply-analytics-platform-system-hotfixes.md)  
- [분석 플랫폼 시스템 핫픽스 &#40;분석 플랫폼 시스템을 제거&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [소프트웨어 서비스 &#40;분석 플랫폼 시스템&#41;](software-servicing.md)  
  
