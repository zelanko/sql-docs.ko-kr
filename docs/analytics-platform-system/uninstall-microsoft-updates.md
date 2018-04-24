---
title: 업데이트-분석 플랫폼 시스템 제거 | "Microsoft Docs
description: Analytics Platform System (APS)의 업데이트를 제거 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57d0eb3616cf3567f63d75029f79cea6709ed955
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 업데이트 제거
이 문서에서는 분석 플랫폼 시스템 기기에서 이전에 설치 된 Microsoft 업데이트를 제거 하는 방법을 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>필수 구성 요소  
다음이 단계를 수행 하려면 다음이 필요 합니다.  
  
-   어플라이언스를 모니터링 하는 관리 콘솔에 액세스할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인입니다.  
  
-   패브릭 도메인 관리자 계정에 로그인 하려면 기술 자료는  *<Fabric Domain>* * *-HST01** 노드.  
  
## <a name="HowToUninstallMSFT"></a>Microsoft 업데이트를 제거 하려면  
  
1.  에 로그인 하 고  *<Fabric Domain>* * *-HST01** 패브릭 도메인 관리자로 노드.  
  
2.  제거 하는 WSUS에 대 한 승인 된 모든 업데이트를 제거 하려면 명령 프롬프트 창을 열고 다음 명령을 입력 합니다. 자리 표시자 항목으로 대체 *< >* 적절 한 정보를 사용 합니다.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>다음 단계
참조 항목:
- [다운로드 하 여 Microsoft 업데이트 적용 &#40;분석 플랫폼 시스템&#41;](download-and-apply-microsoft-updates.md) 
- [분석 플랫폼 시스템 핫픽스를 적용 &#40;분석 플랫폼 시스템&#41;](apply-analytics-platform-system-hotfixes.md)  
- [분석 플랫폼 시스템 핫픽스 제거 &#40;분석 플랫폼 시스템&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [소프트웨어 서비스 &#40;분석 플랫폼 시스템&#41;](software-servicing.md)  
  
