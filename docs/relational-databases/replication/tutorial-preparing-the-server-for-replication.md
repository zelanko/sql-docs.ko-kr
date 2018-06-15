---
title: '자습서: 복제를 위한 SQL Server 준비 - 게시자, 배포자, 구독자 | Microsoft Docs'
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6b6651f84ac219330b2b236f3ee6537cc754b45c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32964728"
---
# <a name="tutorial-prepare-sql-server-for-replication-publisher-distributor-subscriber"></a>자습서: 복제를 위한 SQL Server 준비(게시자, 배포자, 구독자)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
복제 토폴로지를 구성하기 전에 보안을 계획해야 합니다. 이 자습서에서는 복제 토폴로지의 보안을 강화하는 방법에 대해 설명합니다. 또한 데이터를 복제하는 첫 번째 단계인 배포를 구성하는 방법도 보여 줍니다. 다른 자습서를 사용하기 전에 먼저 이 자습서를 완료해야 합니다.  
  
> [!NOTE]  
> 서버 간 데이터를 안전하게 복제하려면 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)의 모든 권장 사항을 구현해야 합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서에서는 최소의 권한을 사용하여 안전하게 복제를 실행할 수 있도록 서버를 준비하는 방법을 설명합니다.  

이 자습서에서는 다음 작업 방법을 배웁니다.
> [!div class="checklist"]
> * 복제용 Windows 계정을 만듭니다.
> * 스냅숏 폴더를 준비합니다.
> * 배포를 구성합니다.

## <a name="prerequisites"></a>사전 요구 사항
이 자습서는 기본적인 데이터베이스 작업에는 익숙하지만 복제에 대한 경험은 풍부하지 않은 사용자를 위한 것입니다. 

이 자습서를 완료하려면 SQL Server, SSMS(SQL Server Management Studio) 및 AdventureWorks 데이터베이스가 필요합니다.  
  
- 게시자 서버(원본)에서 설치합니다.  
  
   - SQL Server Express 또는 SQL Server Compact를 제외한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전. 이들 버전은 복제 게시자가 될 수 없습니다.   
   - [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 예제 데이터베이스. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다.  
  
- 구독자 서버(대상)에서 [!INCLUDE[ssEW](../../includes/ssew-md.md)]을 제외한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 버전을 설치합니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)]는 트랜잭션 복제에서 구독자가 될 수 없습니다.  
  
- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 다운로드합니다. SSMS에서 데이터베이스를 복원하는 방법에 대한 지침은 [데이터베이스 복원](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)을 참조하세요. 
    
>[!NOTE]
> - 두 버전이 넘게 차이 나는 SQL Server 인스턴스에서는 복제가 지원되지 않습니다. 자세한 내용은 [복제 토폴로지에서 지원되는 SQL Server 버전](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/)을 참조하세요.
> - [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 **sysadmin** 고정 서버 역할의 멤버인 로그인을 사용하여 게시자 및 구독자에 연결해야 합니다. 이 역할에 대한 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles)을 참조하세요.  


**이 자습서를 완료하는 데 소요되는 예상 시간: 30분**
  
## <a name="create-windows-accounts-for-replication"></a>복제용 Windows 계정 만들기
이 섹션에서는 복제 에이전트를 실행할 Windows 계정을 만듭니다. 다음 에이전트에 대해 로컬 서버에 별도의 Windows 계정을 만듭니다.  
  
|에이전트|위치|계정 이름|  
|---------|------------|----------------|  
|스냅숏 에이전트|게시자|<*machine_name*>\repl_snapshot|  
|로그 판독기 에이전트|게시자|<*machine_name*>\repl_logreader|  
|배포 에이전트|게시자 및 구독자|<*machine_name*>\repl_distribution|  
|병합 에이전트|게시자 및 구독자|<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> 복제 자습서에서는 게시자 및 배포자가 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스(NODE1\SQL2016)를 공유합니다. 구독자 인스턴스(NODE2\SQL2016)는 원격입니다. 게시자와 구독자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 같은 인스턴스를 공유할 수 있지만 반드시 이렇게 해야 하는 것은 아닙니다. 게시자와 구독자가 같은 인스턴스를 공유하는 경우 구독자에서는 계정을 만드는 단계를 수행하지 않아도 됩니다.  

### <a name="create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>게시자에서 복제 에이전트에 대한 로컬 Windows 계정 만들기
  
1. 게시자에서 제어판의 **관리 도구**에 있는 **컴퓨터 관리**를 엽니다.  
  
2. **시스템 도구**에서 **로컬 사용자 및 그룹**을 확장합니다.  
  
3. **사용자**를 마우스 오른쪽 단추로 클릭한 다음, **새 사용자**를 선택합니다.  
     
4. **사용자 이름** 상자에 **repl_snapshot**을 입력하고, 암호 및 다른 관련 정보를 입력한 다음, **만들기**를 선택하여 repl_snapshot 계정을 만듭니다. 

   ![“새 사용자” 대화 상자](media/tutorial-preparing-the-server-for-replication/newuser.png)
  
5. 이전 단계를 반복하여 repl_logreader, repl_distribution 및 repl_merge 계정을 만듭니다.  
 
   ![복제 사용자 목록](media/tutorial-preparing-the-server-for-replication/replusers.png)
  
6. **닫기**를 선택합니다.  
  
### <a name="create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>구독자에서 복제 에이전트에 대한 로컬 Windows 계정 만들기  
  
1. 구독자에서 제어판의 **관리 도구**에 있는 **컴퓨터 관리**를 엽니다.  
  
2. **시스템 도구**에서 **로컬 사용자 및 그룹**을 확장합니다.  
  
3. **사용자**를 마우스 오른쪽 단추로 클릭한 다음, **새 사용자**를 선택합니다.  
  
4. **사용자 이름** 상자에 **repl_distribution**을 입력하고, 암호 및 다른 관련 정보를 입력한 다음, **만들기**를 선택하여 repl_distribution 계정을 만듭니다.  
  
5. 이전 단계를 반복하여 repl_merge 계정을 만듭니다.  
  
6. **닫기**를 선택합니다.  

자세한 내용은 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)을 참조하세요.  

## <a name="prepare-the-snapshot-folder"></a>스냅숏 폴더 준비
이 섹션에서는 게시 스냅숏을 만들고 저장하는 데 사용되는 스냅숏 폴더를 구성합니다. 

### <a name="create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>스냅숏 폴더에 대한 공유 만들기 및 사용 권한 할당  
  
1. 파일 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 폴더로 이동합니다. 기본 위치는 C:\Program Files\Microsoft SQL Server\MSSQL.X\MSSQL\Data입니다.  
  
2. **repldata**라는 새 폴더를 만듭니다.  
  
3. 이 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
   1. **repldata 속성** 대화 상자의 **공유** 탭에서 **고급 공유**를 선택합니다.  
  
   2. **고급 공유** 대화 상자에서 **이 폴더 공유**를 선택한 다음, **권한**을 선택합니다.  

   ![Repldata 폴더를 공유하기 위한 선택 항목](media/tutorial-preparing-the-server-for-replication/repldata.png)

6. **repldata의 사용 권한** 대화 상자에서 **추가**를 선택합니다. **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 상자에서 이전에 만든 스냅숏 에이전트 계정 이름을 <*Publisher_Machine_Name>*>**\repl_snapshot**으로 입력합니다. **이름 확인**을 선택한 다음, **확인**을 선택합니다.  

   ![공유 권한 추가를 위한 선택 항목](media/tutorial-preparing-the-server-for-replication/addshareperms.png)

7. 6단계를 반복하여 이전에 생성된 다른 두 계정(<*Publisher_Machine_Name*>**\repl_merge** 및 <*Publisher_Machine_Name*>**\repl_distribution**)을 추가합니다.

8. 3개의 계정을 추가한 후에 다음과 같은 권한을 할당합니다.      
   - repl_distribution: **읽기**  
   - repl_merge: **읽기**  
   - repl_snapshot: **모든 권한**    

   ![각 계정에 대한 공유 권한](media/tutorial-preparing-the-server-for-replication/sharedpermissions.png)

9. 공유 권한이 올바르게 구성된 후 **확인**을 선택하여 **repldata의 사용 권한** 대화 상자를 닫습니다. **확인**을 선택하여 **고급 공유** 대화 상자를 닫습니다. 

10. **repldata 속성** 대화 상장에서 **보안** 탭 및 **편집**을 차례로 선택합니다.  

    ![“보안” 탭에서 “편집” 단추](media/tutorial-preparing-the-server-for-replication/editsecurity.png)   

11. **repldata의 사용 권한** 대화 상자에서 **추가**를 선택합니다. **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 상자에서 이전에 만든 스냅숏 에이전트 계정 이름을 <*Publisher_Machine_Name>*>**\repl_snapshot**으로 입력합니다. **이름 확인**을 선택한 다음, **확인**을 선택합니다.  

    ![보안 권한 추가를 위한 선택 항목](media/tutorial-preparing-the-server-for-replication/addsecuritypermissions.png)

  
12. 이전 단계를 반복하여 배포 에이전트에 대한 사용 권한을 <*Publisher_Machine_Name*>**\repl_distribution**으로, 병합 에이전트에 대한 사용 권한을 <*Publisher_Machine_Name*>**\repl_merge**로 추가합니다.  
    
  
13. 다음 사용 권한이 허용되는지 확인합니다.  
  
    - repl_distribution: **읽기**
    - repl_merge: **읽기**
    - repl_snapshot: **모든 권한**   
 
    ![복제 데이터에 대한 사용자 권한](media/tutorial-preparing-the-server-for-replication/replpermissions.png) 

14. **공유** 탭을 다시 선택하고 공유에 대한 **네트워크 경로**를 기록합니다. 이 경로는 나중에 스냅숏 폴더를 구성할 때 필요합니다.  

    !["공유" 탭에서 네트워크 경로](media/tutorial-replicating-data-between-continuously-connected-servers/networkpath.png)

15. **확인**을 선택하여 **repldata 속성** 대화 상자를 닫습니다. 
 
자세한 내용은 [스냅숏 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  

## <a name="configure-distribution"></a>배포 구성
이 섹션에서는 게시자에서 배포를 구성하고 게시 및 배포 데이터베이스에 대한 필수 사용 권한을 설정합니다. 배포자를 이미 구성한 경우 이 섹션을 시작하기 전에 게시와 배포를 해제해야 합니다. 특히 프로덕션에서 기존 복제 토폴로지를 유지해야 하는 경우에는 이 작업을 수행하지 마세요.   
  
원격 배포자를 사용한 게시자 구성은 이 자습서의 범위를 벗어납니다.  

### <a name="configure-distribution-at-the-publisher"></a>게시자에서 배포 구성  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음, 해당 서버 노드를 확장합니다.  
  
2. **복제** 폴더를 마우스 오른쪽 단추로 클릭하고 **배포 구성**을 선택합니다.  

   ![바로 가기 메뉴에서 "배포 구성" 명령](media/tutorial-preparing-the-server-for-replication/configuredistribution.png)
  
   > [!NOTE]  
   > 실제 서버 이름이 아니라 **localhost**를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 **localhost**에 연결할 수 없다는 경고 메시지가 표시됩니다. 경고 대화 상자에서 **확인**을 선택합니다. **서버에 연결** 대화 상자에서 **서버 이름** 을 **localhost**에서 실제 서버 이름으로 변경합니다. 그런 다음 **연결**을 선택합니다.  
  
   배포 구성 마법사가 시작됩니다.  
  
3. **배포자** 페이지에서 <*'ServerName'*> **을(를) 자체 배포자로 사용합니다. SQL Server에서 배포 데이터베이스와 로그를 만듭니다**를 선택합니다. 그런 후 **다음**을 선택합니다.  

   ![서버를 자체 배포자로 작동하게 하는 옵션](media/tutorial-preparing-the-server-for-replication/serverdistributor.png)
  
4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행되고 있지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **에이전트 시작** 페이지에서 **예를 선택하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 시작**되도록 구성합니다. **다음**을 선택합니다.  

     
5. **스냅숏 폴더** 상자에 \\\\<*Publisher_Machine_Name*>**\repldata** 경로를 입력한 후, **다음**을 선택합니다. 이 경로는 공유 속성을 구성한 후 repldata 속성 폴더의 **네트워크 경로**에서 이전의 본 것과 일치해야 합니다. 

   ![배포 구성 마법사 및 "repldata 속성" 대화 상자에서 네트워크 경로의 비교](media/tutorial-preparing-the-server-for-replication/repldatasnapshot.png)
  
6. 마법사의 나머지 페이지에 기본값을 적용합니다.  
    
   ![마법사의 마지막 페이지](media/tutorial-preparing-the-server-for-replication/distributionwizarddefaults.png)
  
7. **마침**을 선택하여 배포를 사용하도록 설정합니다. 

배포자를 구성할 때 이 오류가 발생할 수 있습니다. 이는 SQL Server 에이전트 계정을 시작하는 데 사용된 계정이 시스템 관리자가 아님을 나타냅니다. SQL Server 에이전트를 수동으로 시작하거나 기존 계정에 사용 권한을 부여하거나 SQL Server 에이전트가 사용하는 계정을 수정해야 합니다. 

![SQL Server 에이전트를 구성하기 위한 오류 메시지](media/tutorial-preparing-the-server-for-replication/startingagenterror.png)

SQL Server Management Studio 인스턴스를 관리자 권한으로 실행 중인 경우 SSMS 내에서 수동으로 SQL 에이전트를 시작할 수 있습니다.  
    
![SSMS의 에이전트에 대한 바로 가기 메뉴에서 "시작" 선택](media/tutorial-preparing-the-server-for-replication/ssmsstartagent.png) 

>[!NOTE]
> SQL 에이전트가 시각적으로 시작되지 않으면 SSMS에서 SQL Server 에이전트를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 클릭합니다. 여전히 중지 상태인 경우 SQL Server 구성 관리자에서 수동으로 시작합니다.    
  
### <a name="set-database-permissions-at-the-publisher"></a>게시자에서 데이터베이스 권한 설정  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **보안**을 확장하고, **로그인**을 마우스 오른쪽 단추로 클릭한 다음, **새 로그인**을 선택합니다.  

   ![바로 가기 메뉴에서 "새 로그인" 명령](media/tutorial-preparing-the-server-for-replication/newlogin.png)
  
2. **일반** 페이지에서 **검색**을 선택합니다. **선택할 개체 이름 입력** 상자에 <*Publisher_Machine_Name*>**\repl_snapshot**을 입력한 후, **이름 확인**을 선택한 다음, **확인**을 선택합니다.  

   ![개체 이름 입력을 위한 선택 항목](media/tutorial-preparing-the-server-for-replication/addsnapshotlogin.png)
  
3. **사용자 매핑** 페이지의 **이 로그인으로 매핑된 사용자** 목록에서 **배포** 및 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 둘 다 선택합니다.  
  
   데이터베이스 역할 멤버 자격 목록에서 두 데이터베이스의 로그인에 대해 **db_owner** 역할을 선택합니다.  

   ![데이터베이스와 해당 역할 선택](media/tutorial-preparing-the-server-for-replication/dbowner.png)
  
4. **확인**을 선택하여 로그인을 만듭니다.  
  
5. 1-4단계를 반복하여 다른 로컬 계정(repl_distribution, repl_logreader 및 repl_merge)에 대한 로그인을 만듭니다. 이러한 로그인은 **배포** 및 **AdventureWorks** 데이터베이스에서 **db_owner** 고정 데이터베이스 역할의 멤버인 사용자에게도 매핑되어야 합니다.  

   ![개체 탐색기에서 4개 계정 모두 보기](media/tutorial-preparing-the-server-for-replication/usersinssms.png)
  
  
참조 항목:
- [배포 구성](../../relational-databases/replication/configure-distribution.md) 
- [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)  

## <a name="next-steps"></a>다음 단계
이제 서버의 복제가 성공적으로 준비되었습니다. 다음 문서에서는 트랜잭션 복제를 구성하는 방법을 설명합니다. 

> [!div class="nextstepaction"]
> [자습서: 두 개의 완전히 연결된 서버 간 복제 구성(트랜잭션)](tutorial-replicating-data-between-continuously-connected-servers.md)

  
  
