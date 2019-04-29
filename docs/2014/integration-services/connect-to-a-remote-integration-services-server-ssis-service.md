---
title: 원격 Integration Services (SSIS 서비스) 서버에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], remote instance
- Integration Services service, connecting
- Integration Services service, remote instance
- service [Integration Services], connecting
ms.assetid: 9487aff1-44d8-42c1-8176-bb9891d4632d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d2e64744ea39296d16fbe88ad20993e8909988d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62834035"
---
# <a name="connect-to-a-remote-integration-services-server-ssis-service"></a>원격 Integration Services 서버에 연결(SSIS 서비스)
    
> [!IMPORTANT] 
> 이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]는 이전 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 버전과의 호환성을 위한 서비스를 지원합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 나 다른 관리 애플리케이션에서 원격 서버의 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 인스턴스에 연결하려면 애플리케이션 사용자에게 서버에 대한 특정 권한 집합이 필요합니다.  
  
> [!IMPORTANT] 
> 원격 서버에 저장된 패키지를 관리하는 경우 해당 원격 서버에 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스 인스턴스에 연결할 필요가 없습니다. 대신 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 원격 서버에 저장된 패키지를 표시하도록 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 서비스에 대한 구성 파일을 편집합니다. 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](service/integration-services-service-ssis-service.md)버전과의 호환성을 위한 서비스를 지원합니다.  
  
## <a name="connecting-to-integration-services-on-a-remote-server"></a>원격 서버의 Integration Services에 연결  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>원격 서버의 Integration Services에 연결하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  **파일**, **개체 탐색기 연결** 을 차례로 선택하여 **서버에 연결** 대화 상자를 표시합니다.  
  
3.  **서버 유형** 목록에서 **Integration Services** 를 선택합니다.  
  
4.   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 입력란에 **서버의 이름을** 입력합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 인스턴스에 국한되지 않습니다. Integration Services 서버가 실행 중인 컴퓨터의 이름을 사용하여 서비스에 연결합니다.  
  
5.  **연결**을 클릭합니다.  
  
> [!NOTE]  
>  **서버 찾아보기** 대화 상자에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 원격 인스턴스가 표시되지 않습니다. 또한 **옵션** 단추를 클릭하면 표시되는 **서버에 연결** 대화 상자의 **연결 옵션** 탭에서 사용할 수 있는 옵션은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 연결에는 적용되지 않습니다.  
  
## <a name="eliminating-the-access-is-denied-error"></a>"액세스가 거부되었습니다." 오류 제거  
 충분한 권한이 없는 사용자가 원격 서버의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 인스턴스에 연결하려고 하면 "액세스가 거부되었습니다."라는 오류 메시지가 나타납니다. 사용자에게 필요한 DCOM 권한을 부여하면 이 오류 메시지를 방지할 수 있습니다.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>Windows Server 2003 또는 Windows XP에서 원격 사용자의 권한을 구성하려면  
  
1.  사용자가 로컬 Administrators 그룹의 멤버가 아니면 분산 COM 사용자 그룹에 해당 사용자를 추가합니다. 이 작업은 **관리 도구** 메뉴에서 액세스할 수 있는 컴퓨터 관리 MMC 스냅인에서 수행할 수 있습니다.  
  
2.  제어판을 열고 **관리 도구** 를 두 번 클릭한 다음 **구성 요소 서비스** 를 두 번 클릭하여 구성 요소 서비스 MMC 스냅인을 시작합니다.  
  
3.  콘솔의 왼쪽 창에서 **구성 요소 서비스** 노드를 확장합니다. **컴퓨터** 노드를 확장하고 **내 컴퓨터**를 확장한 다음 **DCOM 구성** 노드를 클릭합니다.  
  
4.  **DCOM 구성** 노드를 선택하고 구성할 수 있는 애플리케이션 목록에서 SQL Server Integration Services 11.0을 선택합니다.  
  
5.  SQL Server Integration Services 11.0을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **SQL Server Integration Services 11.0 속성** 대화 상자에서 **보안** 탭을 선택합니다.  
  
7.  **시작 및 활성화 권한**에서 **사용자 지정**을 선택하고 **편집** 을 클릭하여 **시작 권한** 대화 상자를 엽니다.  
  
8.  **시작 권한** 대화 상자에서 사용자를 추가하거나 삭제하고 적절한 사용자 및 그룹에 적절한 권한을 할당합니다. 로컬 시작, 원격 시작, 로컬 활성화 및 원격 활성화 권한을 할당할 수 있습니다. 시작 권한은 서비스를 시작 및 중지할 수 있는 권한을 부여하거나 거부하고, 활성화 권한은 서비스에 연결할 수 있는 권한을 부여하거나 거부합니다.  
  
9. 확인을 클릭하여 대화 상자를 닫습니다.  
  
10. **액세스 권한**에서 7-8단계를 반복하여 적절한 사용자 및 그룹에 적절한 권한을 할당합니다.  
  
11. MMC 스냅인을 닫습니다.  
  
12. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 다시 시작합니다.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>Windows 2000 최신 서비스 팩에서 원격 사용자의 권한을 구성하려면  
  
1.  명령 프롬프트에서 **dcomcnfg.exe** 를 실행합니다.  
  
2.  **DCOM 구성 속성** 대화 상자의 **애플리케이션** 페이지에서 SQL Server Integration Services 11.0을 선택하고 **속성**을 클릭합니다.  
  
3.  **보안** 페이지를 선택합니다.  
  
4.  두 개의 개별 대화 상자를 사용하여 **액세스 권한** 과 **시작 권한**을 구성합니다. 원격 액세스와 로컬 액세스는 구별할 수 없습니다. 액세스 권한에는 로컬 및 원격 액세스가 포함되고 시작 권한에는 로컬 및 원격 시작이 포함됩니다.  
  
5.  대화 상자 및 **dcomcnfg.exe**를 닫습니다.  
  
6.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 다시 시작합니다.  
  
## <a name="connecting-by-using-a-local-account"></a>로컬 계정을 사용하여 연결  
 클라이언트 컴퓨터에서 로컬 Windows 계정으로 작업하는 경우 동일한 이름 및 암호와 적절한 권한이 있는 로컬 계정이 원격 컴퓨터에 있는 경우에만 원격 컴퓨터의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 연결할 수 있습니다.  
  
## <a name="by-default-the-ssis-service-does-not-support-delegation"></a>기본적으로 위임이 지원되지 않는 SSIS 서비스  
기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에서는 자격 증명의 위임(이중 홉이라고도 함)이 지원되지 않습니다. 이 시나리오에서는 클라이언트 컴퓨터에서 작업 중이고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 두 번째 컴퓨터에서 실행 중이며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 세 번째 컴퓨터에서 실행 중이라고 가정합니다. 먼저 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 가 클라이언트 컴퓨터에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 실행 중인 두 번째 컴퓨터로 자격 증명을 성공적으로 전달합니다. 그러나 그런 다음 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 두 번째 컴퓨터에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 실행 중인 세 번째 컴퓨터에 자격 증명을 위임할 수 없습니다.

SQL Server 서비스 계정에 **모든 서비스에 대한 위임용으로 이 사용자 트러스트(Kerberos만)** 권한을 부여하여 자격 증명을 위임할 수 있으며 하위 프로세스로 Integration Services 서비스(ISServerExec.exe)가 시작됩니다. 이 권한을 부여하기 전에 조직의 보안 요구 사항을 충족하는지 여부를 고려해야 합니다.

자세한 내용은 [Getting Cross Domain Kerberos and Delegation working with SSIS Package](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/)(SSIS 패키지로 도메인 간 Kerberos 및 위임 가져오기)를 참조하세요.
  
## <a name="see-also"></a>관련 항목  
 [SSIS 서비스 액세스에 대한 Windows 방화벽 구성](../../2014/integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md)  
  
  
