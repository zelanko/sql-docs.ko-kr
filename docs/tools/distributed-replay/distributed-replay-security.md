---
title: Distributed Replay 보안 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 7e2e586d-947d-4fe2-86c5-f06200ebf139
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6279a9ff5dd965a1ca2920c13c993bf364736355
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079855"
---
# <a name="distributed-replay-security"></a>Distributed Replay 보안
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 기능을 설치 및 사용하기 전에 이 항목에 나오는 중요 보안 정보를 검토해야 합니다. 이 항목에서는 Distributed Replay를 사용하기 전에 수행해야 하는 설치 후 보안 구성 단계에 대해 설명합니다. 또한 데이터 보호 및 중요한 제거 단계와 관련하여 고려해야 할 주요 사항도 설명합니다.  
  
## <a name="user-and-service-accounts"></a>사용자 및 서비스 계정  
 다음 표에서는 Distributed Replay에 사용되는 계정에 대해 설명합니다. Distributed Replay를 설치한 후 컨트롤러 및 클라이언트 서비스 계정이 실행될 보안 주체를 할당해야 합니다. 따라서 Distributed Replay 기능을 설치하기 전에 해당 도메인 사용자 계정을 구성하는 것이 좋습니다.  
  
|사용자 계정|요구 사항|  
|------------------|------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 서비스 계정|도메인 사용자 계정 또는 로컬 사용자 계정일 수 있습니다. 로컬 사용자 계정을 사용하려면 관리 도구, 컨트롤러 및 클라이언트가 모두 동일한 컴퓨터에서 실행되고 있어야 합니다.<br /><br /> **\*\* 보안 정보 \*\*** Windows의 로컬 관리자 그룹 멤버가 아닌 계정을 사용하는 것이 좋습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 서비스 계정|도메인 사용자 계정 또는 로컬 사용자 계정일 수 있습니다. 로컬 사용자 계정을 사용하려면 컨트롤러, 클라이언트 및 대상 SQL Server가 모두 동일한 컴퓨터에서 실행되고 있어야 합니다.<br /><br /> **\*\* 보안 정보 \*\*** Windows의 로컬 관리자 그룹 멤버가 아닌 계정을 사용하는 것이 좋습니다.|  
|Distributed Replay Administration Tool을 실행하는 데 사용되는 대화형 사용자 계정|로컬 사용자 계정 또는 도메인 사용자 계정일 수 있습니다. 로컬 사용자 계정을 사용하려면 관리 도구와 컨트롤러가 동일한 컴퓨터에서 실행되고 있어야 합니다.|  
  
 **중요**: Distributed Replay Controller를 구성할 때 Distributed Replay Client 서비스를 실행하는 데 사용할 사용자 계정을 하나 이상 지정할 수 있습니다. 다음은 지원되는 계정 목록입니다.  
  
-   도메인 사용자 계정  
  
-   사용자가 만든 로컬 사용자 계정  
  
-   관리자  
  
-   가상 계정 및 MSA(관리 서비스 계정)  
  
-   Network Services, 로컬 서비스 및 시스템  
  
 그룹 계정(로컬 또는 도메인) 및 다른 기본 제공 계정(예: Everyone)은 사용할 수 없습니다.  
  
 Distributed Replay를 설치한 후 서비스 계정이나 해당 암호를 설정하려면 Windows 서비스 도구를 사용하면 됩니다. Distributed Replay Controller 또는 Distributed Replay Client 서비스와 연결된 서비스 계정을 변경하려면 다음 단계를 따르십시오.  
  
1.  운영 체제에 따라 다음 중 하나를 수행합니다.  
  
    -   **시작**을 클릭하고 **검색** 상자에 **services.msc** 를 입력한 다음 Enter 키를 누릅니다.  
  
    -   **시작**, **실행**을 차례로 클릭하고 **services.msc**를 입력한 다음 Enter 키를 누릅니다.  
  
2.  **서비스** 대화 상자에서 구성할 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **계정 지정**을 클릭합니다.  
  
4.  사용할 사용자 계정을 구성합니다.  
  
## <a name="file-and-folder-permissions"></a>파일 및 폴더 권한  
 서비스 계정을 지정한 후에는 해당 서비스 계정에 필요한 파일 및 폴더 사용 권한을 부여해야 합니다. 다음 표에 따라 파일 및 폴더 사용 권한을 구성합니다.  
  
|계정|폴더 권한|  
|-------------|------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 서비스 계정|`<Controller_Installation_Path>\DReplayController` (읽기, 쓰기, 삭제)<br /><br /> `DReplayServer.xml` 파일(읽기, 쓰기)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 서비스 계정|`<Client_Installation_Path>\DReplayClient` (읽기, 쓰기, 삭제)<br /><br /> `DReplayClient.xml` 파일(읽기, 쓰기)<br /><br /> 클라이언트 구성 파일의 `WorkingDirectory` 및 `ResultDirectory` 요소에 각각 지정된 작업 디렉터리 및 결과 디렉터리(읽기, 쓰기)|  
  
## <a name="dcom-permissions"></a>DCOM 권한  
 DCOM은 컨트롤러와 관리 도구 간 및 컨트롤러와 모든 클라이언트 간 RPC(원격 프로시저 호출) 통신에 사용됩니다. Distributed Replay 기능을 설치한 후 컴퓨터 차원에서 그리고 애플리케이션별로 컨트롤러에 대한 DCOM 권한을 구성해야 합니다.  
  
 컨트롤러 DCOM 권한을 구성하려면 다음 단계에 따르십시오.  
  
1.  **구성 요소 서비스 스냅인 dcomcnfg.exe 열기**: 이 도구는 DCOM 권한을 구성하는 데 사용됩니다.  
  
    1.  컨트롤러 컴퓨터에서 **시작**을 클릭합니다.  
  
    2.  **검색** 상자에 **dcomcnfg.exe** 를 입력합니다.  
  
    3.  Enter 키를 누릅니다.  
  
2.  **컴퓨터 전체 DCOM 권한 구성**: 다음 표에 나열된 각 계정에 대해 해당하는 컴퓨터 전체 DCOM 권한을 부여합니다. 컴퓨터 전체 권한을 설정하는 방법은 [검사 목록: DCOM 애플리케이션 관리](https://go.microsoft.com/fwlink/?LinkId=185842)를 참조하세요.  
  
3.  **애플리케이션별 DCOM 권한 구성**: 다음 표에 나열된 각 계정에 대해 해당하는 애플리케이션별 DCOM 권한을 부여합니다. 컨트롤러 서비스에 대한 DCOM 애플리케이션 이름은 **DReplayController**입니다. 애플리케이션별 권한을 설정하는 방법은 [검사 목록: DCOM 애플리케이션 관리](https://go.microsoft.com/fwlink/?LinkId=185842)를 참조하세요.  
  
 다음 표에서는 관리 도구를 실행하는 데 사용되는 대화형 사용자 계정과 클라이언트 서비스 계정에 필요한 DCOM 권한에 대해 설명합니다.  
  
|기능|계정|컨트롤러에 필요한 DCOM 권한|  
|-------------|-------------|---------------------------------------------|  
|Distributed Replay Administration Tool|대화형 사용자 계정|로컬 액세스<br /><br /> 원격 액세스<br /><br /> 로컬 시작<br /><br /> 원격 시작<br /><br /> 로컬 활성화<br /><br /> 원격 활성화|  
|Distributed Replay Client|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 서비스 계정|로컬 액세스<br /><br /> 원격 액세스<br /><br /> 로컬 시작<br /><br /> 원격 시작<br /><br /> 로컬 활성화<br /><br /> 원격 활성화|  
  
> [!IMPORTANT]  
>  악의적인 쿼리나 서비스 거부 공격으로부터 보호하려면 신뢰할 수 있는 사용자 계정만 클라이언트 서비스 계정으로 사용해야 합니다. 이 계정은 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결하여 작업을 재생할 수 있습니다.  
  
## <a name="sql-server-permissions"></a>SQL Server 사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 서비스 계정은 작업의 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결하는 데 사용됩니다. 이러한 연결에는 Windows 인증 모드만 지원됩니다.  
  
 일련의 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 서비스를 설치한 후 추적 작업을 재생할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 sysadmin 서버 역할을 해당 서비스 계정에 사용되는 보안 주체에 부여해야 합니다. 이 단계는 Distributed Replay 설치 중 자동으로 수행되지 않습니다.  
  
## <a name="data-protection"></a>데이터 보호  
 Distributed Replay 환경에서 다음 사용자 계정에는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]서버 인스턴스, 입력 추적 데이터 및 결과 추적 파일에 대한 모든 액세스 권한이 부여됩니다.  
  
-   관리 도구를 실행하는 데 사용되는 대화형 사용자 계정  
  
-   컨트롤러 서비스 계정  
  
-   클라이언트 서비스 계정  
  
-   컨트롤러의 로컬 Administrators 그룹 멤버  
  
-   클라이언트의 로컬 Administrators 그룹 멤버  
  
    > [!IMPORTANT]  
    >  이러한 계정은 Distributed Replay에 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일, 추적 파일, 중간 파일 또는 디스패치 파일에 포함된 PII(개인 식별이 가능한 정보)나 중요한 정보에 대한 모든 액세스 권한을 가집니다.  
  
 다음 보안 예방 조치를 수행하는 것이 좋습니다.  
  
-   입력 추적 데이터, 출력 추적 결과 및 데이터베이스 파일을 NTFS 파일 시스템(NTFS)을 사용하는 위치에 저장하고 적절한 ACL(액세스 제어 목록)을 적용합니다. 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 저장되는 데이터를 암호화합니다. ACL은 추적 파일에 적용되지 않으며 데이터 마스킹 또는 난독 처리되지 않습니다. 이러한 파일은 사용 후 신속하게 삭제해야 합니다.  
  
-   Distributed Replay에서 생성하는 모든 중간 파일과 디스패치 파일에 적절한 ACL 및 보존 정책을 적용합니다.  
  
-   SSL(Secure Sockets Layer)을 사용하여 네트워크 전송에 대해 보안을 설정합니다.  
  
## <a name="important-removal-steps"></a>중요한 제거 단계  
 테스트 환경에서만 Distributed Replay를 사용하는 것이 좋습니다. 테스트를 완료한 후 다른 태스크를 위해 해당 컴퓨터를 프로비전하기 전에 다음 작업을 수행하십시오.  
  
-   Distributed Replay 기능을 제거하고 관련 구성 파일을 컨트롤러 및 모든 클라이언트에서 제거합니다.  
  
-   테스트에 사용된 추적 파일, 중간 파일, 디스패치 파일 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일을 모두 삭제합니다. 중간 파일 및 디스패치 파일은 각각 컨트롤러와 클라이언트의 작업 디렉터리에 저장됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Distributed Replay 설치 - 개요](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
  
