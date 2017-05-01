---
title: "웹 동기화 구성 | Microsoft 문서"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL10.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
helpviewer_keywords:
- Web synchronization, security best practices
- Web synchronization, configuring
ms.assetid: 21f8e4d4-cd07-4856-98f0-9c9890ebbc82
caps.latest.revision: 74
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bc4b16adf509a811980323e2bc41e3f44c9906d9
ms.lasthandoff: 04/11/2017

---
# <a name="configure-web-synchronization"></a>웹 동기화 구성
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 병합 복제를 위한 웹 동기화 옵션을 사용하면 인터넷에서 HTTPS 프로토콜을 사용하여 데이터를 복제할 수 있습니다. 웹 동기화를 사용하려면 먼저 다음 구성 동작을 수행해야 합니다.  
  
1.  새 도메인 계정을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 매핑합니다.  
  
2.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS)를 실행하는 컴퓨터에서 구독을 동기화하도록 구성합니다.  
  
3.  병합 게시에서 웹 동기화를 사용하도록 구성합니다.  
  
4.  하나 이상의 구독에서 웹 동기화를 사용하도록 구성합니다.  
  
> [!NOTE]  
>  많은 양의 데이터를 복제하거나 **varchar(max)**등의 큰 데이터 형식을 사용하려는 경우 이 항목의 "많은 양의 데이터 복제" 섹션을 참조하십시오.  
  
 웹 동기화를 성공적으로 설정하려면 특정 요구 사항 및 정책에 맞게 보안을 구성하는 방법을 결정해야 합니다. IIS, 게시 및 구독을 구성하기 전에 이러한 의사 결정을 내리고 필요한 계정을 만드는 것이 가장 좋습니다.  
  
 이후의 절차에서는 간결한 설명을 위해 로컬 계정을 사용하는 간단한 보안 구성에 대해 설명합니다. 프로덕션 설치의 경우 사용자가 다중 서버 토폴로지를 사용할 가능성이 매우 높으며 또한 이렇게 하는 것이 권장되지만 IIS와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자 및 배포자가 모두 동일한 컴퓨터에서 실행되는 설치에는 이러한 간단한 구성이 적합합니다. 다음 절차에서 로컬 계정 대신 도메인 계정을 사용할 수 있습니다.  
  
## <a name="creating-new-accounts-and-mapping-sql-server-logins"></a>새 계정 만들기 및 SQL Server 로그인 매핑  
 복제 웹 사이트와 연결된 응용 프로그램 풀에 대해 지정된 계정을 가장하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기(replisapi.dll)가 게시자에 연결됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기에 사용되는 계정에는 [병합 에이전트 보안](../../relational-databases/replication/merge-agent-security.md)의 "게시자 또는 배포자에 연결" 섹션에 설명된 대로 사용 권한이 있어야 합니다. 요약하면, 계정은 다음 조건을 만족해야 합니다.  
  
-   PAL(게시 액세스 목록)의 멤버여야 합니다.  
  
-   게시 데이터베이스의 사용자와 연결된 로그인에 매핑되어야 합니다.  
  
-   배포 데이터베이스의 사용자와 연결된 로그인에 매핑되어야 합니다.  
  
-   스냅숏 공유에 대한 읽기 권한을 가지고 있어야 합니다.  
  
 처음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제를 사용하는 경우에는 복제 에이전트에 대한 계정 및 로그인도 만들어야 합니다. 자세한 내용은 이 항목의 "게시 구성" 및 "구독 구성" 섹션을 참조하십시오.  
  
 웹 동기화를 구성하기 전에 이 항목의 "웹 동기화에 대한 최상의 보안 방법" 섹션을 읽어 보는 것이 좋습니다. 웹 동기화 보안에 대한 자세한 내용은 [Security Architecture for Web Synchronization](../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)를 참조하십시오.  
  
## <a name="configuring-the-computer-that-is-running-iis"></a>IIS를 실행하는 컴퓨터 구성  
 웹 동기화를 수행하려면 IIS를 설치하고 구성해야 합니다. 게시에서 웹 동기화를 사용하도록 구성하려면 복제 웹 사이트에 대한 URL이 필요합니다.  
  
 웹 동기화는 IIS 버전 5.0부터 지원됩니다. 웹 동기화 구성 마법사는 IIS 버전 7.0에서 지원되지 않습니다. SQL Server 2012부터 IIS 서버의 웹 동기화 구성 요소를 사용하려면 사용자가 복제와 함께 SQL Server를 설치하는 것이 좋습니다. 무료 SQL Server Express Edition일 수 있습니다.  
  
 웹 동기화에 SSL이 필요합니다. 인증 기관에서 발급한 보안 인증서가 필요합니다. 테스트용으로만 자체 발급 보안 인증서를 사용할 수 있습니다.  
   
  
 **웹 동기화를 위해 IIS를 구성하려면**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configure IIS for Web Synchronization](../../relational-databases/replication/configure-iis-for-web-synchronization.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configure IIS 7 for Web Synchronization](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md)  
  
## <a name="creating-a-web-garden"></a>웹 가든 만들기  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기에서는 스레드당 두 개의 동기화 작업이 동시에 수행되도록 지원합니다. 이 제한을 초과하면 복제 수신기에서 응답을 중지할 수 있습니다. replisapi.dll에 할당된 스레드 수는 응용 프로그램 풀 최대 작업자 프로세스 수 속성에 의해 결정됩니다. 기본적으로 이 속성은 1로 설정됩니다.  
  
 최대 작업자 프로세스 수 속성 값을 늘려 CPU당 동시에 실행할 수 있는 동기화 작업 수를 더 늘릴 수 있습니다. CPU당 작업자 프로세스의 수를 늘려 확장하는 것을 "웹 가든"을 만드는 것이라고 합니다.  
  
 웹 가든 만들기를 통해 동시에 세 개 이상의 구독자를 동기화할 수 있습니다. 또한 replisapi.dll에 의한 CPU 사용률이 증가하는데 이로 인해 전체 서버 성능에 부정적인 영향을 끼칠 수 있습니다. 따라서 최대 작업자 프로세스 수의 값을 선택할 때에는 이러한 사항을 균형 있게 고려하는 것이 중요합니다.  
  
#### <a name="to-increase-maximum-worker-processes-in-iis-7"></a>IIS 7에서 최대 작업자 프로세스 수를 늘리려면  
  
1.  **인터넷 정보 서비스(IIS) 관리자**에서 로컬 서버 노드를 확장한 다음 **응용 프로그램 풀** 노드를 클릭합니다.  
  
2.  웹 동기화 사이트와 연결된 응용 프로그램 풀을 선택한 다음 **동작** 창에서 **고급 설정** 을 클릭합니다.  
  
3.  고급 설정 대화 상자의 **프로세스 모델** 머리글 아래에서 **최대 작업자 프로세스 수**라는 레이블이 지정된 행을 클릭합니다. 속성 값을 변경한 다음 **확인**을 클릭합니다.  
  
## <a name="configuring-the-publication"></a>게시 구성  
 웹 동기화를 사용하려면 표준 병합 토폴로지를 만드는 것과 같은 방법으로 게시를 만듭니다. 자세한 내용은 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)를 참조하세요.  
  
 게시가 생성되면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]또는 RMO(복제 관리 개체) 방법 중 하나를 사용하여 웹 동기화를 허용하는 옵션을 활성화합니다. 웹 동기화를 사용하도록 설정하려면 구독자 연결에 대한 웹 서버 주소를 제공해야 합니다.  
  
 게시자를 처음으로 사용하는 경우에는 배포자 및 스냅숏 공유도 구성해야 합니다. 각 구독자의 병합 에이전트에는 이 스냅숏 공유에 대한 읽기 권한이 있어야 합니다. 자세한 내용은 [배포 구성](../../relational-databases/replication/configure-distribution.md) 및 [스냅숏 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  
 **gen** 은 websync xml 파일의 예약어입니다. 이름이 **gen**인 열을 포함하는 테이블은 게시하지 마십시오.  
  
## <a name="configuring-the-subscription"></a>구독 구성  
 게시를 설정하고 IIS를 구성한 다음에는 끌어오기 구독을 만들고 이 구독에서 IIS를 사용하여 동기화를 수행하도록 지정합니다. 웹 동기화는 끌어오기 구독에 대해서만 지원됩니다.  
  
## <a name="upgrading-from-an-earlier-version-of-sql-server"></a>이전 버전의 SQL Server에서 업그레이드  
 기존 웹 동기화 토폴로지를 구성한 상태에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하는 경우 웹 동기화에 사용되는 가상 디렉터리에 최신 버전의 Replisapi.dll이 복사되어 있는지 확인해야 합니다. 기본적으로 최신 버전의 Replisapi.dll은 C:\Program Files\Microsoft SQL Server\\<nnn\>\COM에 있습니다.  
  
## <a name="replicating-large-volumes-of-data"></a>많은 양의 데이터 복제  
 구독자 컴퓨터에서 메모리 문제가 발생하지 않도록 웹 동기화에서 변경 내용을 전송하는 데 사용되는 XML 파일에 대해 기본 최대 크기인 100MB를 사용합니다. 다음 레지스트리 키를 설정하여 제한을 늘릴 수 있습니다.  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\Replication**  
  
 **WebSyncMaxXmlSize DWORD 2000000**  
  
 이러한 키에 허용되는 값 범위는 100MB ~ 4GB입니다. 값이 KB로 지정됩니다. 이 매개 변수를 높은 값으로 설정해도 사용자가 해당 양의 데이터를 동기화할 수 있다고 보장하지는 않습니다. 유효 제한은 구독자 컴퓨터에서 사용할 수 있는 연속적인 메모리 양에 따라 달라집니다. 100MB보다 큰 값이 필요한 경우 값을 증분식으로 늘리고 구독자에서의 일반적인 작업을 수행하는 데 필요한 메모리 사용을 테스트하는 것이 좋습니다.  
  
 XML 파일의 최대 크기는 4GB이지만 복제를 수행하면 일괄 처리에 있는 해당 파일의 변경 내용이 동기화됩니다. 데이터 및 메타데이터의 최대 일괄 처리 크기는 25MB입니다. 각 일괄 처리의 데이터가 20MB를 초과하지 않도록 해야 메타데이터 및 기타 오버헤드를 위한 공간이 확보됩니다. 이러한 제한이 의미하는 바는 다음과 같습니다.  
  
-   데이터와 메타데이터가 25MB를 초과하도록 하는 열은 복제할 수 없습니다. 이는 **varchar(max)**등의 큰 데이터 형식이 포함된 행을 복제하는 경우 문제가 될 수 있습니다.  
  
-   많은 양의 데이터를 복제하는 경우 병합 에이전트 일괄 처리 크기를 조정해야 합니다.  
  
 병합 복제를 위한 일괄 처리 크기는 아티클 단위의 변경 내용 컬렉션인 *세대*로 측정됩니다. 일괄 처리에 포함되는 세대의 수는 병합 에이전트의 -**DownloadGenerationsPerBatch** 및 -**UploadGenerationsPerBatch** 매개 변수를 사용하여 지정됩니다. 자세한 내용은 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)을(를) 참조하세요.  
  
 데이터의 양이 많은 경우 각 일괄 처리 매개 변수에 작은 수를 지정하십시오. 10부터 시작한 다음 응용 프로그램 요구 사항과 성능에 따라 조정하는 것이 좋습니다. 일반적으로 이러한 매개 변수는 에이전트 프로필에 지정됩니다. 프로필에 대한 자세한 내용은 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하십시오.  
  
## <a name="security-best-practices-for-web-synchronization"></a>웹 동기화에 대한 최상의 보안 방법  
 웹 동기화의 보안 관련 설정은 다양하게 지정할 수 있습니다. 다음 방법을 사용하는 것이 좋습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자 및 게시자는 동일한 컴퓨터에 있을 수 있습니다. 이러한 설정은 병합 복제에 일반적입니다. 그러나 IIS는 서로 다른 컴퓨터에 설치되어 있어야 합니다.  
  
-   SSL(Secure Sockets Layer)을 사용하여 IIS를 실행하는 컴퓨터와 구독자 간의 연결을 암호화합니다. 이 작업은 웹 동기화에 필요합니다.  
  
-   구독자에서 IIS로 연결할 때 기본 인증을 사용합니다. 기본 인증을 사용하면 IIS가 위임 없이 구독자를 대신하여 게시자/배포자에 연결할 수 있습니다. 통합 인증을 사용하는 경우에는 위임이 필요합니다.  
  
    > [!NOTE]  
    >  기본 인증은 IIS로 자격 증명을 전달하는 방법입니다. 기본 인증은 IIS에 대해 설정한 연결에 Windows 도메인 계정을 지정하는 작업을 방지하지 않습니다.  
  
-   Windows 도메인 계정으로 스냅숏 에이전트를 실행 및 연결하도록 지정합니다. 이것이 기본 구성입니다. 구독자 컴퓨터를 사용하는 사용자의 도메인 계정으로 각 병합 에이전트를 실행 및 연결하도록 지정합니다.  
  
     에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
-   새 구독 마법사의 **웹 서버 정보** 페이지에서 계정과 암호를 지정할 때 또는 **@internet_url** 및 **@internet_login** 및 [@internet_login](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)를 참조하십시오. 이 계정에는 스냅숏 공유에 대한 읽기 권한이 있어야 합니다.  
  
-   각 게시는 IIS에 대해 서로 다른 가상 디렉터리를 사용해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기(Replisapi.dll)를 실행하는 계정은 동기화하는 동안 게시자 및 배포자에 연결되는 계정이기도 합니다. 계정은 게시자 및 배포자의 SQL 로그인 계정에 매핑되어야 합니다. 자세한 내용은 [웹 동기화를 위한 IIS 구성](../../relational-databases/replication/configure-iis-for-web-synchronization.md)에서 "SQL Server 복제 수신기에 대한 사용 권한 설정" 섹션을 참조하세요.  
  
-   FTP를 사용하여 게시자에 있는 스냅숏을 IIS를 실행하는 컴퓨터로 배달할 수 있습니다. 스냅숏은 항상 IIS를 실행하는 컴퓨터에서 HTTPS를 사용하여 구독자로 배달됩니다. 자세한 내용은 [FTP를 통해 스냅숏 전송](../../relational-databases/replication/transfer-snapshots-through-ftp.md)을 참조하세요.  
  
-   복제 토폴로지에 있는 서버에 방화벽이 설정되어 있는 경우 웹 동기화를 사용하기 위해 방화벽에서 포트를 열어야 할 수 있습니다.  
  
    -   구독자 컴퓨터는 SSL을 사용하는 HTTPS(일반적으로 포트 443을 사용하도록 구성)를 통해 IIS를 실행하는 컴퓨터에 연결합니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자는 HTTP(일반적으로 포트 80을 사용하도록 구성)를 통해 연결할 수도 있습니다.  
  
    -   IIS를 실행하는 컴퓨터는 일반적으로 포트 1433(기본 인스턴스)을 사용하여 게시자나 배포자에 연결합니다. 다른 기본 인스턴스가 있는 서버에서 게시자나 배포자가 명명된 인스턴스인 경우 일반적으로 포트 1500을 사용하여 명명된 인스턴스에 연결합니다.  
  
    -   IIS를 실행하는 컴퓨터가 방화벽에 의해 배포자와 분리되고 스냅숏 전달에 FTP 공유가 사용되는 경우 FTP에 사용되는 포트를 열어야 합니다. 자세한 내용은 [FTP를 통해 스냅숏 전송](../../relational-databases/replication/transfer-snapshots-through-ftp.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  방화벽의 포트를 열면 서버가 악의적인 공격에 노출될 수 있습니다. 포트를 열기 전에 방화벽 시스템을 잘 이해해야 합니다. 자세한 내용은 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [병합 복제에 대한 웹 동기화](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  

