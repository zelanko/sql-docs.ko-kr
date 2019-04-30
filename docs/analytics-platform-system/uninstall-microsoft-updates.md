---
title: Microsoft 업데이트-Analytics Platform System 제거 | Microsoft Docs "
description: Microsoft Analytics Platform System (APS)에서 업데이트를 제거 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4739d05b1878c8b7fc9f66f2e0b8145ff1044e54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63243832"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Analytics Platform System의 Microsoft 업데이트를 제거 합니다.
이 문서에서는 Analytics Platform System appliance에서 이전에 설치 된 Microsoft 업데이트를 제거 하는 방법을 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
### <a name="prerequisites"></a>사전 요구 사항  
이러한 단계를 수행 하려면 해야 합니다.  
  
-   어플라이언스를 모니터링 하려면 관리자 콘솔에 액세스할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인을 합니다.  
  
-   에 로그인 하기 위해 패브릭 도메인 관리자 계정에 대 한 지식이 합니다 <em> <Fabric Domain> </em> **-HST01** 노드.  
  
## <a name="HowToUninstallMSFT"></a>Microsoft 업데이트를 제거 하려면  
  
1.  에 로그인 합니다 <em> <Fabric Domain> </em> **-HST01** 노드 Fabric 도메인 관리자입니다.  
  
2.  제거 하는 WSUS에 대 한 승인 된 모든 업데이트를 제거 하려면 명령 프롬프트 창을 열고 다음 명령을 입력 합니다. 자리 표시자 항목을 바꿉니다 *< >* 적절 한 정보를 사용 하 여 합니다.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>다음 단계
참조 항목:
- [Microsoft 업데이트 다운로드 및 적용 &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 
- [Analytics Platform System 핫픽스 적용 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Analytics Platform System 핫픽스 제거 &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [소프트웨어 설치 &#40;Analytics Platform System&#41;](software-servicing.md)  
  
