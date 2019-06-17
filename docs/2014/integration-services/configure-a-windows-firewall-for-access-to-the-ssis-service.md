---
title: SSIS 서비스에 대 한 액세스를 위한 Windows 방화벽 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], firewalls
- Windows Firewall [Integration Services]
- unauthorized access [Integration Services]
- Integration Services service, firewalls
- firewall systems [Integration Services]
- SQL Server Integration Services, firewalls
- SSIS, firewalls
ms.assetid: 39975cf2-c351-4205-8c39-27a0fadfb010
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b2c6a19eb44b1d53fe87bef0183bdafbb3ec105b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060849"
---
# <a name="configure-a-windows-firewall-for-access-to-the-ssis-service"></a>SSIS 서비스 액세스에 대한 Windows 방화벽 구성
    
> [!IMPORTANT]  
>  이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]는 이전 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 버전과의 호환성을 위한 서비스를 지원합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
 Windows 방화벽 시스템을 사용하면 네트워크 연결을 통해 이루어지는 컴퓨터 리소스에 대한 무단 액세스를 차단할 수 있습니다. 이 방화벽을 통해 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에 액세스하려면 액세스 가능하도록 방화벽을 구성해야 합니다.  
  
> [!IMPORTANT]  
>  원격 서버에 저장된 패키지를 관리하는 경우 해당 원격 서버에 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스 인스턴스에 연결할 필요가 없습니다. 대신 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 원격 서버에 저장된 패키지를 표시하도록 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 서비스에 대한 구성 파일을 편집합니다. 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](configuring-the-integration-services-service-ssis-service.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에는 DCOM 프로토콜이 사용됩니다. 방화벽을 통한 DCOM 프로토콜 작동 하는 방법에 대 한 자세한 내용은 문서를 참조 하세요. "[방화벽과 함께 분산 COM 사용 하 여](https://manualzz.com/doc/19762578/using-distributed-com-with-firewalls-by-michael-nelson-in...)"입니다.  
  
 사용할 수 있는 방화벽 시스템은 여러 가지가 있습니다. Windows 방화벽 이외의 다른 방화벽을 사용하는 경우 사용 중인 시스템별 정보를 보려면 해당 방화벽 설명서를 참조하십시오.  
  
 방화벽에서 애플리케이션 수준의 필터링이 지원되는 경우 Windows에서 제공하는 사용자 인터페이스를 사용하여 프로그램 및 서비스와 같이 방화벽을 통해 허용되는 예외를 지정할 수 있습니다. 그렇지 않으면 제한된 TCP 포트 집합을 사용하도록 DCOM을 구성해야 합니다. 이전에 제공된 Microsoft 웹 사이트 링크에는 사용할 TCP 포트 지정 방법에 대한 정보가 포함됩니다.  
  
 Integration Services 서비스에는 포트 135가 사용되며 이 포트는 변경할 수 없습니다. SCM(서비스 제어 관리자)에 액세스하려면 TCP 포트 135를 열어야 합니다. SCM은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스 시작 및 중지와 실행 중인 서비스에 대한 제어 요청 전송과 같은 태스크를 수행합니다.  
  
 다음 섹션의 정보는 Windows 방화벽에만 해당됩니다. 명령 프롬프트에서 명령을 실행하거나 Windows 방화벽 대화 상자에서 속성을 설정하여 Windows 방화벽 시스템을 구성할 수 있습니다.  
  
 기본 Windows 방화벽 설정 방법과 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
## <a name="configuring-a-windowsfirewall"></a>Windows 방화벽 구성  
 다음 명령을 사용하면 TCP 포트 135를 열고, 예외 목록에 MsDtsSrvr.exe를 추가하고, 방화벽에 대한 차단 해제 범위를 지정할 수 있습니다.  
  
#### <a name="to-configure-a-windowsfirewall-using-the-command-prompt-window"></a>명령 프롬프트 창을 사용하여 Windows 방화벽을 구성하려면  
  
1.  다음 명령을 실행합니다. `netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET`  
  
2.  다음 명령을 실행합니다. `netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET`  
  
    > [!NOTE]  
    >  모든 컴퓨터와 인터넷상의 컴퓨터에 대해서도 방화벽을 열려면 scope=SUBNET을 scope=ALL로 바꿉니다.  
  
 다음 절차에서는 Windows 사용자 인터페이스를 사용하여 TCP 포트 135를 열고, 예외 목록에 MsDtsSrvr.exe를 추가하고, 방화벽에 대한 차단 해제 범위를 지정할 수 있습니다.  
  
#### <a name="to-configure-a-firewall-using-the-windowsfirewall-dialog-box"></a>Windows 방화벽 대화 상자를 사용하여 방화벽을 구성하려면  
  
1.  제어판에서 **Windows 방화벽**을 두 번 클릭합니다.  
  
2.  **Windows 방화벽** 대화 상자에서 **예외** 탭을 클릭한 다음 **프로그램 추가**를 클릭합니다.  
  
3.  **프로그램 추가** 대화 상자에서 **찾아보기**를 클릭하고 Program Files\Microsoft SQL Server\100\DTS\Binn 폴더로 이동한 다음 MsDtsSrvr.exe를 클릭하고 **열기**를 클릭합니다. **확인** 을 클릭하여 **프로그램 추가** 대화 상자를 닫습니다.  
  
4.  **예외** 탭에서 **포트 추가**를 클릭합니다.  
  
5.  **포트 추가** 대화 상자의 **이름** 상자에 **RPC(TCP/135)** 나 다른 설명이 포함된 이름을 입력하고 **포트 번호** 상자에 **135** 를 입력한 다음 **TCP**를 선택합니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 항상 포트 135를 사용합니다. 다른 포트를 지정할 수 없습니다.  
  
6.  **포트 추가** 대화 상자에서는 선택적으로 **범위 변경** 을 클릭하여 기본 범위를 수정할 수 있습니다.  
  
7.  **범위 변경** 대화 상자에서 **내 네트워크(서브넷 전용)** 을 선택하거나 사용자 지정 목록을 입력한 다음 **확인**을 클릭합니다.  
  
8.  **확인** 을 클릭하여 **포트 추가**대화 상자를 닫습니다.  
  
9. **Windows 방화벽** 대화 상자를 닫으려면 **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  Windows 방화벽을 구성하려면 이 절차에서 제어판의 **Windows 방화벽** 항목을 사용합니다. **Windows 방화벽** 항목은 현재 네트워크 위치 프로필에 대한 방화벽만 구성합니다. 그러나 **netsh** 명령줄 도구 또는 고급 보안이 설정된 Windows 방화벽 MMC( [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console) 스냅인을 사용하여 Windows 방화벽을 구성할 수도 있습니다. 이러한 도구에 대한 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](service/integration-services-service-ssis-service.md)   
 [Integration Services 서비스&#40;SSIS 서비스&#41;](service/integration-services-service-ssis-service.md)  
  
  
