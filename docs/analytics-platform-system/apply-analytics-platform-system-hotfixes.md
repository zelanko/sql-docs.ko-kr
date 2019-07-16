---
title: Analytics Platform System 핫픽스 적용 | Microsoft Docs
description: 이 문서는 분석 플랫폼 시스템 소프트웨어에 핫픽스를 적용 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d6af4a1eaf1e9891356fae40a3d3bb7f11e41dc6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961423"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Analytics Platform System 핫픽스 적용
이 문서는 분석 플랫폼 시스템 소프트웨어에 핫픽스를 적용 하는 방법을 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
> [!WARNING]  
> 어플라이언스 또는 어플라이언스 구성 요소가 중단 또는 실패 한 경우 Analytics Platform System 핫픽스를 적용 하지 마십시오 상태 위로 합니다. 이 경우 지원에 문의 합니다.  
  
> [!WARNING]  
> Analytics Platform System 핫픽스 어플라이언스를 사용 중일 때에 적용 되지 않습니다. 핫픽스를 적용 하면 어플라이언스 노드를 다시 부팅 될 수 있습니다. 어플라이언스를 사용 하는 경우 유지 관리 기간 동안 핫픽스를 적용 되어야 합니다.  
  
### <a name="prerequisites"></a>사전 요구 사항  
이러한 단계를 수행 하려면 해야 합니다.  
  
-   액세스 관리 콘솔 어플라이언스 상태를 모니터링할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인을 합니다. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   연결할 패브릭 도메인 관리자 계정에 대 한 지식이 합니다 _< 도메인 _ 이름 >_ **-HST01** 노드.  
  
## <a name="HowToInstallPDW"></a>Analytics Platform System 핫픽스 적용  
Microsoft 업데이트와는 달리 핫픽스는 분석 플랫폼 시스템 소프트웨어에 대 한 WSUS를 통해 처리 되지 않습니다. 다른 워크플로가 않으며 핫픽스 패키지를 실행 하 여 설치 됩니다.  
  
1.  **어플라이언스 상태 표시기를 확인 합니다.**  
  
    1.  관리 콘솔을 열고 어플라이언스 상태 페이지로 이동 합니다. 자세한 내용은 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  다음 단계를 계속 진행 하기 전에 모든 빨간색 또는 노란색 표시기를 확인 해야 합니다. 몇 가지 예외입니다.  
  
        -   디스크 실패의 경우에 각 서버 또는 SAN 배열 내에서 둘 이상의 디스크 오류가 있는지 확인 하려면 관리 콘솔 경고 페이지를 사용 합니다. 각 서버 또는 SAN 배열 내에서 둘 이상의 디스크 오류 이면 디스크 오류를 수정 하기 전에 다음 단계를 진행할 수 있습니다. 가능한 한 빨리 디스크 오류를 해결 하려면 Microsoft 지원에 문의 해야 합니다.  
  
        -   C:\ 드라이브에 있지 않은 중요 하지 않은 (노란색) 디스크 볼륨 오류가 있으면 디스크 볼륨 오류를 해결 하기 전에 다음 단계를 진행할 수 있습니다.  
  
2.  **Analytics Platform System 핫픽스를 설치 합니다.**  
  
    1.  로그인 하는 <*appliance_domain*>-도메인 관리자로 HST01 노드.  
  
    2.  사용 된 **관리자 권한으로 실행** 옵션을 명령 프롬프트를 엽니다.  
  
    3.  다음 명령을 실행 교체 *<HotfixPackageName>* 다른 자리 표시자 항목 바꾸고 핫픽스 실행 패키지 이름의 *< >* 적절 한 정보를 사용 하 여 합니다.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  핫픽스 패키지에 의해 제시 된 단계를 따릅니다.  
  
## <a name="see-also"></a>관련 항목  
[Microsoft 업데이트 다운로드 및 적용 &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Microsoft 업데이트를 제거할 &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Analytics Platform System 핫픽스 제거 &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[소프트웨어 설치 &#40;Analytics Platform System&#41;](software-servicing.md)  
  
