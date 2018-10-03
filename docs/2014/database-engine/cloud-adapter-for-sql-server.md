---
title: SQL server 클라우드 어댑터 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Cloud adapter
- Deploy to Windows Azure
ms.assetid: 82ed0d0f-952d-4d49-aa36-3855a3ca9877
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90bc2c9f6f268bf03904d768fd25b25b3ade3fbc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157994"
---
# <a name="cloud-adapter-for-sql-server"></a>SQL Server에 대한 클라우드 어댑터
  클라우드 어댑터 서비스는 Windows Azure VM에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로비전의 일부로 만들어집니다. 클라우드 어댑터 서비스는 첫 번째 실행 중에 자체 서명된 SSL 인증서를 생성한 다음 **로컬 시스템** 계정으로 실행됩니다. 이 서비스는 자체적으로 구성하는 데 사용되는 구성 파일을 생성합니다. 또한 클라우드 어댑터는 기본 포트 11435에서 들어오는 TCP 연결을 허용하는 Windows Firewall 규칙도 만듭니다.  
  
 클라우드 어댑터는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 온-프레미스 인스턴스에서 메시지를 수신하는 상태 비저장 동기 서비스입니다. 클라우드 어댑터 서비스가 중지되면 원격 액세스 클라우드 어댑터가 중지되고 SSL 인증서가 바인딩 해제되며 Windows 방화벽 규칙이 사용되지 않습니다.  
  
## <a name="cloud-adapter-requirements"></a>클라우드 어댑터 요구 사항  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 클라우드 어댑터를 설치, 사용 및 실행하려면 다음 요구 사항을 따라야 합니다.  
  
-   클라우드 어댑터는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 이상에서 지원됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 대한 클라우드 어댑터를 사용하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012용 SQL Management Objects가 필요합니다.  
  
-   클라우드 어댑터 웹 서비스는 **로컬 시스템** 계정으로 실행되며 태스크를 실행하기 전에 클라이언트 자격 증명을 확인합니다. 클라이언트에서 제공한 자격 증명은 로컬의 멤버인 사용 계정에 속해야 **관리자** 원격 컴퓨터의 그룹입니다.  
  
-   클라우드 어댑터는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증만 지원합니다.  
  
-   클라우드 어댑터는 sa 계정이 아니라 VM 로컬 관리자 계정을 사용하여 로컬 컴퓨터에서 명령을 실행합니다.  
  
-   클라우드 어댑터는 TCP/IP를 수신 대기합니다. 기본 포트는 11435입니다.  
  
-   클라우드 어댑터는 Windows 방화벽 규칙을 만들고 수정할 수 있는 권한이 있어야 합니다.  
  
## <a name="cloud-adapter-configuration-settings"></a>클라우드 어댑터 구성 설정  
 다음 클라우드 어댑터 구성 세부 정보를 사용하여 클라우드 어댑터에 대한 설정을 수정합니다.  
  
-   **구성 파일에 대 한 기본 경로** – C:\Program Files\Microsoft SQL server\120\tools\cloudadapter \  
  
-   **구성 파일 매개 변수** -  
  
    -   \<구성 >  
  
        -   \<appSettings >  
  
            -   \<키 추가 = "WebServicePort" value = "" / >  
  
            -   \<키 추가 = "WebServiceCertificate" value = "GUID" / >  
  
            -   \<키 추가 = "ExposeExceptionDetails" value = "true" / >  
  
        -   \</appSettings >  
  
    -   \</configuration >  
  
-   **인증서 세부 정보** – 인증서의 값은 다음과 같습니다.  
  
    -   제목 – "CN = CloudAdapter\<VMName >, DC = SQL Server, DC = Microsoft"  
  
    -   인증서에는 서버 인증 EKU만 사용해야 합니다.  
  
    -   인증서 키 길이는 2048입니다.  
  
 **구성 파일 값**:  
  
|설정|값|Default|주석|  
|-------------|------------|-------------|--------------|  
|WebServicePort|1-65535|11435|지정되지 않은 경우 11435를 사용합니다.|  
|WebServiceCertificate|지문|비어 있음|비어 있는 경우 새로운 자체 서명된 인증서가 생성됩니다.|  
|ExposeExceptionDetails|True/False|False||  
  
## <a name="cloud-adapter-troubleshooting"></a>클라우드 어댑터 문제 해결  
 다음 정보를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 클라우드 어댑터의 문제를 해결할 수 있습니다.  
  
-   **오류 처리 및 로깅** - 오류 및 상태 메시지는 응용 프로그램 이벤트 로그에 기록됩니다.  
  
-   **추적, 이벤트** - 모든 이벤트는 응용 프로그램 이벤트 로그에 기록됩니다.  
  
-   **제어, 구성** –에 있는 구성 파일을 사용 하 여: C:\Program Files\Microsoft SQL Server\120\Tools\CloudAdapter\\합니다.  
  
|Error|오류 ID|원인|해결 방법|  
|-----------|--------------|-----------|----------------|  
|인증서를 인증서 저장소에 추가하는 동안 예외가 발생했습니다. {예외 텍스트}.|45560|컴퓨터 인증서 저장소 사용 권한|클라우드 어댑터 서비스가 인증서를 컴퓨터 인증서 저장소에 추가할 수 있는 권한이 있는지 확인하십시오.|  
|포트 {포트 번호} 및 인증서 {지문}에 대한 SSL 바인딩을 구성하려고 하는 동안 예외가 발생했습니다. {예외}.|45561|다른 응용 프로그램에서 포트를 이미 사용하고 있거나 인증서를 포트에 바인딩했습니다.|구성 파일에서 기존 바인딩을 제거하거나 클라우드 어댑터 포트를 변경합니다.|  
|인증서 저장소에서 SSL 인증서 [{지문}]를 찾지 못했습니다.|45564|인증서 지문은 구성 파일에 있지만 서비스에 대한 개인 인증서 저장소에는 인증서가 들어 있지 않습니다.<br /><br /> 사용 권한 부족|인증서가 서비스에 대한 개인 인증서 저장소에 있는지 확인합니다.<br /><br /> 서비스가 저장소에 대한 올바른 사용 권한이 있는지 확인합니다.|  
|웹 서비스를 시작하지 못했습니다. {예외 텍스트}.|45570|예외에서 설명됩니다.|ExposeExceptionDetails를 사용하고 예외에서 확장된 정보를 사용합니다.|  
|[{Thumbprint}] 인증서가 만료되었습니다.|45565|구성 파일에서 만료된 인증서가 참조되었습니다.|유효한 인증서를 추가하고 지문을 사용하여 구성 파일을 업데이트합니다.|  
|웹 서비스 오류: {0}합니다.|45571|예외에서 설명됩니다.|ExposeExceptionDetails를 사용하고 예외에서 확장된 정보를 사용합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft Azure 가상 머신에 SQL Server 데이터베이스 배포](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)  
  
  
