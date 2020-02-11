---
title: Analytics Platform System 핫픽스 적용
description: 이 문서에서는 분석 플랫폼 시스템 소프트웨어에 핫픽스를 적용 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd62413ec8542aba9f3973d0e8483cb9c5c9128a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401372"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Analytics Platform System 핫픽스 적용
이 문서에서는 분석 플랫폼 시스템 소프트웨어에 핫픽스를 적용 하는 방법을 설명 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
> [!WARNING]  
> 어플라이언스 또는 어플라이언스 구성 요소가 다운 되거나 장애 조치 (failover) 된 경우에는 분석 플랫폼 시스템 핫픽스를 적용 하지 마십시오. 이 경우 지원 담당자에 게 문의 하세요.  
  
> [!WARNING]  
> 어플라이언스를 사용 하는 동안에는 분석 플랫폼 시스템 핫픽스를 적용 하지 마십시오. 핫픽스를 적용 하면 어플라이언스 노드가 재부팅 될 수 있습니다. 어플라이언스를 사용 하지 않는 경우 유지 관리 기간 중에 핫픽스를 적용 해야 합니다.  
  
### <a name="prerequisites"></a>사전 요구 사항  
이러한 단계를 수행 하려면 다음이 필요 합니다.  
  
-   관리 콘솔에 액세스 하 여 어플라이언스 상태를 모니터링할 수 있는 권한이 있는 분석 플랫폼 시스템 로그인입니다. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   _<domain_name>_ **HST01** 노드에 연결 하는 패브릭 도메인 관리자 계정에 대 한 정보입니다.  
  
## <a name="HowToInstallPDW"></a>분석 플랫폼 시스템 핫픽스를 적용 하려면  
Microsoft 업데이트와 달리 분석 플랫폼 시스템 소프트웨어에 대 한 핫픽스는 WSUS를 통해 처리 되지 않습니다. 다른 워크플로를 가지 며 핫픽스 패키지를 실행 하 여 설치 됩니다.  
  
1.  **어플라이언스 상태 표시기를 확인 합니다.**  
  
    1.  관리 콘솔을 열고 어플라이언스 상태 페이지로 이동 합니다. 자세한 내용은 [관리 콘솔 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 을 참조 하세요&#41;  
  
    2.  다음 단계를 진행 하기 전에 빨간색 또는 노란색 표시기를 모두 해결 해야 합니다. 이에 대 한 몇 가지 예외는 다음과 같습니다.  
  
        -   디스크 오류가 발생 하는 경우 관리 콘솔 경고 페이지를 사용 하 여 각 서버 또는 SAN 배열 내에 디스크 오류가 둘 이상 없는지 확인 합니다. 각 서버 또는 SAN 배열 내에 디스크 오류가 둘 이상 없는 경우 디스크 오류를 수정 하기 전에 다음 단계를 진행할 수 있습니다. 가능한 한 빨리 디스크 오류를 해결 하려면 Microsoft 지원에 문의 하세요.  
  
        -   C:\에 없는 (노란색) 디스크 볼륨 오류가 발생 한 경우 드라이브, 디스크 볼륨 오류를 확인 하기 전에 다음 단계를 진행할 수 있습니다.  
  
2.  **분석 플랫폼 시스템 핫픽스 설치**  
  
    1.  <*appliance_domain*>-HST01 노드에 도메인 관리자로 로그인 합니다.  
  
    2.  **관리자 권한으로 실행** 옵션을 사용 하 여 명령 프롬프트를 엽니다.  
  
    3.  다음 명령을 실행 하 여를 *<HotfixPackageName>* 핫픽스 실행 파일 패키지의 이름으로 바꾸고 다른 자리 표시자 항목 *<  >* 를 적절 한 정보로 바꿉니다.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  핫픽스 패키지에 표시 되는 단계를 따릅니다.  
  
## <a name="see-also"></a>참고 항목  
[Microsoft 업데이트 &#40;분석 플랫폼 시스템&#41;다운로드 및 적용](download-and-apply-microsoft-updates.md)  
[Microsoft 업데이트 &#40;분석 플랫폼 시스템을 제거&#41;](uninstall-microsoft-updates.md)  
[분석 플랫폼 시스템 핫픽스 &#40;분석 플랫폼 시스템을 제거&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[소프트웨어 서비스 &#40;분석 플랫폼 시스템&#41;](software-servicing.md)  
  
