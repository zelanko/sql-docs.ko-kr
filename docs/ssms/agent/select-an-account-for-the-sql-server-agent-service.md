---
title: "SQL Server 에이전트 서비스의 계정 선택 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, accounts
- startup accounts [SQL Server]
- SQL Server Agent service, accounts
- accounts [SQL Server], SQL Server Agent
- Windows groups [SQL Server Agent]
- SQL Server Agent, permissions
- members [SQL Server], SQL Server Agent service
- Windows domain accounts [SQL Server]
- security [SQL Server], SQL Server Agent
ms.assetid: fe658e32-9e6b-4147-a189-7adc3bd28fe7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b8ea899dbbf5b94205ba7cfa0afee4aad262d79a
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="select-an-account-for-the-sql-server-agent-service"></a>SQL Server 에이전트 서비스의 계정 선택
서비스 시작 계정은 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에이전트를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Windows 계정과 해당 네트워크 사용 권한을 정의합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 지정된 사용자 계정으로 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구성 관리자에서 다음 옵션 중 하나를 선택하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스의 계정을 선택하십시오.  
  
-   **기본 제공 계정**. 다음 기본 제공 Windows 서비스 계정 목록에서 선택할 수 있습니다.  
  
    -   **로컬 시스템 계정** . 이 계정의 이름은 NT AUTHORITY\System입니다. 모든 로컬 시스템 리소스에 대해 무제한 액세스 권한이 있는 강력한 계정으로 로컬 컴퓨터에서 Windows **Administrators** 그룹의 멤버이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **sysadmin** 고정 서버 역할의 멤버가 됩니다.  
  
        > [!IMPORTANT]  
        > **로컬 시스템 계정** 옵션은 이전 버전과의 호환성 확보를 위해서만 제공됩니다. 로컬 시스템 계정에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에 필요하지 않은 권한이 있으므로 로컬 시스템 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트를 실행하지 마십시오. 보안 향상을 위해 다음 "Windows 도메인 계정의 권한" 섹션에 나열된 사용 권한을 가진 Windows 도메인 계정을 사용하십시오.  
  
-   **계정 지정**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스가 실행되는 Windows 도메인 계정을 지정할 수 있습니다. Windows **Administrators** 그룹의 멤버가 아닌 Windows 사용자 계정을 선택하는 것이 좋습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 계정이 로컬 **Administrators** 그룹의 멤버가 아니면 다중 서버 관리 작업 시 제한 사항이 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 '지원되는 서비스 계정 유형'을 참조하십시오.  
  
## <a name="windows-domain-account-permissions"></a>Windows 도메인 계정의 권한  
보안 향상을 위해 Windows 도메인 계정을 지정하는 **계정 지정**을 선택합니다. 지정한 Windows 도메인 계정에는 다음 권한이 있어야 합니다.  
  
-   모든 Windows 버전에서 서비스로 로그온할 수 있는 권한(SeServiceLogonRight)  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 계정은 도메인 컨트롤러의 Windows 2000 이전 버전 호환 액세스 그룹의 일부여야 합니다. 그렇지 않으면 Windows Administrators 그룹의 멤버가 아닌 도메인 사용자가 소유한 작업이 실패합니다.  
  
-   Windows 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스가 실행되는 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 프록시를 지원하기 위해 다음 권한이 필요합니다.  
  
    -   트래버스 검사 무시 권한(SeChangeNotifyPrivilege)  
  
    -   프로세스 수준 토큰 대체 권한(SeAssignPrimaryTokenPrivilege)  
  
    -   프로세스의 메모리 할당량 조정 권한(SeIncreaseQuotaPrivilege)  
  
    -   일괄 처리 로그온 유형을 사용하여 로그온할 수 있는 권한(SeBatchLogonRight)  
  
> [!NOTE]  
> 프록시 지원에 필요한 권한이 계정에 없는 경우 **sysadmin** 고정 서버 역할의 멤버만이 작업을 만들 수 있습니다.  
  
> [!NOTE]  
> WMI 경고 알림을 받으려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트의 서비스 계정에 WMI 이벤트를 포함하는 네임스페이스와 ALTER ANY EVENT NOTIFICATION에 대한 권한이 있어야 합니다.  
  
## <a name="sql-server-role-membership"></a>SQL Server 역할 멤버 자격  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 실행하는 계정은 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 역할의 멤버여야 합니다.  
  
-   계정은 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
-   다중 서버 작업 처리를 사용하려면 계정이 마스터 서버의 **msdb** 데이터베이스 역할인 **TargetServersRole** 의 멤버여야 합니다.  
  
## <a name="supported-service-account-types"></a>지원되는 서비스 계정 유형  
다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스에 사용할 수 있는 Windows 계정 유형을 나열합니다.  
  
|서비스 계정 유형|비클러스터형 서버|클러스터형 서버|도메인 컨트롤러(비클러스터형)|  
|------------------------|-------------------------|--------------------|--------------------------------------|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 도메인 계정(Windows Administrators 그룹의 멤버)|지원됨|지원됨|지원됨|  
|Windows 도메인 계정(비관리자)|지원됨<br /><br />아래의 제한 사항 1을 참조하세요.|지원됨<br /><br />아래의 제한 사항 1을 참조하세요.|지원됨<br /><br />아래의 제한 사항 1을 참조하세요.|  
|네트워크 서비스 계정(NT AUTHORITY\NetworkService)|지원됨<br /><br />아래의 제한 사항 1, 3 및 4를 참조하세요.|지원되지 않음|지원되지 않음|  
|로컬 사용자 계정(비관리자)|지원됨<br /><br />아래의 제한 사항 1을 참조하세요.|지원되지 않음|해당 사항 없음|  
|로컬 시스템 계정(NT AUTHORITY\System)|지원됨<br /><br />아래의 제한 사항 2를 참조하세요.|지원되지 않음|지원됨<br /><br />아래의 제한 사항 2를 참조하세요.|  
|로컬 서비스 계정(NT AUTHORITY\LocalService)|지원되지 않음|지원되지 않음|지원되지 않음|  
  
### <a name="limitation-1-using-non-administrative-accounts-for-multiserver-administration"></a>제한 사항 1: 다중 서버 관리에 비관리자 계정 사용  
대상 서버를 마스터 서버에 참여시키면 실패하고 "참여 작업이 실패했습니다."라는 오류 메시지가 표시될 수 있습니다.  
  
이 오류를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 모두 다시 시작합니다. 자세한 내용은 [Start, Stop, Pause, Resume, Restart the Database Engine, SQL Server Agent, or SQL Server Browser Service](http://msdn.microsoft.com/en-us/32660a02-e5a1-411a-9e57-7066ca459df6)을 참조하세요.  
  
### <a name="limitation-2-using-the-local-system-account-for-multiserver-administration"></a>제한 사항 2: 다중 서버 관리에 로컬 시스템 계정 사용  
마스터 서버와 대상 서버가 같은 컴퓨터에 있을 경우에만 로컬 시스템 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 실행할 때 다중 서버 관리가 지원됩니다. 이 구성을 사용하면 대상 서버를 마스터 서버에 참여시킬 때 다음 메시지가 반환됩니다.  
  
"*<target_server_computer_name>*의 에이전트 시작 계정에 대상 서버로 로그인할 권한이 있는지 확인하세요."  
  
이 정보 메시지는 무시해도 됩니다. 참여 작업이 성공적으로 완료됩니다. 자세한 내용은 [다중 서버 환경 만들기](../../ssms/agent/create-a-multiserver-environment.md)를 참조하세요.  
  
### <a name="limitation-3-using-the-network-service-account-when-it-is-a-sql-server-user"></a>제한 사항 3: SQL Server 사용자인 경우 네트워크 서비스 계정 사용  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 네트워크 서비스 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 실행하고 해당 네트워크 서비스 계정에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용자로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 로그인할 수 있는 액세스 권한이 명시적으로 부여된 경우 에이전트가 시작되지 않을 수 있습니다.  
  
이 오류를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 가 실행되고 있는 컴퓨터를 다시 부팅합니다. 이 작업은 한 번만 수행해야 합니다.  
  
### <a name="limitation-4-using-the-network-service-account-when-sql-server-reporting-services-is-running-on-the-same-computer"></a>제한 사항 4: 같은 컴퓨터에서 SQL Server Reporting Services가 실행되고 있을 때 네트워크 서비스 계정 사용  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 네트워크 서비스 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트를 실행하고 같은 컴퓨터에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] 도 실행되고 있으면 에이전트가 시작되지 않을 수 있습니다.  
  
이 오류를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 가 실행되고 있는 컴퓨터를 다시 부팅하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 모두 다시 시작합니다. 이 작업은 한 번만 수행해야 합니다.  
  
## <a name="common-tasks"></a>일반 태스크  
**SQL Server 에이전트 서비스의 시작 계정을 지정하려면**  
  
-   [SQL Server 에이전트의 서비스 시작 계정 설정&amp;#40;SQL Server 구성 관리자&amp;#41;](../../ssms/agent/set-service-startup-account-sql-server-agent-sql-server-configuration-manager.md)  
  
**SQL Server 에이전트의 메일 프로필을 지정하려면**  
  
-   [방법: 데이터베이스 메일을 사용하도록 SQL Server 에이전트 메일 구성(SQL Server Management Studio)](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구성 관리자를 사용하여 운영 체제가 시작될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 시작되도록 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
[Windows 서비스 계정 설정](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014)  
[SQL 컴퓨터 관리자를 사용하여 서비스 관리](http://msdn.microsoft.com/en-us/78dee169-df0c-4c95-9af7-bf033bc9fdc6)  
[SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)  
  

