---
title: WSUS 구성
description: 이 지침에서는 WSUS (Windows Server Update Services) 구성 마법사를 사용 하 여 분석 플랫폼 시스템용 WSUS를 구성 하는 단계를 안내 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 06ac0126bb12668654c04e6a82b20ca551dd925e
ms.sourcegitcommit: a49a66dbda0cb16049e092b49c8318ac3865af3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2020
ms.locfileid: "94983064"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 Windows Server Update Services (WSUS) 구성
이 지침에서는 WSUS (Windows Server Update Services) 구성 마법사를 사용 하 여 분석 플랫폼 시스템용 WSUS를 구성 하는 단계를 안내 합니다. 어플라이언스에 소프트웨어 업데이트를 적용 하려면 먼저 WSUS를 구성 해야 합니다. WSUS가 이미 어플라이언스의 VMM 가상 컴퓨터에 설치 되어 있습니다.  
  
Wsus를 구성 하는 방법에 대 한 자세한 내용은 wsus 웹 사이트에서 [Wsus 단계별 설치 가이드](/windows/deployment/deploy-whats-new) 를 참조 하세요. WSUS를 구성한 후 업데이트를 시작 하려면 [Microsoft 업데이트 &#40;분석 플랫폼 시스템&#41;다운로드 및 적용 ](download-and-apply-microsoft-updates.md) 을 참조 하세요.  
  
> [!WARNING]  
> 이 구성 프로세스 중에 오류가 발생 하면를 중지 하 고 지원 서비스에 문의 하십시오. 오류를 받은 후 오류를 무시 하거나 프로세스에서 계속 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
WSUS를 구성 하려면 다음을 수행 해야 합니다.  
  
-   분석 플랫폼 시스템 어플라이언스 도메인 관리자 계정 로그인 정보가 있어야 합니다.  
  
-   **관리 콘솔** 에 액세스 하 고 어플라이언스 상태 정보를 볼 수 있는 권한이 있는 분석 플랫폼 시스템 로그인이 있어야 합니다.  
  
-   업데이트를 Microsoft 업데이트에서 직접 동기화 하는 대신 업스트림 wsus 서버에서 업데이트를 동기화 하려는 경우 업스트림 WSUS 서버의 IP 주소를 알고 있어야 합니다. 업스트림 WSUS 서버가 익명 연결을 허용 하도록 설정 되어 있고 SSL을 지원 하도록 설정 되어 있는지 확인 합니다.  
  
-   어플라이언스에서 프록시 서버를 사용 하 여 업스트림 서버 또는 Microsoft 업데이트에 액세스 하는 경우 프록시 서버의 IP 주소를 알고 있어야 합니다.  
  
-   대부분의 경우 WSUS는 어플라이언스 외부의 서버에 액세스 해야 합니다. 이 사용 시나리오를 지원 하기 위해 분석 플랫폼 시스템 DNS는 외부 DNS 서버를 사용 하 여 어플라이언스 외부에서 이름을 확인할 수 있도록 하 Virtual Machines는 외부 이름 전달자를 지원 하도록 구성 될 수 있습니다. 자세한 내용은 [Dns 전달자를 사용 하 여 비 어플라이언스 DNS 이름 확인 &#40;분석 플랫폼 시스템&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)을 참조 하세요.  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>WSUS (Windows Server Update Services를 구성 하려면  
  
1.  **관리 콘솔** 에 로그인 합니다. **어플라이언스 상태** 탭에서 **클러스터** 및 **네트워크** 열이 모든 노드에 녹색 또는 **NA** 를 표시 하는지 확인 합니다. **어플라이언스 상태의** 모든 노드에 대 한 상태 표시기를 확인 합니다.  
  
    -   녹색 또는 NA 표시기를 계속 사용 해도 됩니다.  
  
    -   중요 하지 않은 (노란색) 경고 오류를 평가 합니다. 일부 경우에 경고 메시지가 업데이트를 차단 하지 않습니다. C:\에 없는 디스크 볼륨 오류가 발생 한 경우 드라이브, 디스크 볼륨 오류를 확인 하기 전에 다음 단계를 진행할 수 있습니다.  
  
    -   계속 하려면 빨간색 표시기를 가장 먼저 해결 해야 합니다. 디스크 오류가 발생 하는 경우 **관리 콘솔 경고** 페이지를 사용 하 여 각 서버 또는 SAN 배열 내에 디스크 오류가 둘 이상 없는지 확인 합니다. 각 서버 또는 SAN 배열 내에 디스크 오류가 둘 이상 없는 경우 디스크 오류를 수정 하기 전에 다음 단계를 진행할 수 있습니다. 가능한 한 빨리 디스크 오류를 해결 하려면 Microsoft 지원에 문의 하세요.  
  
2.  어플라이언스 도메인 관리자로 VMM 가상 머신에 로그온 합니다.  
  
3.  구성 마법사를 시작 합니다.  
  
    #### <a name="to-launch-the-configuration-wizard"></a>구성 마법사를 시작 하려면  
  
    1.  **서버 관리자 대시보드의** **도구** 메뉴에서 **Windows Server Update Services** 를 클릭 합니다.  
  
    2.  **업데이트 서비스** 창의 왼쪽 창에서 가상 컴퓨터 관리 노드 서버 (**_appliance_domain_ VMM**)를 클릭 하 여 확장 한 다음 **옵션** 을 클릭 합니다.  
  
    3.  **옵션** 창에서 **WSUS 서버 구성 마법사** 를 클릭 하 여 구성 마법사를 시작 합니다.  
  
        ![서버 관리자 대시보드 메뉴](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  WSUS 마법사를 처음 실행 하는 경우 업데이트를 저장할 디렉터리를 구성 하 라는 메시지가 표시 될 수 있습니다. `C:\wsus` 는 적절 한 위치입니다. 그러나 다른 경로를 제공할 수도 있습니다.  
  
        ![WSUS 경로](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  마법사를 완료 하기 전에 완료 하려면 항목 목록을 **시작 하기 전에** 를 검토 합니다.  
  
        ![WSUS 시작하기 전 주의 사항](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  **Microsoft 업데이트 개선 프로그램에 참여** 페이지에서 **예, Microsoft 업데이트 개선 프로그램에 참여** 합니다 .를 선택 하 고 **다음** 을 클릭 합니다.  
  
        ![WSUS 개선 프로그램](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    이제 **업스트림 서버 선택** 페이지가 표시 됩니다. 다음 스크린샷은 구성 마법사의 시작 지점입니다.  
  
    ![WSUS 업스트림 서버 동기화](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  업스트림 서버를 선택 합니다.  
  
    WSUS 구성 마법사의 **업스트림 서버 선택** 페이지에서 가상 컴퓨터 관리 노드의 WSUS가 업스트림 서버에 연결 하 여 소프트웨어 업데이트를 가져오는 방법을 선택 합니다. 두 가지 선택 사항은 업스트림 서버를 [Microsoft 업데이트](https://go.microsoft.com/fwlink/?LinkId=133349) 와 동기화 하거나 업데이트를 다른 Windows Server Update Services 서버와 동기화 하는 것입니다.  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Microsoft 업데이트를 사용 하 여 업데이트 하려면  
  
    1.  Microsoft 업데이트와 동기화 하도록 선택 하면 **업스트림 서버 선택** 페이지를 변경할 필요가 없습니다. **다음** 을 클릭합니다.  
  
        ![WSUS 업스트림 서버 동기화](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>다른 WSUS 서버에서 업데이트 하려면  
  
    1.  Microsoft 업데이트 (업스트림 서버)가 아닌 원본과 동기화 하도록 선택 하는 경우 서버 (IP 주소 입력)와이 서버가 업스트림 서버와 통신할 포트를 지정 합니다.  
  
        ![WSUS에서 WSUS 업스트림 서버 동기화](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  SSL(Secure Sockets Layer) (SSL)을 사용 하려면 **업데이트 정보를 동기화 할 때 Ssl 사용** 확인란을 선택 합니다. 이 경우 서버는 동기화에 포트 443을 사용 합니다.  
  
        ![WSUS SSL에서 WSUS 업스트림 서버 동기화](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  이 서버가 복제 서버인 경우에는 **업스트림 서버의 복제 서버** 확인란을 선택합니다. **업데이트 정보를 동기화 할 때 SSL 사용** 과 **업스트림 서버의 복제본** 을 모두 선택할 수 있습니다.  
  
        ![WSUS 업스트림 서버 복제본](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  이 시점에서 업스트림 서버 구성을 완료 했습니다. **다음** 을 클릭 하거나 왼쪽 탐색 창에서 **프록시 서버 지정** 을 선택 합니다.  
  
5.  프록시 서버를 지정 합니다.  
  
    이 서버에 Microsoft 업데이트 또는 다른 업스트림 서버에 액세스 하기 위해 프록시 서버가 필요한 경우 여기에서 프록시 서버 설정을 구성할 수 있습니다. 그렇지 않으면 **다음** 을 클릭 합니다.  
  
    ![WSUS 프록시](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>프록시 서버 설정을 구성하려면  
  
    1.  구성 마법사의 **프록시 서버 지정** 페이지에서 **동기화 할 때 프록시 서버 사용** 확인란을 선택한 다음 해당 상자에 프록시 서버 IP 주소 (이름 없음) 및 포트 번호 (기본적으로 포트 80)를 입력 합니다.  
  
    2.  특정 사용자의 자격 증명을 사용해 프록시 서버에 연결할 경우 **사용자 자격 증명을 사용하여 프록시 서버에 연결** 확인란을 선택한 다음 해당 상자에 사용자 이름, 도메인 및 사용자 암호를 입력합니다. 프록시 서버에 연결 하는 사용자에 대 한 기본 인증을 사용 하도록 설정 하려는 경우는 **기본 인증 허용 (암호는 일반 텍스트로 보내짐)** 확인란입니다.  
  
        ![WSUS 프록시 자격 증명](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  이 시점에서 프록시 서버 구성을 완료 했습니다. **다음** 을 클릭해 동기화 프로세스의 설정을 시작할 수 있는 그 다음 페이지로 이동합니다.  
  
6.  연결을 시작 합니다.  
  
    ![WSUS 프록시 연결 시작](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    **연결 시작** 을 클릭 합니다.  
  
    연결에 성공한 후 **다음** 을 클릭 하 여 언어를 선택할 수 있는 다음 페이지로 이동 합니다.  
  
7.  언어를 선택 합니다.  
  
    **이러한 언어의 업데이트만 다운로드를** 선택 합니다.  
  
    **영어** 를 선택 하 고 **다음** 을 클릭 합니다.  
  
    ![언어 선택](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  제품을 선택 합니다.  
  
    > [!NOTE]  
    > 업스트림 서버를 사용 하는 경우 제품을 선택 하지 못할 수 있습니다. 이 옵션을 사용할 수 없는 경우이 단계를 건너뜁니다.

    > [!WARNING]  
    > SQL Server 2016 업데이트를 제외 하세요.
  
    선택한 모든 업데이트를 선택 취소 합니다.  
  
    **SQL Server 2012**, **SQL Server 2014**, **windows Server 2012 R2**, **system Center 2012 R2-Virtual Machine Manager**, **windows server 2016** 및 **system center 2016-Virtual Machine Manager** 을 선택 하 고 **다음** 을 클릭 합니다.  
  
9. 분류를 선택 합니다.  
  
    > [!NOTE]  
    > 업스트림 서버를 사용 하는 경우 분류를 선택 하지 못할 수 있습니다.  이 옵션을 사용할 수 없는 경우이 단계를 건너뜁니다.  
  
    이전에 선택한 모든 업데이트를 선택 취소 합니다.  
  
    분석 플랫폼 시스템 어플라이언스에 대해 동기화 할 업데이트에 대 한 **중요 업데이트**, **보안 업데이트** 및 **업데이트 롤업을** 선택 하 고 **다음** 을 클릭 합니다.  
  
    ![분류 선택](./media/configure-windows-server-update-services-wsus/sql-server-pdw-wsus-choose-classifications.png "sql server-pdw-wsus-선택-분류")  
  
10. 동기화 일정을 구성 합니다.  
  
    **수동으로 동기화** 를 선택 하 고 **다음** 을 클릭 합니다.  
  
    ![일정 동기화 설정](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. 초기 동기화를 시작 합니다.  
  
    **초기 동기화 시작** 을 선택 하 고 **다음** 을 클릭 합니다.  
  
12. 마치고.  
  
    **Finish** 를 클릭합니다.  
  
## <a name="group-the-appliance-servers-in-wsus"></a><a name="bkmk_WSUSGroup"></a>WSUS에서 어플라이언스 서버 그룹화  
분석 플랫폼 시스템에 대해 WSUS를 구성한 후 다음 단계는 어플라이언스 서버를 그룹화 하는 것입니다. 모든 어플라이언스 서버를 그룹에 추가 하면 WSUS는 기기의 모든 서버에 소프트웨어 업데이트를 적용할 수 있습니다.  
  
> [!NOTE]  
> WSUS 시스템은 비동기식으로 실행 되도록 설계 되었습니다. 작업을 시작 하면 즉시 업데이트가 발생 하지 않습니다. 따라서 WSUS 대화 상자에 컴퓨터가 표시 될 때까지 잠시 기다려야 할 수도 있습니다. `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"`항목의 끝에 설명 된 명령을 실행 하 여 [Microsoft 업데이트를 다운로드 하 고 적용 &#40;분석 플랫폼 시스템&#41;](download-and-apply-microsoft-updates.md) 를 통해 대화 상자를 새로 고칠 수 있습니다.  
  
#### <a name="to-group-the-appliance-servers"></a>어플라이언스 서버를 그룹화 하려면  
  
1.  WSUS 콘솔을 열고 **모든 컴퓨터** 를 마우스 오른쪽 단추로 클릭 한 다음 **컴퓨터 그룹 추가** 를 클릭 합니다.  
  
    ![컴퓨터 그룹을 추가합니다.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  컴퓨터 그룹에 "APS" 이름을 입력 한 다음 **추가** 를 클릭 합니다.  
  
    ![새 컴퓨터 그룹의 이름을 입력합니다.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  **모든 컴퓨터** 를 다시 클릭 하 고 **상태** 드롭다운 메뉴의 상태를 **모두** 로 변경한 다음 **새로 고침** 을 클릭 합니다. 방금 추가한 새 그룹을 보려면 왼쪽의 트리 컨트롤에서 **모든 컴퓨터** 를 클릭 하 여 확장 해야 할 수도 있습니다.  
  
    ![상태를 Any로 변경 하 고 새로 고침을 클릭 합니다.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  어플라이언스의 일부인 모든 컴퓨터를 선택 하 고 마우스 오른쪽 단추를 클릭 한 다음 **구성원 변경** 을 클릭 합니다.  
  
    ![모든 PDW 컴퓨터의 구성원십을 변경합니다.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  확인란을 클릭 한 다음 **확인을** 클릭 하 여 만든 새 컴퓨터 그룹을 선택 합니다.  
  
    ![컴퓨터 그룹 구성원십 선택](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  새 컴퓨터 그룹을 선택 하 고, **상태** 를 **Any** 로 변경한 다음, **새로 고침** 을 클릭 합니다. 이제 모든 컴퓨터가이 그룹에 할당 되 고 오른쪽 창에 나열 됩니다. 일반적으로 노드에 **이 노드가 아직 상태를 보고 하지** 않은 등의 경고가 표시 되는 경우 계속 안전 합니다.  
  
    ![상태를 임의로 변경하고 새로 고침을 클릭합니다.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
