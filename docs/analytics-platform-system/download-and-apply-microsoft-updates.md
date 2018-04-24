---
title: Microsoft 업데이트-분석 플랫폼 시스템 다운로드 | Microsoft Docs
description: 이 항목에서는 Windows Server Update Services (WSUS)를 Microsoft Update 카탈로그에서 업데이트를 다운로드 하 고 분석 플랫폼 시스템 기기 서버 해당 업데이트를 적용 하는 방법에 설명 합니다. Microsoft 업데이트를 통해 Windows 및 SQL Server에 대 한 모든 적용 가능한 업데이트를 설치 합니다. WSUS는 어플라이언스의 VMM 가상 컴퓨터에 설치 됩니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b98a2be90f222fc2c531c1f1983f8882bdab640e
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>다운로드 하 여 분석 플랫폼 시스템에 대 한 Microsoft 업데이트 적용
이 항목에서는 Windows Server Update Services (WSUS)를 Microsoft Update 카탈로그에서 업데이트를 다운로드 하 고 분석 플랫폼 시스템 기기 서버 해당 업데이트를 적용 하는 방법에 설명 합니다. Microsoft 업데이트를 통해 Windows 및 SQL Server에 대 한 모든 적용 가능한 업데이트를 설치 합니다. WSUS는 어플라이언스의 VMM 가상 컴퓨터에 설치 됩니다.  
  
## <a name="TOP"></a>시작하기 전 주의 사항  
  
> [!WARNING]  
> 어플라이언스 또는 어플라이언스 구성 요소가 다운 되었거나 장애 경우 업데이트를 적용 하려고 하지 마십시오 상태 위로 합니다. 이 경우 지원 담당자에 문의 합니다.  
>   
> 어플라이언스에 사용 중인 동안에 Microsoft 업데이트를 적용 하지 마십시오. 업데이트를 적용 하면 어플라이언스 노드를 다시 부팅 될 수 있습니다. 어플라이언스를 사용 하는 경우 유지 관리 기간 동안 업데이트를 적용 되어야 합니다.  
  
### <a name="prerequisites"></a>필수 구성 요소  
다음이 단계를 수행 하기 전에 해야 합니다.  
  
-   지침에 따라 WSUS 어플라이언스 구성 [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;분석 플랫폼 시스템&#41;](configure-windows-server-update-services-wsus.md)합니다.  
  
-   패브릭 도메인 관리자 계정 로그인 정보를 알고 있어야 합니다.  
  
-   분석 플랫폼 시스템 관리 콘솔에 액세스 하 고 어플라이언스 상태 정보를 볼 수 있는 권한이 있는 로그인이 있어야 합니다.  
  
-   대부분의 경우에서 WSUS 어플라이언스에 외부 서버에 액세스 해야 합니다. 분석 플랫폼 시스템 DNS 외부의 분석 플랫폼 시스템 호스트 및 가상 컴퓨터 (Vm) 이름을 확인 하기 위해 외부 DNS 서버를 사용할 수 있는 외부 이름 전달자를 지원 하도록 구성할 수 있습니다이 사용 시나리오를 지원 하기 위해는 구성할 수 있습니다. 자세한 내용은 참조 [비 어플라이언스 DNS 이름 확인에 DNS 전달자를 사용 하 여 &#40;분석 플랫폼 시스템&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)합니다.  
  
## <a name="bkmk_ImportUpdates"></a>다운로드 하 여 Microsoft 업데이트 적용  
  
#### <a name="verify-the-appliance-state-indicators"></a>어플라이언스 상태 표시기를 확인 합니다.  
  
1.  관리 콘솔을 열고 기기 상태 페이지로 이동 합니다. 자세한 내용은 참조 [관리 콘솔을 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  어플라이언스 상태에서 모든 노드에 대 한 상태 표시기를 확인 합니다.  
  
    -   녹색 또는 NA 지표를 계속 해도 됩니다.  
  
    -   (노란색) 중요 하지 않은 경고 오류를 평가 합니다. 일부 경우에 경고 메시지는 업데이트를 차단 하지 않습니다. C:\ 드라이브에 있지 않은 중요 하지 않은 디스크 볼륨 오류 이면 디스크 볼륨 오류를 해결 하기 전에 다음 단계를 진행할 수 있습니다.  
  
    -   대부분 빨간색 표시기 계속 하기 전에 해결 해야 합니다. 디스크 오류가 발생 하는, 관리 콘솔 경고 페이지를 사용 하 여 각 서버 또는 SAN 배열 내에서 둘 이상의 디스크 오류 확인 합니다. 각 서버 또는 SAN 배열 내에서 둘 이상의 디스크 오류 이면 디스크 오류를 수정 하기 전에 다음 단계를 진행할 수 있습니다. 가능한 한 빨리 디스크 오류를 해결 하려면 Microsoft 지원에 문의 해야 합니다.  
  
#### <a name="synchronize-the-wsus-server"></a>WSUS 서버 동기화  
  
1.  VMM 가상 컴퓨터에 도메인 관리자로 로그온 합니다.  
  
2.  에 **서버 관리자 대시보드**의 **도구** 메뉴를 클릭 하 여 **Windows Server Update Services** (**wsus.msc**).  
  
3.  WSUS 관리 콘솔에서 클릭 **동기화**합니다.  
  
4.  클릭 하 여 동기화를 실행 하지 않는 경우 **지금 동기화** 오른쪽 창에서. 아래쪽 창에서에 동기화 상태가 생깁니다. 동기화가 완료 될 때까지 기다립니다.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>WSUS에서 Microsoft 업데이트를 승인 합니다.  
  
1.  WSUS 콘솔의 왼쪽된 창에서 클릭 **모든 업데이트**합니다.  
  
2.  에 **모든 업데이트** 창에서 클릭는 **승인** 드롭 다운 메뉴에서 집합 **승인** 를 **모든 예외 거부 됨**합니다. 클릭는 **상태** 드롭 다운 메뉴에서 집합 **상태** 를 **모든**합니다. **새로 고침**을 클릭합니다.  
  
    마우스 오른쪽 단추로 클릭는 **제목** 선택 **파일 상태** 다운로드가 완료 된 후에 파일 상태를 확인 하려면.  
  
    선택할 수도 있습니다 **중요 업데이트** 또는 **보안 업데이트** 의 왼쪽된 창 및 보기 사용 가능한 업데이트에 이러한 범주에 대 한 합니다.  
  
    ![모든 업데이트를 선택 하 고 상태를 임의로 변경 합니다. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  모든 업데이트를 선택한 다음 클릭는 **승인** 오른쪽 창에 링크 합니다.  
  
    또한 선택한 업데이트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **승인**합니다. "Microsoft 소프트웨어 사용 조건에 동의" 하 라는 메시지가 표시 될 수 있습니다. 그렇다면, **동의** 계속 하려면는 창에서.  
  
    ![모든 업데이트를 적용 하 고 승인을 클릭을 선택 합니다. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  만든 기기 서버 그룹을 선택 [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;분석 플랫폼 시스템&#41;](configure-windows-server-update-services-wsus.md)합니다.  
  
5.  클릭 **설치 승인**, 클릭 하 고 **확인**합니다.  
  
    ![컴퓨터 그룹에 대 한 업데이트를 승인 합니다. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  에 **승인 진행률** 대화 상자에서 승인 프로세스를 완료 하는 경우 클릭 **닫기**합니다.  
  
    ![업데이트가 승인 된 경우 창을 닫습니다. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>WSUS에서 업데이트가 잘 실행 되었는지 확인 하십시오.  
  
-  모든 업데이트의 파일 상태를 확인 합니다. 각 파일의 제목 왼쪽에 녹색 화살표 아이콘에 필요 합니다. 이 파일은 설치 준비 나타냅니다.  
  
    ![파일 상태: 성공](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    업데이트를 설치 하기 전에 이들이 모두 다운로드 하 고 WSUS 콘솔에서 사용할 수 있는지를 확인 합니다.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>모든 업데이트가 다운로드 되었는지 확인 하려면  
  
-  확인 된 **다운로드 상태** 다음 스크린샷에 표시 된 것 처럼 WSUS 콘솔에서 업데이트 합니다. 확인 **파일이 필요한 업데이트** 0 이면 모든 업데이트가 다운로드 되었는지 확인 하 고 있습니다. 이 숫자는 0 보다, 돌아가서 추가 업데이트를 승인 해야 합니다.  
  
    ![모든 업데이트가 다운로드 되었는지 확인 합니다. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Microsoft 업데이트 적용  
  
1.  시작 하기 전에 열는 [관리 콘솔을 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md), 클릭는 **기기 상태** 탭을 확인 하는  **클러스터** 및 **네트워크** 모든 노드에 대 한 열 녹색 표시 (또는 NA). 경고 이러한 열 중 하나에 있으면 기기 제대로 업데이트를 설치 하지 못할 수 있습니다. 주소에서 모든 기존 경고는 **클러스터** 및 **네트워크** 계속 진행 하기 전에 열입니다.  
  
2.  로그온 하는 *< i n _ > * * *-HST01** 패브릭 도메인 관리자로 노드.  
  
3.  WSUS에 대 한 승인 된 모든 업데이트를 적용 하려면 업데이트 프로그램을 실행 합니다. 참조 [업데이트 프로그램 실행](#RunUpdateWizard) 아래 지침에 대 한 합니다.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>모든 노드에서 업데이트를 확인 합니다.  
  
1.  VMM 노드에서 WSUS 관리 콘솔을 시작 합니다. 이 응용 프로그램을 확인할 수 있습니다 **시작**, **관리 도구**, **Windows Server Update Services**합니다.  
  
2.  확장 **컴퓨터**합니다.  
  
3.  확장 **모든 컴퓨터**합니다.  
  
4.  만든 기기 서버 그룹을 선택 [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;분석 플랫폼 시스템&#41;](configure-windows-server-update-services-wsus.md)합니다.  
  
5.  에 **상태** 드롭 다운 메뉴 **모든** 클릭 **새로 고침**합니다.  
  
6.  확장 **서비스 업데이트**, *<appliance name>*-VMM에서는 **업데이트**, **모든 업데이트**여기서 *<appliance name>* 기기 이름입니다.  
  
7.  에 **모든 업데이트** 창 집합 **승인** 를 **모든 예외 거부 됨**합니다.  
  
8.  에 **모든 업데이트** 창의 설정 **상태** 를 **또는 실패 했거나 필요한**합니다.  
  
9. **새로 고침**을 클릭합니다.  
  
10. 경우 **필요한 업데이트** 0 개, 지원 팀에 문의 지원 보다 큽니다.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>SQL Server PDW 관리 콘솔에서 중요 한 알림이 있는 있는지 확인 하십시오  
  
1.  관리 콘솔을 열고, 기기 상태 탭을 클릭 합니다. 참조 [관리 콘솔을 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)합니다.  
  
2.  확인 된 **클러스터** 및 **네트워크** 모든 노드에 대 한 열 녹색 표시 (또는 NA). 경고 이러한 열 중 하나에 있으면 기기 제대로 업데이트를 설치 하지 못할 수 있습니다. 모든 중요 한 경고가 지원에 문의 합니다.  
  
## <a name="RunUpdateWizard"></a>업데이트 프로그램 실행  
분석 플랫폼 시스템 업데이트 프로그램을 실행 하려면 다음이 지침을 따릅니다.  
  
> [!NOTE]  
> WSUS 시스템은 설계 실행 비동기적으로 시간이 많이 걸리므로 완전히 모든 업데이트를 적용 해야 합니다. 업데이트를 시작 합니다. 업데이트 예약 하지만 즉시 업데이트 동작을 보장 하지 않습니다.  
  
1.  HST01 노드 패브릭 도메인 관리자가에 로그인 되어 있는지 확인 합니다.  
  
2.  명령 프롬프트 창을 열고 다음 명령을 입력 합니다. 대체 *<parameter>* 지정된 정보를 사용 합니다.  
  
**실행 하려면 Microsoft 업데이트:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Microsoft 업데이트 상태를 보고할:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>관련 항목:  
[업데이트 제거 &#40;분석 플랫폼 시스템&#41;](uninstall-microsoft-updates.md)  
[분석 플랫폼 시스템 핫픽스를 적용 &#40;분석 플랫폼 시스템&#41;](apply-analytics-platform-system-hotfixes.md)  
[분석 플랫폼 시스템 핫픽스 제거 &#40;분석 플랫폼 시스템&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[소프트웨어 서비스 &#40;분석 플랫폼 시스템&#41;](software-servicing.md)  
  
