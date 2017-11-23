---
title: "Microsoft 업데이트 (분석 플랫폼 시스템)를 제거 합니다."
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df61570a-210d-4154-822f-98acd721f075
caps.latest.revision: "19"
ms.openlocfilehash: c801918cbac5d0762384a0cd3adcca9ddf8f346a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="uninstall-microsoft-updates"></a>업데이트 제거
이 항목에서는 분석 플랫폼 시스템 기기에서 이전에 설치 된 Microsoft 업데이트를 제거 하는 방법에 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>필수 구성 요소  
다음이 단계를 수행 하려면 다음이 필요 합니다.  
  
-   어플라이언스를 모니터링 하는 관리 콘솔에 액세스할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인입니다.  
  
-   패브릭 도메인 관리자 계정에 로그인 하려면 기술 자료는  *<Fabric Domain>*  **-HST01** 노드.  
  
## <a name="HowToUninstallMSFT"></a>Microsoft 업데이트를 제거 하려면  
  
1.  로그인에는  *<Fabric Domain>*  **-HST01** 패브릭 도메인 관리자로 노드.  
  
2.  제거 하는 WSUS에 대 한 승인 된 모든 업데이트를 제거 하려면 명령 프롬프트 창을 열고 다음 명령을 입력 합니다. 자리 표시자 항목으로 대체 *< >* 적절 한 정보를 사용 합니다.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="see-also"></a>관련 항목:  
[다운로드 하 여 Microsoft 업데이트 &#40; 적용 분석 플랫폼 시스템 &#41;](download-and-apply-microsoft-updates.md)  
[분석 플랫폼 시스템 핫픽스 &#40; 적용 분석 플랫폼 시스템 &#41;](apply-analytics-platform-system-hotfixes.md)  
[분석 플랫폼 시스템 핫픽스 &#40; 제거 분석 플랫폼 시스템 &#41;](uninstall-analytics-platform-system-hotfixes.md)  
[소프트웨어 설치 &#40; 분석 플랫폼 시스템 &#41;](software-servicing.md)  
  
