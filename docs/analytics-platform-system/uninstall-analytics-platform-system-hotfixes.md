---
title: 분석 플랫폼 시스템에는 핫픽스를 제거 합니다. | Microsoft Docs
description: 분석 플랫폼 시스템 핫픽스를 제거 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 83e57a676ee0eff21eb3a736484d8e286cdeee01
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538783"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>분석 플랫폼 시스템 핫픽스를 제거 합니다. 
다음 단계에서는 이전에 설치한 분석 플랫폼 시스템 핫픽스를 제거 하는 방법에 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>필수 구성 요소  
다음이 단계를 수행 하려면 다음이 필요 합니다.  
  
-   어플라이언스를 모니터링 하는 관리 콘솔에 액세스할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인입니다.  
  
-   도메인 관리자 계정에 로그인 하 고 *< appliance_domain > * * *-HST01** 노드.  
  
-   기술 자료 문서 번호 핫픽스를 제거 합니다.  
  
## <a name="HowToUninstallPDW"></a>SQL Server PDW 핫픽스를 제거 하려면  
  
1.  로그온 하는 *< appliance_domain > * * *-HST01** 패브릭 도메인 관리자로 노드.  
  
2.  명령 프롬프트를 열려면 관리자 옵션으로 실행을 사용 합니다.  
  
3.  디렉터리 `C:\PDWINST\Patches\<kbarticle>\media` 여기서 *<kbarticle>* 핫픽스를 제거 하려면 기술 자료 문서입니다.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  핫픽스를 제거 하려면 다음 명령을 실행 합니다.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>관련 항목:  
[다운로드 하 여 Microsoft 업데이트 적용 &#40;분석 플랫폼 시스템&#41;](download-and-apply-microsoft-updates.md)  
[업데이트 제거 &#40;분석 플랫폼 시스템&#41;](uninstall-microsoft-updates.md)  
[분석 플랫폼 시스템 핫픽스를 적용 &#40;분석 플랫폼 시스템&#41;](apply-analytics-platform-system-hotfixes.md)  
[소프트웨어 서비스 &#40;분석 플랫폼 시스템&#41;](software-servicing.md)  
  
