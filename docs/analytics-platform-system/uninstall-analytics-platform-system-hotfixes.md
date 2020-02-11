---
title: 핫픽스 제거
description: 분석 플랫폼 시스템 핫픽스를 제거 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef6929aeb06c9472eb3ff210de016117a9636ded
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399760"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>분석 플랫폼 시스템 핫픽스 제거 
다음 단계에서는 이전에 설치 된 분석 플랫폼 시스템 핫픽스를 제거 하는 방법을 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>사전 요구 사항  
이러한 단계를 수행 하려면 다음이 필요 합니다.  
  
-   어플라이언스를 모니터링 하기 위해 관리 콘솔에 액세스할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인입니다.  
  
-   <em><appliance_domain></em> **HST01** 노드에 로그인 할 도메인 관리자 계정입니다.  
  
-   제거할 핫픽스에 대 한 기술 자료 문서 번호입니다.  
  
## <a name="HowToUninstallPDW"></a>SQL Server PDW 핫픽스를 제거 하려면  
  
1.  패브릭 도메인 관리자로 <em><appliance_domain></em> **HST01** 노드에 로그온 합니다.  
  
2.  관리자 권한으로 실행 옵션을 사용 하 여 명령 프롬프트를 엽니다.  
  
3.  디렉터리를로 `C:\PDWINST\Patches\<kbarticle>\media` 변경 *<kbarticle>* 합니다. 여기서는 핫픽스를 제거할 기술 자료 문서 번호입니다.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  핫픽스를 제거 하려면 다음 명령을 실행 합니다.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>참고 항목  
[Microsoft 업데이트 &#40;분석 플랫폼 시스템&#41;다운로드 및 적용](download-and-apply-microsoft-updates.md)  
[Microsoft 업데이트 &#40;분석 플랫폼 시스템을 제거&#41;](uninstall-microsoft-updates.md)  
[Analytics platform System 핫픽스 &#40;Analytics platform system&#41;적용](apply-analytics-platform-system-hotfixes.md)  
[소프트웨어 서비스 &#40;분석 플랫폼 시스템&#41;](software-servicing.md)  
  
