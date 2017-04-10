---
title: "웹 동기화를 위한 IIS 구성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "IIS 서버 구성 [SQL Server 복제]"
  - "websync.log"
  - "웹 동기화, IIS 서버"
ms.assetid: d651186e-c9ca-4864-a444-2cd6943b8e35
caps.latest.revision: 88
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 88
---
# 웹 동기화를 위한 IIS 구성
  이 항목의 절차는 병합 복제를 위해 웹 동기화를 구성하는 두 번째 단계입니다. 게시를 웹 동기화용으로 설정한 다음 이 단계를 수행합니다. 구성 프로세스에 대한 개요는 [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md). 이 항목의 절차를 완료한 다음에는 구독이 웹 동기화를 사용하도록 구성하는 세 번째 단계를 이어서 수행합니다. 세 번째 단계는 다음 항목에서 설명합니다.  
  
-   [! INCLUDE [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [How to: Configure a Subscription to Use Web Synchronization \(SQL Server Management Studio\)](http://msdn.microsoft.com/library/ms345214.aspx)  
  
-   복제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래밍: [하는 방법: 사용 하 여 웹 동기화 (Replication TRANSACT-SQL Programming)에 대 한 구독을 구성 합니다.](http://msdn.microsoft.com/library/ms345206.aspx)  
  
-   RMO: [하는 방법: 웹 동기화 (RMO 프로그래밍)를 사용 하 여 구독 구성](http://msdn.microsoft.com/library/ms345207.aspx)  
  
 웹 동기화는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS)를 실행하는 컴퓨터를 사용하여 끌어오기 구독을 병합 게시에 동기화합니다. IIS 버전 5.0, IIS 버전 6.0 및 [!INCLUDE[iisver](../../includes/iisver-md.md)] 이 지원됩니다. 웹 동기화 구성 마법사는 [!INCLUDE[iisver](../../includes/iisver-md.md)]에서 지원되지 않습니다.  
  
> [!IMPORTANT]  
>  응용 프로그램에서 [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] 이상 버전을 사용해야 하며, 이전 버전의 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 가 IIS 서버에 설치되어 있으면 안 됩니다. 이전 버전의 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 가 있으면 오류가 발생할 수 있습니다. 여기에는 다음이 포함됩니다. "웹 동기화 중 메시지 형식이 잘못되었습니다. 웹 서버에서 복제 구성 요소가 올바르게 구성되었는지 확인하십시오."  
  
> [!CAUTION]  
>  WebSync 및 대체 스냅숏 폴더 위치를 동시에 사용하지 마십시오.  
  
 웹 동기화를 사용하려면 다음 단계를 완료하여 IIS를 구성해야 합니다. 이 항목에서는 각 단계를 자세히 설명합니다.  
  
1.  SSL(Secure Sockets Layer)을 구성합니다. SSL은 IIS와 모든 구독자 간의 통신을 위해 필요합니다.  
  
2.  설치 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 IIS를 실행 하는 컴퓨터에서 연결 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사. 3단계에서 언급한 웹 동기화 구성 마법사를 사용하려면 IIS를 실행하는 컴퓨터에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 도 설치해야 합니다.  
  
3.  IIS를 실행하는 컴퓨터를 웹 동기화용으로 구성합니다. 컴퓨터를 수동으로 구성할 수 있지만 웹 동기화 구성 마법사를 사용하는 것이 좋습니다.  
  
    > [!NOTE]  
    >  IIS를 실행하는 컴퓨터에서 64비트 버전의 Windows를 실행 중인 경우 다음 명령을 실행하여 서버가 ISAPI(Internet Server API) 응용 프로그램을 실행하도록 적절하게 구성되었는지 확인해야 합니다. 자세한 내용은 IIS 설명서를 참조하십시오.  
  
    ```  
    cscript %SystemDrive%\inetpub\AdminScripts\adsutil.vbs set w3svc/AppPools/Enable32bitAppOnWin64 1  
    ```  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기에 대해 적절한 권한을 설정합니다.  
  
5.  진단 모드에서 웹 동기화를 실행하여 IIS를 실행하는 컴퓨터에 대한 연결을 테스트하고 SSL 인증서가 제대로 설치되었는지 확인합니다.  
  
## SSL(Secure Sockets Layer) 구성  
 SSL을 구성하려면 IIS를 실행하는 컴퓨터에서 사용할 인증서를 지정합니다. 병합 복제를 위한 웹 동기화에서는 서버 인증서를 사용할 수 있지만 클라이언트 인증서는 사용할 수 없습니다. 배포를 위해 IIS를 구성하려면 먼저 CA(인증 기관)에서 인증서를 얻어야 합니다. 인증 기관은 사용자, 컴퓨터 또는 다른 인증 기관에 속하는 공용 암호화 키의 신뢰성을 수립 및 보증하는 주체입니다. 인증서에 대한 자세한 내용은 IIS 설명서를 참조하십시오. 인증서를 설치한 다음에는 웹 동기화에서 사용하는 웹 사이트와 인증서를 연결해야 합니다.  
  
#### 배포를 위한 인증서를 지정하려면  
  
1.  IIS를 실행하는 컴퓨터에 관리자로 로그온합니다.  
  
2.  시작 **인터넷 정보 서비스 (IIS) 관리자**:  
  
    1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
    2.  **열기** 상자에 **inetmgr**을 입력한 다음 **확인**을 클릭합니다.  
  
3.  IIS 인증서 마법사를 실행합니다.  
  
    1.   **인터넷 정보 서비스 (IIS) 관리자**, 를 확장 하 고는 **로컬 컴퓨터** 노드를 확장 한 다음는 **웹 사이트** 폴더입니다.  
  
    2.  마우스 오른쪽 단추로 클릭 **기본 웹 사이트**, 를 클릭 하 고 **속성**합니다.  
  
    3.  **기본 웹 사이트 속성** 대화 상자의 **디렉터리 보안** 탭에서 **서버 인증서**를 클릭합니다.  
  
    4.  웹 서버 인증서 마법사를 완료합니다.  
  
4.  **확인**을 클릭합니다.  
  
 CA에서 서버 인증서를 얻을 수 없는 경우에는 테스트용 인증서를 지정할 수 있습니다. 테스트를 위해 IIS 6.0을 구성하려면 SelfSSL 유틸리티를 사용하여 인증서를 설치합니다. 이 유틸리티는 IIS 6.0 Resource Kit에서 사용할 수 있습니다. [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=30958)에서 도구를 다운로드할 수 있습니다. IIS 5.0의 경우 [Microsoft 도움말 및 지원](http://go.microsoft.com/fwlink/?LinkId=46229)을 방문하십시오.  
  
> [!NOTE]  
>  웹 사이트에서 SSL을 사용하려면 먼저 인증서를 웹 사이트에 연결해야 합니다. SelfSSL에서는 인증서를 자동으로 기본 웹 사이트에 연결합니다. 이미 인증서가 있거나 CA에서 나중에 인증서를 설치할 경우 해당 인증서를 웹 동기화에서 사용하는 웹 사이트에 명시적으로 연결해야 합니다. 구독 동기화에 사용되는 웹 사이트에는 인증서를 하나만 연결해야 합니다. 인증서를 여러 개 연결하는 경우 구독자는 사용 가능한 첫 번째 웹 사이트를 사용합니다.  
  
#### IIS 6.0에서 테스트를 위해 인증서를 지정하려면  
  
1.  IIS를 실행하는 컴퓨터에 관리자로 로그온합니다.  
  
2.  SelfSSL을 다운로드하고 설치합니다. 기본적으로 응용 프로그램을 설치 \<*드라이브*>: files\iis Resources\SelfSSL 합니다. 응용 프로그램 및 설명서 바로 가기에 복사 됩니다 \<*드라이브*>: \Documents and Settings\All Users\Start Menu\Programs\IIS Resources\SelfSSL 합니다.  
  
3.  SelfSSL을 실행합니다.  
  
    -   모든 매개 변수에 대해 기본값으로 SelfSSL을 실행하려면 이 응용 프로그램의 설치 디렉터리를 찾은 다음 SelfSSL.exe를 두 번 클릭합니다.  
  
        > [!NOTE]  
        >  기본적으로 SelfSSL에서 설치한 인증서는 7일 동안 유효합니다.  
  
    -   하나 이상의 매개 변수에 대한 값을 지정하려면 **시작**, **실행**을 차례로 클릭합니다. **열기** 상자에 **cmd**을 입력한 다음 **확인**을 클릭합니다. SelfSSL 설치 디렉터리를 찾고 `SelfSSL`을 입력한 다음 하나 이상의 매개 변수에 대해 값을 지정합니다. 매개 변수 목록을 보려면 `SelfSSL -?`를 입력합니다.  
  
## 연결 구성 요소 및 SQL Server Management Studio 설치  
  
#### SQL Server 연결 구성 요소 및 SQL Server Management Studio를 설치하려면  
  
1.  IIS를 실행하는 컴퓨터에 관리자로 로그온합니다.  
  
2.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 설치 디스크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 시작합니다. 이 마법사를 사용 하는 방법에 대 한 자세한 내용은 참조 [설치 마법사 및 #40;에서 SQL Server 2016 설치 설치 및 #41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)합니다.  
  
3.  **기능 선택** 페이지에서 **클라이언트 도구 연결**을 선택합니다.  
  
4.  웹 동기화 구성 마법사를 사용 하려는 경우 선택 **관리 도구-기본**합니다.  
  
5.  마법사를 완료한 다음 컴퓨터를 다시 시작합니다.  
  
    > [!NOTE]  
    >  추가 구성 요소를 설치할 수도 있지만 웹 동기화를 위해서는 연결 구성 요소만 필요합니다.  
  
## 웹 동기화 구성 마법사를 사용하여 IIS를 실행하는 컴퓨터 구성  
 웹 동기화 구성 마법사를 사용하거나 수동으로 IIS 서버를 구성합니다. 마법사를 사용하는 것이 좋지만 다음 섹션에서는 수동 구성 단계도 설명합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서 제공되는 웹 동기화 마법사는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]을 실행하는 게시자 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]로 업그레이드된 게시자에서 만들어진 게시에서만 사용할 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 게시에서는 이 마법사를 사용할 수 없습니다. 이 마법사는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전 및 [!INCLUDE[ssEWnoversion](../../includes/ssewnoversion-md.md)] 3.0 이상 버전의 구독에서 사용할 수 있습니다.  
  
 구성의 특징은 다음과 같습니다.  
  
-   IIS에서 기본 웹 사이트를 사용합니다. 그러나 다른 웹 사이트를 사용할 수도 있습니다. 웹 사이트를 만드는 방법은 IIS 설명서를 참조하십시오.  
  
    > [!NOTE]  
    >  사용자가 지정하는 웹 사이트를 통해 웹 동기화에서 사용하는 구성 요소에 액세스할 수 있지만 이 웹 사이트를 통해 다른 데이터나 웹 페이지에 액세스하려면 별도의 구성이 필요합니다.  
  
-   가상 디렉터리 및 관련 별칭을 만듭니다. 별칭은 웹 동기화 구성 요소에 액세스할 때 사용됩니다. 예를 들어 IIS 주소가 https://*server.domain.com* 와 'websync1'의 별칭 지정 하면 replisapi.dll 구성 요소에 액세스 하는 주소는 https://*server.domain.com*/websync1/replisapi.dll 합니다.  
  
-   기본 인증을 사용합니다. 기본 인증을 사용하면 Kerberos 위임 없이도 IIS와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자/배포자를 서로 다른 컴퓨터에서 실행(권장 구성)할 수 있으므로 기본 인증을 사용하는 것이 좋습니다. 기본 인증과 함께 SSL을 사용하면 로그인, 암호 및 모든 데이터가 전송 중에 암호화됩니다. 이때 사용하는 인증 유형에 관계없이 SSL이 필요합니다. 최상의 웹 동기화 방법은 [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md).  
  
#### 웹 동기화 구성 마법사를 사용하여 IIS를 실행하는 컴퓨터를 구성하려면  
  
1.  IIS를 실행하는 컴퓨터에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작합니다.  
  
2.  게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
3.  확장 된 **로컬 게시** 폴더에서 게시를 마우스 오른쪽 단추로 클릭 **웹 동기화 구성**합니다.  
  
4.  웹 동기화 구성 마법사의 **구독자 유형** 페이지에서 **SQL Server**를 선택합니다.  
  
5.  **웹 서버** 페이지에서 다음을 수행하십시오.  
  
    1.  구독을 동기화할 IIS 인스턴스를 선택합니다.  
  
    2.  **새 가상 디렉터리 만들기**를 선택합니다.  
  
    3.  페이지의 아래 창에서 IIS 인스턴스를 확장하고 **웹 사이트**를 확장한 다음 **기본 웹 사이트**를 클릭합니다.  
  
6.  **가상 디렉터리 정보** 페이지에서 다음을 수행하십시오.  
  
    1.  **별칭** 상자에 가상 디렉터리의 별칭을 입력합니다.  
  
    2.  **경로** 상자에 가상 디렉터리의 경로를 입력합니다. 예를 들어, 입력 한 경우 **websync1** 에 **별칭** 상자에 입력 합니다 **C:\Inetpub\wwwroot\websync1** 에 **경로** 상자입니다. **다음**을 클릭합니다.  
  
    3.  두 대화 상자에서 모두 **예**를 클릭합니다. 새 폴더가 생성되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ISAPI(Internet Server API) DLL이 복사됩니다. .  
  
7.  **인증된 액세스** 페이지에서 다음을 수행하십시오.  
  
    1.  **Windows 통합 인증** 및 **Windows 도메인 서버의 다이제스트 인증** 의 선택을 취소합니다.  
  
    2.  **기본 인증**을 선택합니다.  
  
    3.  **기본 도메인** 및 **영역** 상자에 IIS를 실행하는 컴퓨터의 도메인을 입력합니다.  
  
8.  **디렉터리 액세스** 페이지에서 다음을 수행하십시오.  
  
    1.  **추가**를 클릭한 다음 **사용자 또는 그룹 선택** 대화 상자에서 구독자가 IIS 연결에 사용할 계정을 추가합니다. 이러한 계정은 계정 지정 하는 것에 **웹 서버 정보** 에 대 한 값 또는 새 구독 마법사의 페이지는 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)*@internet_login* 매개 변수입니다.  
  
9. **스냅숏 공유 액세스** 페이지에서 스냅숏 공유를 입력합니다. 구독자가 스냅숏 파일에 액세스할 수 있도록 이 공유에는 적절한 사용 권한이 설정되어 있습니다. 공유에 대 한 사용 권한에 대 한 자세한 내용은 참조 [스냅숏 폴더 보안](../../relational-databases/replication/security/secure-the-snapshot-folder.md)합니다.  
  
10. **마법사 완료** 페이지에서 **마침**을 클릭합니다.  
  
     IIS를 실행하는 원격 컴퓨터를 구성하는 동안 네트워크 오류와 같은 오류가 발생하면 완료된 모든 동작이 롤백되고 남은 동작이 모두 취소됩니다. 완료된 동작을 롤백할 수 없으면 마법사의 마지막 페이지에 나타나는 상태는 **성공** 으로 표시되고 완료된 동작은 커밋된 상태로 유지됩니다.  
  
11. IIS를 실행하는 컴퓨터에서 64비트 버전의 Windows를 실행 중인 경우 replisapi.dll을 해당 디렉터리에 복사해야 합니다.  
  
    1.  **시작**을 클릭한 다음 **실행**을 클릭합니다. **열기** 상자에 **iisreset**을 입력한 다음 **확인**을 클릭합니다.  
  
    2.  IIS를 중지했다가 다시 시작한 다음 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\replisapi에 있는 replisapi.dll을 6b단계에서 지정한 디렉터리로 복사합니다.  
  
    3.  **시작**을 클릭한 다음 **실행**을 클릭합니다. **열기** 상자에 **cmd**을 입력한 다음 **확인**을 클릭합니다.  
  
    4.  6b단계에서 지정한 디렉터리에서 다음 명령을 실행합니다.  
  
         **regsvr32 replisapi.dll**  
  
## IIS를 실행하는 컴퓨터를 수동으로 구성  
 IIS를 실행하는 컴퓨터를 수동으로 구성하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기를 설치하고 구성한 다음 IIS에 연결할 구독자에 대해 권한을 구성해야 합니다.  
  
#### SQL Server 복제 수신기를 설치 및 구성하려면  
  
1.  IIS를 실행하는 컴퓨터에 replisapi.dll을 포함시킬 파일 디렉터리를 만듭니다. 원하는 있지만 디렉터리 아래에 만드는 것이 좋습니다 위치에 디렉터리를 만들 수는 \<*드라이브*>: \Inetpub 디렉터리입니다. 예를 들어, 디렉터리를 만들 \<*드라이브*>: \Inetpub\SQLReplication\\합니다.  
  
    > [!IMPORTANT]  
    >  이 디렉터리는 FAT 파일 시스템이 아닌 NTFS 파일 시스템 파티션에 만드는 것이 가장 좋습니다. NTFS 파일 시스템을 사용하면 NTFS 파일 시스템 권한을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제에 액세스할 수 있는 사용자를 정확하게 제어할 수 있습니다.  
  
2.  [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ 디렉터리에 있는 replisapi.dll을 1단계에서 만든 파일 디렉터리로 복사합니다.  
  
3.  replisapi.dll을 등록합니다.  
  
    1.  **시작**을 클릭한 다음 **실행**을 클릭합니다. **열기** 상자에 **cmd**을 입력한 다음 **확인**을 클릭합니다.  
  
    2.  1단계에서 만든 디렉터리에서 다음 명령을 실행합니다.  
  
         **regsvr32 replisapi.dll**  
  
4.  복제를 위한 새 웹 사이트를 만들거나 기존 사이트를 사용합니다. 이 웹 사이트는 동기화를 수행하는 동안 복제 구성 요소에서 액세스합니다. 웹 사이트를 만드는 방법은 IIS 설명서를 참조하십시오.  
  
5.  IIS에 가상 디렉터리를 만듭니다. 가상 디렉터리는 4단계에서 만든 웹 사이트 아래에 만들어야 하며 1단계에서 만든 디렉터리에 매핑해야 합니다. 가상 디렉터리를 만드는 방법은 IIS 설명서를 참조하십시오. 이 디렉터리에 대한 사용 권한은 가능한 제한적으로 할당하는 것이 좋습니다. **읽기** 및 **실행** 권한은 선택해야 하지만 **스크립트 실행**, **쓰기**및 **찾아보기** 권한은 선택하지 않아도 됩니다.  
  
6.  replisapi.dll이 실행될 수 있도록 IIS를 구성합니다. 이전 버전의 IIS에서는 4단계에서 할당한 사용 권한만으로도 충분하지만 IIS 버전 6.0에서는 ISAPI(Internet Server API) 확장을 사용해야 합니다. 자세한 내용은 IIS 6.0 설명서의 "ISAPI 확장 구성" 및 "동적 콘텐트 사용 설정 및 해제"를 참조하십시오.  
  
#### IIS 인증을 구성하려면  
  
-   구독자가 IIS에 연결한 다음 리소스 및 프로세스에 액세스하려면 먼저 IIS에서 해당 구독자를 인증해야 합니다. IIS는 익명, 기본 및 통합의 3가지 인증 유형을 제공합니다. 인증은 전체 웹 사이트나 사용자가 만든 가상 디렉터리에 적용할 수 있습니다.  
  
     기본 인증과 함께 SSL을 사용하는 것이 좋습니다. SSL은 사용하는 인증 유형에 관계없이 필요합니다. 인증을 구성하는 방법은 IIS 설명서를 참조하십시오.  
  
## SQL Server 복제 수신기에 대한 사용 권한 설정  
 구독자가 IIS를 실행하는 컴퓨터에 연결하면 IIS 구성 시 지정한 인증 유형을 사용하여 해당 구독자가 인증됩니다. IIS에서는 구독자를 인증한 다음 해당 구독자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제를 호출할 수 있는 권한이 있는지 여부를 확인합니다. replisapi.dll에 대한 권한을 설정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제를 호출할 수 있는 사용자를 제어합니다. Properly configuring permissions is necessary to prevent unauthorized access to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제에 무단으로 액세스하지 못하도록 하려면 사용 권한을 적절하게 구성해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기를 실행할 계정에 대해 최소 사용 권한을 구성하려면 다음 절차를 완료합니다. 이 절차의 단계는 IIS 6.0을 실행하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 에 해당됩니다.  
  
 다음 단계를 수행한 다음에는 PAL(게시 액세스 목록)에 필요한 로그인을 추가합니다. PAL에 대 한 자세한 내용은 참조 [게시자 보안 설정](../../relational-databases/replication/security/secure-the-publisher.md)합니다.  
  
#### 계정 및 사용 권한을 구성하려면  
  
1.  IIS를 실행하는 컴퓨터에 로컬 계정을 만듭니다.  
  
    1.  마우스 오른쪽 단추로 클릭 **내 컴퓨터**, 를 클릭 하 고 **관리**합니다.  
  
    2.  **컴퓨터 관리**에서 **로컬 사용자 및 그룹**을 확장합니다.  
  
    3.  마우스 오른쪽 단추로 클릭 **사용자**, 를 클릭 하 고 **새로운 사용자**합니다.  
  
    4.  사용자 이름과 강력한 암호를 입력합니다.  
  
    5.  **만들기**를 클릭한 다음 **닫기**를 클릭합니다.  
  
2.  IIS_WPG 그룹에 계정을 추가합니다.  
  
    1.  **컴퓨터 관리**에서 **로컬 사용자 및 그룹**을 확장한 다음 **그룹**을 클릭합니다.  
  
    2.  마우스 오른쪽 단추로 클릭 **IIS_WPG**, 를 클릭 하 고 **그룹에 추가**합니다.  
  
    3.  에 **IIS_WPG 속성** 대화 상자를 클릭 하 여 **추가**합니다.  
  
    4.  **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에 1단계에서 만든 계정을 추가합니다.  
  
    5.  **다음 위치에서** 필드에 도메인이 아닌 로컬 컴퓨터 이름이 표시되는지 확인합니다. 로컬 컴퓨터 이름이 아닌 경우 **위치**를 클릭합니다. **위치** 대화 상자에서 로컬 컴퓨터를 선택한 다음 **확인**을 클릭합니다.  
  
    6.  에 **사용자 선택** 대화 상자 및 **IIS_WPG 속성** 대화 상자를 클릭 하 여 **확인**합니다.  
  
3.  계정에 대한 replisapi.dll을 포함하는 폴더에 최소 사용 권한을 부여합니다.  
  
    1.  Replisapi.dll에 대해 만든 폴더를 찾아 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **공유 및 보안**합니다.  
  
    2.  **보안** 탭에서 **추가**를 클릭합니다.  
  
    3.  **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에 1단계에서 만든 계정을 추가합니다.  
  
    4.  **다음 위치에서** 필드에 도메인이 아닌 로컬 컴퓨터 이름이 표시되는지 확인합니다. 로컬 컴퓨터 이름이 아닌 경우 **위치**를 클릭합니다. **위치** 대화 상자에서 로컬 컴퓨터를 선택한 다음 **확인**을 클릭합니다.  
  
    5.  계정에만 부여 되 고 있는지 확인 **읽기**, **읽기 및 실행**, 및 **폴더 내용** 사용 권한입니다.  
  
    6.  디렉터리에 대한 액세스가 필요 없는 사용자나 그룹을 선택한 다음 **제거**를 클릭합니다.  
  
    7.  **확인**을 클릭합니다.  
  
4.  응용 프로그램 풀 만들기 **인터넷 정보 서비스 (IIS) 관리자**:  
  
    1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
    2.  **열기** 상자에 **inetmgr**을 입력한 다음 **확인**을 클릭합니다.  
  
    3.   **인터넷 정보 서비스 (IIS) 관리자**, 를 확장 하 고는 **로컬 컴퓨터** 노드.  
  
    4.  마우스 오른쪽 단추로 클릭 **응용 프로그램 풀**, 를 가리키도록 **새로** 클릭 하 고 **응용 프로그램 풀**합니다.  
  
    5.  **응용 프로그램 풀 ID** 필드에 풀 이름을 입력한 다음 **확인**을 클릭합니다.  
  
5.  계정과 응용 프로그램 풀을 연결합니다.  
  
    1.   **인터넷 정보 서비스 (IIS) 관리자**, 를 확장 하 고는 **로컬 컴퓨터** 노드를 확장 한 다음 **응용 프로그램 풀**합니다.  
  
    2.  작성 하 고 클릭 한 다음 응용 프로그램 풀을 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
    3.  에 **\< ApplicationPoolName> 속성** 대화 상자의 **Identity** 탭을 클릭 하 여 **구성할 수 있으며**합니다.  
  
    4.  **사용자 이름** 및 **암호** 필드에 1단계에서 만든 계정과 암호를 입력합니다.  
  
    5.  **확인**을 클릭합니다.  
  
6.  웹 동기화에 사용되는 가상 디렉터리와 응용 프로그램 풀을 연결합니다.  
  
    1.   **인터넷 정보 서비스 (IIS) 관리자**, 를 확장 하 고는 **로컬 컴퓨터** 노드를 확장 한 다음 **웹 사이트**합니다.  
  
    2.  웹 동기화에 사용 중인 웹 사이트를 확장 하 고 웹 동기화를 위해 만든 가상 디렉터리를 마우스 오른쪽 단추로 클릭 한 다음 **속성**합니다.  
  
    3.  에 **가상 디렉터리** 탭은 **\< VirtualDirectoryName> 속성** 대화 상자에서는 **응용 프로그램 풀** 드롭 다운 목록에서 5 단계에서 만든 응용 프로그램 풀을 선택 합니다.  
  
    4.  **확인**을 클릭합니다.  
  
## replisapi.dll에 대한 연결 테스트  
 진단 모드에서 웹 동기화를 실행하여 IIS를 실행하는 컴퓨터에 대한 연결을 테스트하고 SSL(Secure Sockets Layer) 인증서가 제대로 설치되었는지 확인합니다. 진단 모드에서 웹 동기화를 실행하려면 IIS가 실행되는 컴퓨터의 관리자여야 합니다.  
  
#### replisapi.dll에 대한 연결을 테스트하려면  
  
1.  구독자의 LAN(Local Area Network) 설정이 올바른지 확인합니다.  
  
    1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer의 **도구** 메뉴에서 **인터넷 옵션**을 클릭합니다.  
  
    2.  **연결** 탭에서 **LAN 설정**을 클릭합니다.  
  
    3.  LAN에 프록시 서버가 사용되지 않는 경우 **자동으로 설정 검색** 및 **사용자 LAN에 프록시 서버 사용**의 선택을 취소합니다.  
  
    4.  프록시 서버가 사용되는 경우 **사용자 LAN에 프록시 서버 사용** 및 **로컬 주소에 프록시 서버 사용 안 함**을 선택합니다.  
  
    5.  **확인**을 클릭합니다.  
  
2.  구독자에서는 Internet Explorer에서 replisapi.dll에 대한 주소에 `?diag` (예: https://server.domain.com/directory/replisapi.dll?diag)를 추가하여 진단 모드에서 서버에 연결합니다.  
  
3.  IIS에 대해 지정한 인증서를 Windows 운영 체제에서 인식하지 못할 경우 **보안 경고** 대화 상자가 나타납니다. 이 경고는 인증서가 테스트 인증서이거나 Windows에서 인식할 수 없는 CA(인증 기관)에서 발급한 인증서이기 때문에 발생할 수 있습니다.  
  
    > [!NOTE]  
    >  이 대화 상자가 나타나지 않으면 액세스하는 서버에 대한 인증서가 구독자의 인증서 저장소에 신뢰할 수 있는 인증서로 추가되었는지 확인합니다. 인증서를 내보내는 방법은 IIS 설명서를 참조하십시오.  
  
    1.  **보안 경고** 대화 상자에서 **인증서 보기**를 클릭합니다.  
  
    2.  **인증서** 대화 상자의 **일반** 탭에서 **인증서 설치**를 클릭합니다.  
  
    3.  기본값을 적용한 후 인증서 가져오기 마법사를 완료합니다.  
  
    4.  **보안 경고** 대화 상자에서 **예**를 클릭합니다.  
  
    5.  인증서 가져오기 마법사 확인 대화 상자에서 **확인**을 클릭합니다.  
  
    6.  **인증서** 대화 상자를 닫습니다.  
  
    7.  **보안 경고** 대화 상자에서 **예**를 클릭합니다.  
  
    > [!NOTE]  
    >  인증서는 사용자에 대해 설치되므로 IIS와 동기화할 각 사용자에 대해 이 프로세스를 수행해야 합니다.  
  
4.  에 **연결할 \< 서버 이름>** 대화 상자에서 로그인과는 병합 에이전트가 IIS에 연결 하는 데 사용할 암호를 지정 합니다. 이러한 자격 증명은 새 구독 마법사에서도 지정할 수 있습니다.  
  
5.  **SQL Websync 진단 정보**라는 Internet Explorer 창에서 페이지의 각 **상태** 열 값이 **SUCCESS**인지 확인합니다.  
  
6.  구독자에 인증서가 올바르게 설치되어 있는지 확인합니다.  
  
    1.  Internet Explorer를 닫았다가 다시 엽니다.  
  
    2.  진단 모드에서 서버에 연결합니다. 인증서가 제대로 설치된 경우 **보안 경고** 대화 상자가 나타나지 않습니다. 이 대화 상자가 나타나면 병합 에이전트가 IIS를 실행하는 컴퓨터에 연결할 수 없습니다. 액세스하는 서버에 대한 인증서가 구독자의 인증서 저장소에 신뢰할 수 있는 인증서로 추가되었는지 확인합니다. 인증서를 내보내는 방법은 IIS 설명서를 참조하십시오.  
  
## 참고 항목  
 [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md)  
  
  