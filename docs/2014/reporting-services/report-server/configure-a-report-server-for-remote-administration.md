---
title: 원격 관리를 위한 보고서 서버 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- WMI provider [Reporting Services], remote configuration
- configuration management [WMI]
- report servers [Reporting Services], configuring
- remote server administration [Reporting Services]
ms.assetid: 8c7f145f-3ac2-4203-8cd6-2a4694395d09
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e83f539e1ffad77a337fc3e0142379da2ff0f703
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104098"
---
# <a name="configure-a-report-server-for-remote-administration"></a>원격 관리를 위한 보고서 서버 구성
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 보고서 서버 인스턴스를 로컬 또는 원격으로 구성할 수 있습니다. 원격 보고서 서버 인스턴스를 구성하려면 Reporting Services 구성 도구를 사용하거나, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI(Windows Management Instrumentation) 공급자를 사용하는 사용자 지정 코드를 작성할 수 있습니다. Reporting Services 구성 도구는 WMI 공급자에 대한 그래픽 인터페이스를 제공하므로 이 도구를 사용하면 코드를 작성하지 않고도 보고서 서버를 구성할 수 있습니다. 이 도구를 시작할 때 연결할 원격 서버를 지정할 수 있습니다.  
  
 구성 도구를 사용하여 원격 보고서 서버를 구성하기 전에 이 항목의 지침에 따라 Windows 방화벽에서 포트 설정, 원격 연결 설정 및 원격 WMI 요청 설정 작업을 수행해야 합니다.  
  
 적절한 구성을 사용하면 다음 오류를 피할 수 있습니다.  
  
 `The machine could not be found.`  
  
 `"The RPC server is unavailable. (Exception from HRESULT: 0x800706BA)".`  
  
## <a name="prerequisites"></a>사전 요구 사항  
 방화벽 설정을 수정하려면 로컬 Administrators 그룹의 멤버여야 하며 로컬로 로그온해야 합니다. 원격 컴퓨터의 Windows 방화벽 설정을 원격 연결을 통해 수정할 수는 없습니다.  
  
 관리자가 아닌 사용자가 원격 관리를 사용할 수 있도록 하려면 DCOM(Distributed Component Object Model) 원격 활성화 권한을 해당 계정에 부여해야 합니다. 관리자가 아닌 사용자가 액세스할 수 있도록 서버를 구성하는 방법은 이 항목에 설명되어 있습니다.  
  
 일부 조직에는 특정 운영 체제나 사용자에 대해 원격 서버 관리를 사용할 수 없도록 하는 그룹 정책이 있습니다. 따라서 방화벽 설정을 수정하기 전에 네트워크 관리자에게 문의하여 원격 관리에 대한 제한이 있는지 여부를 확인하십시오.  
  
 자세한 내용은 MSDN에 있는 Platform SDK 설명서에서 [Windows 방화벽을 통한 연결](https://go.microsoft.com/fwlink/?LinkId=63615) 을 참조하십시오.  
  
## <a name="tasks"></a>태스크  
 원격 보고서 서버 구성을 활성화하는 태스크는 다음과 같습니다.  
  
-   Windows 방화벽에서 포트를 설정하여 보고서 서버와 SQL Server 데이터베이스 엔진 인스턴스에서 사용하는 포트에 대한 요청을 허용합니다.  
  
-   보고서 서버 데이터베이스를 호스팅하는 데이터베이스 엔진 인스턴스에 대한 원격 연결을 설정합니다. 원격 연결은 보고서 서버 데이터베이스 연결을 구성하고 암호화 키를 관리하는 데 필요합니다.  
  
-   원격 WMI 요청이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 방화벽을 통과하도록 설정합니다.  
  
-   관리 권한이 없는 사용자가 관리할 수 있도록 원격 보고서 서버를 구성하는 경우 표준 Windows 사용자 계정에 대한 원격 WMI 액세스가 가능하도록 DCOM 권한을 설정해야 합니다. WMI에서는 원격 호출을 전송하는 데 DCOM을 사용하므로 로컬 관리자로 로그온하지 않은 사용자가 서버를 구성할 수 있도록 하려면 DCOM 권한을 설정해야 합니다.  
  
-   관리 권한이 없는 사용자가 관리할 수 있도록 원격 보고서 서버를 구성하는 경우 보고서 서버 WMI 네임스페이스에 대한 WMI 권한도 설정해야 합니다. 기본적으로 로컬 Administrators 그룹의 모든 멤버는 보고서 서버 WMI 네임스페이스에 액세스할 수 있습니다. 관리자가 아닌 사용자에게 액세스 권한을 부여하려면 권한을 설정해야 합니다.  
  
 이러한 태스크를 수행하는 방법은 이 항목에 설명되어 있습니다.  
  
### <a name="to-open-ports-in-windows-firewall"></a>Windows 방화벽에서 포트를 열려면  
  
1.  [데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)합니다.  
  
2.  [Configure a Firewall for Report Server Access](configure-a-firewall-for-report-server-access.md)합니다.  
  
### <a name="to-configure-remote-connections-to-the-report-server-database"></a>보고서 서버 데이터베이스에 대한 원격 연결을 구성하려면  
  
1.  **시작**을 클릭하고 **프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  왼쪽 창에서 **SQL Server 네트워크 구성**을 확장한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 **프로토콜**을 클릭합니다.  
  
3.  세부 정보 창에서 TCP/IP 및 명명된 파이프 프로토콜을 설정한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작합니다.  
  
### <a name="to-enable-remote-administration-in-windows-firewall"></a>Windows 방화벽에서 원격 관리를 활성화하려면  
  
1.  원격 관리를 활성화할 컴퓨터에 로컬 관리자로 로그온합니다.  
  
2.  보고서 서버는 Windows Vista에서 실행 중인를 마우스 오른쪽 단추로 클릭 **명령 프롬프트** 선택한 **관리자 권한으로 실행**합니다. 다른 운영 체제의 경우 명령 프롬프트 창을 엽니다.  
  
3.  다음 명령을 실행합니다.  
  
    ```  
    netsh.exe firewall set service type=REMOTEADMIN mode=ENABLE scope=ALL  
    ```  
  
     scope에는 다른 옵션을 지정해도 됩니다. 자세한 내용은 Windows 방화벽 제품 설명서를 참조하십시오.  
  
4.  원격 관리가 활성화되었는지 확인합니다. 다음 명령을 실행하여 상태를 확인할 수 있습니다.  
  
    ```  
    netsh.exe firewall show state  
    ```  
  
5.  컴퓨터를 다시 부팅합니다.  
  
### <a name="to-set-dcom-permissions-to-enable-remote-wmi-access-for-non-administrators"></a>관리자가 아닌 사용자가 원격 WMI에 액세스할 수 있도록 DCOM 권한을 설정하려면  
  
1.  시작 메뉴에서 **관리 도구**를 가리키고 **구성 요소 서비스**를 클릭합니다.  
  
     Windows vista 시작 메뉴를 클릭 **모든 프로그램**, 클릭 **실행**를 입력 한 다음 `mmc comexp.msc`합니다.  
  
2.  구성 요소 서비스 폴더를 엽니다.  
  
3.  컴퓨터 폴더를 엽니다.  
  
4.  내 컴퓨터를 선택합니다.  
  
5.  **동작** 메뉴에서 **속성**을 선택합니다.  
  
6.  **COM 보안**을 클릭합니다.  
  
7.  **시작 및 활성화 권한**에서 **제한값 편집**을 클릭합니다.  
  
8.  **시작 및 활성화 권한**에 사용자의 이름이 표시되어 있지 않으면 **추가**를 클릭합니다.  
  
9. 사용자 계정 이름을 입력하고 **확인**을 클릭합니다.  
  
10. **\<사용자 또는 그룹>의 권한**의 **허용** 열에서 **원격 시작** 및 **원격 활성화**를 선택한 다음 **확인**을 클릭합니다.  
  
### <a name="to-set-permissions-on-the-report-server-wmi-namespace-for-non-administrators"></a>관리자가 아닌 사용자가 액세스할 수 있도록 보고서 서버 WMI 네임스페이스에 대한 권한을 설정하려면  
  
1.  시작 메뉴에서 **관리 도구**를 가리키고 **컴퓨터 관리**를 클릭합니다.  
  
2.  서비스 및 애플리케이션 폴더를 엽니다.  
  
3.  **WMI 컨트롤**을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
4.  **보안**을 클릭합니다.  
  
5.  Root 폴더를 엽니다.  
  
6.  Microsoft 폴더를 엽니다.  
  
7.  SQLServer 폴더를 엽니다.  
  
8.  ReportServer 폴더를 엽니다.  
  
9. 인스턴스 폴더를 엽니다. 기본 인스턴스를 설치한 경우 폴더는 MSSQLSERVER입니다.  
  
10. v10 폴더를 엽니다.  
  
11. Admin 폴더를 선택한 다음 **보안**을 클릭합니다.  
  
12. **추가**를 클릭한 다음 서버를 관리하는 데 사용할 사용자 계정을 입력합니다.  
  
13. **허용** 열에서 **계정 사용**, **원격으로부터 사용 가능**및 **보안 읽기**를 선택한 다음 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
