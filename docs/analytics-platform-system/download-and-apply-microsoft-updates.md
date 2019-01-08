---
title: Microsoft 업데이트-Analytics Platform System 다운로드 | Microsoft Docs
description: 이 항목에서는 Server Update Services (WSUS (Windows)는 Microsoft 업데이트 카탈로그에서 업데이트를 다운로드 및 분석 플랫폼 시스템 어플라이언스 서버 해당 업데이트를 적용 하는 방법을 설명 합니다. Microsoft Update는 Windows 및 SQL Server에 대 한 모든 적용 가능한 업데이트를 설치 됩니다. WSUS는 어플라이언스의 VMM 가상 컴퓨터에 설치 됩니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d71a6ddc965b422f0f96f40788352213501b4db2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521483"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>다운로드 및 Analytics Platform System에 대 한 Microsoft 업데이트를 적용 합니다.
이 항목에서는 Server Update Services (WSUS (Windows)는 Microsoft 업데이트 카탈로그에서 업데이트를 다운로드 및 분석 플랫폼 시스템 어플라이언스 서버 해당 업데이트를 적용 하는 방법을 설명 합니다. Microsoft Update는 Windows 및 SQL Server에 대 한 모든 적용 가능한 업데이트를 설치 됩니다. WSUS는 어플라이언스의 VMM 가상 컴퓨터에 설치 됩니다.  
  
## <a name="TOP"></a>시작하기 전 주의 사항  
  
> [!WARNING]  
> 어플라이언스 또는 어플라이언스 구성 요소가 중단 또는 실패 한 경우 업데이트를 적용 하지 마십시오 상태 위로 합니다. 이 경우 지원에 문의 합니다.  
>   
> 어플라이언스를 사용 중일 때에 Microsoft 업데이트를 적용 되지 않습니다. 업데이트 적용 어플라이언스 노드를 다시 부팅 될 수 있습니다. 어플라이언스를 사용 하는 경우 업데이트를 유지 관리 기간 적용 되어야 합니다.  
  
### <a name="prerequisites"></a>사전 요구 사항  
다음이 단계를 수행 하기 전에 해야 합니다.  
  
-   어플라이언스의 지침을 수행 하 여 WSUS를 구성 [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)합니다.  
  
-   패브릭 도메인 관리자 계정 로그인 정보를 알고 있어야 합니다.  
  
-   분석 플랫폼 시스템 관리자 콘솔에 액세스 하 고 어플라이언스 상태 정보를 볼 수 있는 권한이 있는 로그인이 있어야 합니다.  
  
-   대부분의 경우, WSUS 서버는 어플라이언스 외부에서 액세스 해야 합니다. 외부 DNS 분석 플랫폼 시스템 Analytics Platform System 호스트 및 Virtual Machines (Vm) 외부 DNS 서버 이름을 확인 하기 위해 사용할 수 있는 외부 이름이 전달자를 지원 하도록 구성할 수 있습니다이 사용 시나리오를 지원 하도록 합니다 어플라이언스입니다. 자세한 내용은 [비 어플라이언스 DNS 이름 확인에 DNS 전달자를 사용 하 여 &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)합니다.  
  
## <a name="bkmk_ImportUpdates"></a>다운로드 하 여 Microsoft 업데이트 적용  
  
#### <a name="verify-the-appliance-state-indicators"></a>어플라이언스 상태 표시기를 확인 합니다.  
  
1.  관리 콘솔을 열고 어플라이언스 상태 페이지로 이동 합니다. 자세한 내용은 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  어플라이언스 상태에서 모든 노드에 대 한 상태 표시기를 확인 합니다.  
  
    -   녹색 또는 NA 표시기를 사용 하 여 계속 안전 합니다.  
  
    -   (노란색) 중요 하지 않은 경고 오류를 평가 합니다. 일부 경우에서 경고 메시지는 업데이트를 차단 하지 않습니다. C:\ 드라이브에 있지 않은 중요 하지 않은 디스크 볼륨 오류가 있으면 디스크 볼륨 오류를 해결 하기 전에 다음 단계를 진행할 수 있습니다.  
  
    -   대부분의 빨간색 표시기를 계속 하기 전에 확인 되어야 합니다. 디스크 실패의 경우에 각 서버 또는 SAN 배열 내에서 둘 이상의 디스크 오류가 있는지 확인 하려면 관리 콘솔 경고 페이지를 사용 합니다. 각 서버 또는 SAN 배열 내에서 둘 이상의 디스크 오류 이면 디스크 오류를 수정 하기 전에 다음 단계를 진행할 수 있습니다. 가능한 한 빨리 디스크 오류를 해결 하려면 Microsoft 지원에 문의 해야 합니다.  
  
#### <a name="synchronize-the-wsus-server"></a>WSUS 서버 동기화  
  
1.  VMM 가상 컴퓨터에 도메인 관리자로 로그온 합니다.  
  
2.  에 **서버 관리자 대시보드**에 **도구** 메뉴에서 클릭 **Windows Server Update Services** (**wsus.msc**).  
  
3.  WSUS 관리 콘솔에서 클릭 **동기화**합니다.  
  
4.  동기화를 실행 하지 않는 경우 클릭 **지금 동기화** 오른쪽 창에서. 아래쪽 창에서 동기화 상태 수 됩니다. 동기화가 완료 될 때까지 기다립니다.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>WSUS에서 Microsoft 업데이트를 승인 합니다.  
  
1.  WSUS 콘솔의 왼쪽된 창에서 클릭 **모든 업데이트**합니다.  
  
2.  에 **모든 업데이트** 창 클릭 합니다 **승인** 드롭 다운 메뉴에서 **승인** 에 **거부를 제외한 모든**합니다. 클릭 합니다 **상태** 드롭 다운 메뉴에서 **상태** 하 **모든**합니다. **새로 고침**을 클릭합니다.  
  
    마우스 오른쪽 단추로 클릭 합니다 **제목** 열을 선택 **파일 상태** 다운로드가 완료 된 후 파일 상태를 확인 합니다.  
  
    선택할 수도 있습니다 **중요 업데이트** 하거나 **보안 업데이트** 이러한 범주에 대 한 왼쪽 창과 뷰 사용 가능한 업데이트 합니다.  
  
    ![모든 업데이트를 선택 하 고 상태를 임의로 변경 합니다. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  모든 업데이트를 선택 하 고 클릭 합니다 **승인** 오른쪽 창에서 링크 합니다.  
  
    또한 선택한 업데이트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **승인**합니다. "Microsoft 소프트웨어 라이선스 사용 조건에 동의" 라는 메시지가 표시 될 수 있습니다. 그렇다면, 클릭 **동의** 계속 하려면 창의 합니다.  
  
    ![모든 업데이트를 적용 하 고 승인을 클릭을 선택 합니다. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  만든 어플라이언스 서버 그룹을 선택 [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)합니다.  
  
5.  클릭 **설치 승인**를 클릭 하 고 **확인**합니다.  
  
    ![컴퓨터 그룹에 대 한 업데이트를 승인 합니다. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  에 **승인 진행률** 대화 상자에서 승인 프로세스가 완료 되 면 클릭 **닫기**합니다.  
  
    ![업데이트가 승인 되 면 창을 닫습니다. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>WSUS에서 업데이트 되는지 확인  
  
-  모든 업데이트의 파일 상태를 확인 합니다. 각 파일의 제목 왼쪽에 녹색 화살표 아이콘을가지고 있어야 합니다. 이 파일은 설치에 대 한 준비를 나타냅니다.  
  
    ![파일 상태: 성공](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    업데이트를 설치 하기 전에 모든 다운로드 및 WSUS 콘솔에서 사용할 수 있는지를 확인 합니다.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>모든 업데이트가 다운로드 되었는지 확인 하려면  
  
-  확인 합니다 **다운로드 상태** 다음 스크린샷에 표시 된 대로 WSUS 콘솔에서 업데이트 합니다. 확인 **파일이 필요한 업데이트** 0 이면 모든 업데이트가 다운로드 되었는지 확인 하 고 있습니다. 이 값이 0 보다, 뒤로 돌아가서 추가 업데이트를 승인 해야 합니다.  
  
    ![모든 업데이트가 다운로드 되었는지 확인 합니다. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Microsoft 업데이트 적용  
  
1.  시작 하기 전에 열를 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md), 클릭는 **어플라이언스 상태** 탭을 확인 합니다  **클러스터** 하 고 **네트워크** 모든 노드에 대 한 열 표시 녹색 (또는 NA). 모든 경고에 있는 경우 이러한 열 중 어플라이언스 업데이트를 제대로 설치 하지 못할 수 있습니다. 모든 기존 경고를 해결 합니다 **클러스터** 하 고 **네트워크** 계속 하기 전에 열.  
  
2.  에 로그온 합니다 _< 도메인 _ 이름 >_**-HST01** 노드 Fabric 도메인 관리자입니다.  
  
3.  WSUS에 대 한 승인 된 모든 업데이트를 적용 하려면 업데이트 프로그램을 실행 합니다. 참조 [업데이트 프로그램 실행](#RunUpdateWizard) 아래 지침에 대 한 합니다.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>모든 노드에서 업데이트를 확인 합니다.  
  
1.  VMM 노드에서 WSUS 관리 콘솔을 시작 합니다. 이 응용 프로그램을 찾을 수 있습니다 **시작**, **관리 도구**하십시오 **Windows Server Update Services**합니다.  
  
2.  확장 **컴퓨터**합니다.  
  
3.  확장 **모든 컴퓨터**합니다.  
  
4.  만든 어플라이언스 서버 그룹을 선택 [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)합니다.  
  
5.  에 **상태** 드롭 다운 메뉴에서 **모든** 클릭 **새로 고침**합니다.  
  
6.  확장 **서비스 업데이트**를 *<appliance name>*-VMM **업데이트**를 **업데이트를 모두**여기서 *<appliance name>* 은 어플라이언스 이름입니다.  
  
7.  에 **모든 업데이트** 창 집합 **승인** 하 **거부를 제외한 모든**합니다.  
  
8.  에 **모든 업데이트** 창에서 **상태** 에 **실패 했거나 필요한**합니다.  
  
9. **새로 고침**을 클릭합니다.  
  
10. 하는 경우 **필요한 업데이트** 지원에 대 한 연락처 지원 0 보다 큽니다.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>SQL Server PDW 관리 콘솔에서 중요 한 알림이 있는지 확인  
  
1.  관리자 콘솔을 열고 어플라이언스 상태 탭을 클릭 합니다. 참조 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)합니다.  
  
2.  있는지 확인 합니다 **클러스터** 하 고 **네트워크** 모든 노드에 대 한 열 표시 녹색 (또는 NA). 모든 경고에 있는 경우 이러한 열 중 어플라이언스 업데이트를 제대로 설치 하지 못할 수 있습니다. 모든 중요 한 경고가 지원에 문의 합니다.  
  
## <a name="RunUpdateWizard"></a>업데이트 프로그램 실행  
분석 플랫폼 시스템 업데이트 프로그램을 실행 하려면 다음이 지침을 따릅니다.  
  
> [!NOTE]  
> WSUS 시스템은 실행 비동기적으로 시간이 조금 걸립니다 완벽 하 게 모든 업데이트를 적용 합니다. 업데이트를 시작 합니다. 업데이트 예약 하지만 즉시 업데이트 활동을 보장 하지 않습니다.  
  
1.  HST01 노드 Fabric 도메인 관리자에 로그인 되어 있는지 확인 합니다.  
  
2.  명령 프롬프트 창을 열고 다음 명령을 입력 합니다. 바꿉니다 *<parameter>* 지정된 정보를 사용 하 여 합니다.  
  
**Microsoft 업데이트를 실행 합니다.**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Microsoft 업데이트 상태를 보고 합니다.**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>관련 항목:  
[Microsoft 업데이트를 제거할 &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Analytics Platform System 핫픽스 적용 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Analytics Platform System 핫픽스 제거 &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[소프트웨어 설치 &#40;Analytics Platform System&#41;](software-servicing.md)  
  
