---
title: Analytics Platform System 핫픽스 제거 | Microsoft Docs
description: Analytics Platform System 핫픽스를 제거 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d7135972201fe8cce8a43cbd3c8fe547ce40248e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959900"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Analytics Platform System 핫픽스 제거 
다음 단계를 이전에 설치 된 Analytics Platform System 핫픽스 제거 하는 방법에 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
### <a name="prerequisites"></a>사전 요구 사항  
이러한 단계를 수행 하려면 해야 합니다.  
  
-   어플라이언스를 모니터링 하려면 관리자 콘솔에 액세스할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인을 합니다.  
  
-   도메인 관리자 계정에 로그인 하는 <em>< appliance_domain ></em> **-HST01** 노드.  
  
-   기술 자료 문서 번호를 핫픽스를 제거 합니다.  
  
## <a name="HowToUninstallPDW"></a>SQL Server PDW 핫픽스를 제거 하려면  
  
1.  에 로그온 합니다 <em>< appliance_domain ></em> **-HST01** 노드 Fabric 도메인 관리자입니다.  
  
2.  As Administrator 옵션 실행 사용 하 여 명령 프롬프트를 엽니다.  
  
3.  디렉터리를 변경 `C:\PDWINST\Patches\<kbarticle>\media` 여기서 *<kbarticle>* 기술 자료 문서 번호를 핫픽스 제거 됩니다.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  핫픽스를 제거 하려면 다음 명령을 실행 합니다.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>관련 항목  
[Microsoft 업데이트 다운로드 및 적용 &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Microsoft 업데이트를 제거할 &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Analytics Platform System 핫픽스 적용 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[소프트웨어 설치 &#40;Analytics Platform System&#41;](software-servicing.md)  
  
