---
title: Microsoft 업데이트 다운로드
description: 이 항목에서는 Microsoft 업데이트 카탈로그에서 Windows Server Update Services (WSUS)로 업데이트를 다운로드 하 고 해당 업데이트를 분석 플랫폼 시스템 어플라이언스 서버에 적용 하는 방법을 설명 합니다. Microsoft 업데이트은 Windows 및 SQL Server에 대해 적용 가능한 모든 업데이트를 설치 합니다. WSUS는 기기의 VMM 가상 컴퓨터에 설치 됩니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e5f336c3c2c475523d2081bcf01189e67b77fe19
ms.sourcegitcommit: ce15cbbcb0d5f820f328262ff5451818e508b480
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2020
ms.locfileid: "94947918"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>분석 플랫폼 시스템용 Microsoft 업데이트 다운로드 및 적용
이 항목에서는 Microsoft 업데이트 카탈로그에서 Windows Server Update Services (WSUS)로 업데이트를 다운로드 하 고 해당 업데이트를 분석 플랫폼 시스템 어플라이언스 서버에 적용 하는 방법을 설명 합니다. Microsoft 업데이트은 Windows 및 SQL Server에 대해 적용 가능한 모든 업데이트를 설치 합니다. WSUS는 기기의 VMM 가상 컴퓨터에 설치 됩니다.  
  
## <a name="before-you-begin"></a><a name="TOP"></a>시작하기 전 주의 사항  
  
> [!WARNING]  
> 어플라이언스 또는 어플라이언스 구성 요소가 다운 되거나 장애 조치 (failover) 된 경우 업데이트를 적용 하지 마십시오. 이 경우 지원 담당자에 게 문의 하세요.  
>   
> 어플라이언스를 사용 하는 동안에는 Microsoft 업데이트를 적용 하지 마십시오. 업데이트를 적용 하면 어플라이언스 노드가 재부팅 될 수 있습니다. 어플라이언스를 사용 하지 않는 경우 유지 관리 기간 동안 업데이트를 적용 해야 합니다.  
  
### <a name="prerequisites"></a>사전 요구 사항  
이러한 단계를 수행 하기 전에 다음을 수행 해야 합니다.  
  
-   [구성 Windows Server Update Services &#40;wsus&#41; &#40;분석 플랫폼 시스템&#41;](configure-windows-server-update-services-wsus.md)의 지침에 따라 어플라이언스에서 wsus를 구성 합니다.  
  
-   패브릭 도메인 관리자 계정 로그인 정보에 대 한 정보입니다.  
  
-   분석 플랫폼 시스템 관리 콘솔에 액세스 하 고 어플라이언스 상태 정보를 볼 수 있는 권한이 있는 로그인이 있어야 합니다.  
  
-   대부분의 경우 WSUS는 어플라이언스 외부의 서버에 액세스 해야 합니다. 이 사용 시나리오를 지원 하기 위해 분석 플랫폼 시스템 DNS는 외부 DNS 서버를 사용 하 여 어플라이언스 외부에서 이름을 확인할 수 있도록 하 Virtual Machines는 외부 이름 전달자를 지원 하도록 구성 될 수 있습니다. 자세한 내용은 [Dns 전달자를 사용 하 여 비 어플라이언스 DNS 이름 확인 &#40;분석 플랫폼 시스템&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)을 참조 하세요.  
  
## <a name="to-download-and-apply-microsoft-updates"></a><a name="bkmk_ImportUpdates"></a>Microsoft 업데이트를 다운로드 하 여 적용 하려면  
  
#### <a name="verify-the-appliance-state-indicators"></a>어플라이언스 상태 표시기를 확인 합니다.  
  
1.  관리 콘솔을 열고 어플라이언스 상태 페이지로 이동 합니다. 자세한 내용은 [관리 콘솔 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 을 참조 하세요&#41;  
  
2.  어플라이언스 상태의 모든 노드에 대 한 상태 표시기를 확인 합니다.  
  
    -   녹색 또는 NA 표시기를 계속 사용 해도 됩니다.  
  
    -   중요 하지 않은 (노란색) 경고 오류를 평가 합니다. 일부 경우에 경고 메시지가 업데이트를 차단 하지 않습니다. C:\에 없는 디스크 볼륨 오류가 발생 한 경우 드라이브, 디스크 볼륨 오류를 확인 하기 전에 다음 단계를 진행할 수 있습니다.  
  
    -   계속 하려면 빨간색 표시기를 가장 먼저 해결 해야 합니다. 디스크 오류가 발생 하는 경우 관리 콘솔 경고 페이지를 사용 하 여 각 서버 또는 SAN 배열 내에 디스크 오류가 둘 이상 없는지 확인 합니다. 각 서버 또는 SAN 배열 내에 디스크 오류가 둘 이상 없는 경우 디스크 오류를 수정 하기 전에 다음 단계를 진행할 수 있습니다. 가능한 한 빨리 디스크 오류를 해결 하려면 Microsoft 지원에 문의 하세요.  
  
#### <a name="synchronize-the-wsus-server"></a>WSUS 서버 동기화  
  
1.  VMM 가상 컴퓨터에 도메인 관리자로 로그온 합니다.  
  
2.  **서버 관리자 대시보드의** **도구** 메뉴에서 **Windows Server Update Services** (**wsus**)를 클릭 합니다.  
  
3.  WSUS 관리 콘솔에서 **동기화** 를 클릭 합니다.  
  
4.  동기화가 실행 되 고 있지 않은 경우 오른쪽 창에서 **지금 동기화** 를 클릭 합니다. 아래쪽 창에 동기화 상태가 나타납니다. 동기화가 완료 될 때까지 기다립니다.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>WSUS에서 Microsoft 업데이트 승인  
  
1. **System Center** 가 아닌 모든 업데이트 롤업을 거부 합니다.

2. WSUS 콘솔의 왼쪽 창에서 **모든 업데이트** 를 클릭 합니다.  
  
3.  **모든 업데이트** 창에서 **승인** 드롭다운 메뉴를 클릭 하 고 **승인** 거부 됨을 **제외** 로 설정 합니다. **상태** 드롭다운 메뉴를 클릭 하 고 **상태** 를 **Any** 로 설정 합니다. **새로 고침** 을 클릭합니다.  
  
    **제목** 열을 마우스 오른쪽 단추로 클릭 하 고 **파일 상태** 를 선택 하 여 다운로드 완료 후 파일 상태를 확인 합니다.  
  
    왼쪽 창에서 **중요 업데이트** 또는 **보안 업데이트** 를 선택 하 고 이러한 범주에 대해 사용 가능한 업데이트를 볼 수도 있습니다.  
  
    ![모든 업데이트를 선택하고 상태를 임의로 변경합니다.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
4.  모든 업데이트를 선택 하 고 오른쪽 창에서 **승인** 링크를 클릭 합니다.  
  
    선택한 업데이트를 마우스 오른쪽 단추로 클릭 하 고 **승인** 을 클릭할 수도 있습니다. "Microsoft 소프트웨어 사용 조건"에 동의 하 라는 메시지가 표시 될 수 있습니다. 이 경우 창에서 **동의** 함을 클릭 하 여 계속 합니다.  
  
    ![적용하는 업데이트를 모두 선택하고 승인을 클릭합니다.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
5.  [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)에서 만든 어플라이언스 서버 그룹을 선택 합니다.  
  
6.  **설치 승인** 을 클릭한 다음 **확인** 을 클릭합니다.  
  
    ![컴퓨터 그룹에 대한 업데이트를 승인합니다.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
7.  **승인 진행률** 대화 상자에서 승인 프로세스가 완료 되 면 **닫기** 를 클릭 합니다.  
  
    ![업데이트가 승인되면 창을 닫습니다.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>업데이트가 WSUS에 있는지 확인  
  
-  모든 업데이트의 파일 상태를 확인 합니다. 각 파일에는 제목 왼쪽에 녹색 화살표 아이콘이 있어야 합니다. 이는 파일을 설치할 준비가 되었음을 나타냅니다.  
  
    ![파일 상태: 성공](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    업데이트를 설치 하기 전에 WSUS 콘솔에서 다운로드 하 여 사용할 수 있는지 확인 합니다.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>모든 업데이트가 다운로드 되었는지 확인 하려면  
  
-  다음 스크린샷에 표시 된 것 처럼 WSUS 콘솔에서 업데이트의 **다운로드 상태** 를 확인 합니다. **파일이 필요한 업데이트** 를 확인 하 여 모든 업데이트가 다운로드 되었는지 확인 합니다. 이 수가 0 보다 많은 경우 돌아가서 추가 업데이트를 승인 해야 할 수 있습니다.  
  
    ![모든 업데이트가 다운로드되었는지 확인합니다.](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Microsoft 업데이트 적용  
  
1.  시작 하기 전에 [관리 콘솔 &#40;분석 플랫폼 시스템&#41;사용 하 여 어플라이언스 모니터](monitor-the-appliance-by-using-the-admin-console.md)를 열고 **어플라이언스 상태** 탭을 클릭 한 다음 **클러스터** 및 **네트워크** 열이 모든 노드에 녹색 (또는 NA)을 표시 하는지 확인 합니다. 이러한 열 중 하나에 경고가 있는 경우 어플라이언스는 업데이트를 제대로 설치 하지 못할 수 있습니다. 계속 하기 전에 **클러스터** 및 **네트워크** 열의 기존 경고를 모두 처리 합니다.  
  
2.  패브릭 도메인 관리자로 _<domain_name>_ **HST01** 노드에 로그온 합니다.  
  
3.  WSUS에 대해 승인 된 모든 업데이트를 적용 하려면 업데이트 프로그램을 실행 합니다. 지침은 아래 [업데이트 프로그램 실행](#RunUpdateWizard) 을 참조 하세요.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>모든 노드에서 업데이트 확인  
  
1.  VMM 노드에서 WSUS 관리 콘솔을 시작 합니다. 이 응용 프로그램은 **시작**, **관리 도구**, **Windows Server Update Services** 에서 찾을 수 있습니다.  
  
2.  **컴퓨터** 를 확장 합니다.  
  
3.  **모든 컴퓨터** 를 확장 합니다.  
  
4.  [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)에서 만든 어플라이언스 서버 그룹을 선택 합니다.  
  
5.  **상태** 드롭다운 메뉴에서 **모두** 를 선택 하 고 **새로 고침** 을 클릭 합니다.  
  
6.  **업데이트 서비스**, *<appliance name>* -VMM, **업데이트**, **모든 업데이트** 를 확장 *<appliance name>* 합니다. 여기서은 어플라이언스 이름입니다.  
  
7.  **모든 업데이트** 창에서 승인 거부 됨을 **제외한 모든** **승인** 으로 설정 합니다.  
  
8.  **모든 업데이트** 창에서 **상태** 를 Failed로 설정 **하거나 필요 함** 으로 설정 합니다.  
  
9. **새로 고침** 을 클릭합니다.  
  
10. **필요한 업데이트가** 0 보다 큰 경우 지원 담당자에 게 문의 하세요.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>SQL Server PDW 관리 콘솔에 중요 한 경고가 없는지 확인  
  
1.  관리 콘솔을 열고 어플라이언스 상태 탭을 클릭 합니다. [관리 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)을 참조 하세요.  
  
2.  **클러스터** 및 **네트워크** 열이 모든 노드에 녹색 또는 NA를 표시 하는지 확인 합니다. 이러한 열 중 하나에 경고가 있는 경우 어플라이언스는 업데이트를 제대로 설치 하지 못할 수 있습니다. 중요 한 알림이 있는 경우 지원 담당자에 게 문의 하세요.  
  
## <a name="run-the-update-program"></a><a name="RunUpdateWizard"></a>업데이트 프로그램 실행  
분석 플랫폼 시스템 업데이트 프로그램을 실행 하려면 다음 지침을 따르세요.  
  
> [!NOTE]  
> WSUS 시스템은 비동기적으로 실행 되도록 설계 되었으므로 모든 업데이트를 완전히 적용 하는 데 다소 시간이 걸릴 수 있습니다. 업데이트를 시작 하면 업데이트가 예약 되지만 즉시 업데이트 작업은 보장 되지 않습니다.  
  
1.  HST01 노드에 패브릭 도메인 관리자로 로그인 되어 있는지 확인 합니다.  
  
2.  명령 프롬프트 창을 열고 다음 명령을 입력 합니다. *<parameter>* 지정 된 정보로 대체 합니다.  
  
**Microsoft 업데이트를 실행 하려면 다음을 수행 합니다.**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Microsoft 업데이트 상태를 보고 하려면:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>참고 항목  
[Microsoft 업데이트 &#40;분석 플랫폼 시스템을 제거&#41;](uninstall-microsoft-updates.md)  
[Analytics platform System 핫픽스 &#40;Analytics platform system&#41;적용 ](apply-analytics-platform-system-hotfixes.md)  
[분석 플랫폼 시스템 핫픽스 &#40;분석 플랫폼 시스템을 제거&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[소프트웨어 서비스 &#40;분석 플랫폼 시스템&#41;](software-servicing.md)  
  
