---
title: "오프라인 로그 파일 보기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Log File Viewer, viewing offline logs
- offline log files
ms.assetid: 9223e474-f224-4907-a4f2-081e11db58f5
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e77911326a85724de1fbf901fe31f8d8f9cccca5
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="view-offline-log-files"></a>오프라인 로그 파일 보기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 대상 인스턴스가 오프라인이거나 시작할 수 없는 경우 로컬 또는 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일을 볼 수 있습니다.  
  
 등록된 서버에서 오프라인 로그 파일에 액세스하거나 WMI 및 WQL(WMI Query Language) 쿼리를 통해 프로그래밍 방식으로 액세스할 수 있습니다.  
  
> [!NOTE]  
>  이 방법을 사용하여 온라인 상태인 인스턴스에 연결할 수도 있지만 몇 가지 이유로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 통해서는 연결할 수 없습니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 오프라인 로그 파일에 연결하려면 오프라인 로그 파일을 보는 데 사용하는 컴퓨터와 보려는 로그 파일이 있는 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 설치해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 두 컴퓨터에 설치된 경우 각 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 및 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행하는 인스턴스의 오프라인 파일을 볼 수 있습니다.  
  
 등록된 서버를 사용하는 경우 연결할 인스턴스는 **로컬 서버 그룹** 또는 **중앙 관리 서버**에 등록되어야 합니다. 인스턴스는 자체적으로 등록될 수도 있고 서버 그룹의 멤버로 등록될 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록된 서버에 추가하는 방법은 다음 항목을 참조하십시오.  
  
-   [서버 그룹 만들기 또는 편집&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [연결된 서버 등록&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/register-a-connected-server-sql-server-management-studio.md)  
  
-   [중앙 관리 서버 및 서버 그룹 만들기&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)  
  
 WMI 및 WQL 쿼리를 통해 프로그래밍 방식으로 오프라인 로그 파일을 보는 방법은 다음 항목을 참조하십시오.  
  
-   [SqlErrorLogEvent 클래스](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md) (이 항목에서는 지정된 로그 파일에서 로깅된 이벤트의 값을 검색하는 방법을 보여 줍니다.)  
  
-   [SqlErrorLogFile 클래스](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md) (이 항목에서는 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그 파일에 대한 정보를 검색하는 방법을 보여 줍니다.)  
  
##  <a name="BeforeYouBegin"></a> 사용 권한  
 오프라인 로그 파일에 연결하려면 로컬 컴퓨터와 원격 컴퓨터 모두에서 다음과 같은 사용 권한이 있어야 합니다.  
  
-   **Root\Microsoft\SqlServer\ComputerManagement12** WMI 네임스페이스에 대한 읽기 권한. 기본적으로 모든 사용자는 계정 사용 권한으로 읽기 액세스합니다. 자세한 내용은 이 섹션 뒷부분의 "WMI 사용 권한을 확인하려면" 절차를 참조하십시오.  
  
-   오류 로그 파일을 포함하는 폴더에 대한 읽기 권한. 기본적으로 오류 로그 파일은 다음 경로에 있습니다. 여기서 \<*드라이브>*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치한 드라이브를 나타내고 \<*InstanceName*>은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 이름을 나타냅니다.  
  
     **\<드라이브>:\Program Files\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Log**  
  
 WMI 네임스페이스 보안 설정을 확인하려면 WMI 컨트롤 스냅인을 사용합니다.  
  
#### <a name="to-verify-wmi-permissions"></a>WMI 사용 권한을 확인하려면  
  
1.  WMI 컨트롤 스냅인을 엽니다. WMI 컨트롤 스냅인을 열려면 운영 체제에 따라 다음 중 하나를 수행합니다.  
  
    -   **시작**을 클릭하고 **검색 시작** 상자에 **wmimgmt.msc** 를 입력한 다음 ENTER 키를 누릅니다.  
  
    -   **시작**, **실행**을 차례로 클릭하고 **wmimgmt.msc**를 입력한 다음 ENTER 키를 누릅니다.  
  
2.  기본적으로 WMI 컨트롤 스냅인은 로컬 컴퓨터를 관리합니다.  
  
     원격 컴퓨터에 연결하려면 다음 단계를 수행합니다.  
  
    1.  **WMI 컨트롤(로컬)**을 마우스 오른쪽 단추로 클릭한 다음 **다른 컴퓨터에 연결**을 클릭합니다.  
  
    2.  **관리되는 컴퓨터 변경** 대화 상자에서 **다른 컴퓨터**를 클릭합니다.  
  
    3.  원격 컴퓨터 이름을 입력하고 **확인**을 클릭합니다.  
  
3.  **WMI 컨트롤(로컬)** 또는 **WMI 컨트롤(***RemoteComputerName***)**을 마우스 오른쪽 단추로 클릭한 다음, **속성**을 클릭합니다.  
  
4.  **WMI 컨트롤 속성** 대화 상자에서 **보안** 탭을 클릭합니다.  
  
5.  네임스페이스 트리에서 다음 네임스페이스를 찾아서 클릭합니다.  
  
     **Root\Microsoft\SqlServer\ComputerManagement10**  
  
6.  **보안**을 클릭합니다.  
  
7.  사용할 계정에 **계정 사용** 사용 권한이 있는지 확인합니다. 이 사용 권한이 있으면 WMI 개체에 대한 읽기 액세스가 가능합니다.  
  
### <a name="view-log-files"></a>로그 파일 보기  
 다음 절차에서는 등록된 서버를 통해 오프라인 로그 파일을 보는 방법을 보여 줍니다. 이 절차에서는 다음과 같은 사항을 가정합니다.  
  
 연결하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 이미 등록된 서버에 등록되어 있습니다.  
  
##### <a name="to-view-log-files-for-instances-that-are-offline"></a>오프라인 인스턴스의 로그 파일을 보려면  
  
1.  로컬 인스턴스의 오프라인 로그 파일을 보려면 승격된 권한으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 시작해야 합니다. 이렇게 하려면 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 시작할 때 **SQL Server Management Studio**를 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
3.  콘솔 트리에서 오프라인 파일을 보려는 인스턴스를 찾습니다.  
  
4.  다음 중 하나를 수행합니다.  
  
    -   인스턴스가 **로컬 서버 그룹**아래에 있으면 **로컬 서버 그룹**, 서버 그룹(인스턴스가 그룹의 멤버인 경우)을 차례로 확장하고 인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **SQL Server 로그 보기**를 클릭합니다.  
  
    -   인스턴스가 중앙 관리 서버 자체이면 **중앙 관리 서버**를 확장하고 인스턴스를 마우스 오른쪽 단추로 클릭하고 **중앙 관리 서버 동작**을 가리킨 다음 **SQL Server 로그 보기**를 클릭합니다.  
  
    -   인스턴스가 **중앙 관리 서버**아래에 있으면 **중앙 관리 서버**, 해당 중앙 관리 서버를 차례로 확장하고 인스턴스를 마우스 오른쪽 단추로 클릭한 다음(또는 서버 그룹을 확장하고 인스턴스를 마우스 오른쪽 단추로 클릭한 다음) **SQL Server 로그 보기**를 클릭합니다.  
  
5.  로컬 인스턴스에 연결하는 경우 현재 사용자 자격 증명을 사용하여 연결됩니다.  
  
     원격 인스턴스에 연결하는 경우 **로그 파일 뷰어 - 연결 계정** 대화 상자에서 다음 중 하나를 수행합니다.  
  
    -   현재 사용자로 연결하려면 **다른 사용자로 연결** 확인란의 선택을 지운 다음 **확인**을 클릭합니다.  
  
    -   다른 사용자로 연결하려면 **다른 사용자로 연결** 확인란을 선택한 다음 **사용자 설정**을 클릭합니다. 메시지가 표시되면 *domain_name*\\*user_name*형식의 사용자 이름이 포함된 사용자 자격 증명을 입력하고 **확인**을 클릭한 다음 다시 **확인** 을 클릭하여 연결합니다.  
  
    > [!NOTE]  
    >  로그 파일 로드 시간이 너무 긴 경우 로그 파일 뷰어 도구 모음에서 **중지** 를 클릭할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 파일 뷰어](../../relational-databases/logs/log-file-viewer.md)  
  
  
