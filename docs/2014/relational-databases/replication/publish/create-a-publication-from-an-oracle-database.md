---
title: Oracle 데이터베이스에서 게시 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], Oracle databases
- Oracle publishing [SQL Server replication], configuring
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 61f7e509b715b1156b06362f8e9bcd4a634de0c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63020862"
---
# <a name="create-a-publication-from-an-oracle-database"></a>Oracle 데이터베이스에서 게시 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]의 Oracle 데이터베이스에서 구독을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
-   **다음을 사용하여 Oracle 데이터베이스에서 게시를 만들려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   게시를 만들기 전에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에 Oracle 소프트웨어를 설치하고 Oracle 데이터베이스를 구성해야 합니다. 자세한 내용은 [Oracle 게시자 구성](../non-sql/configure-an-oracle-publisher.md)을 참조하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사를 사용하여 Oracle 데이터베이스에서 스냅샷 또는 트랜잭션 게시를 만듭니다.  
  
 처음으로 Oracle 데이터베이스에서 게시를 만들 때는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 Oracle 게시자를 식별해야 합니다. 같은 데이터베이스의 후속 게시에 대해서는 이 작업을 수행할 필요가 없습니다. 새 게시 마법사나 **배포자 속성 - \<배포자>** 대화 상자에서 Oracle 게시자를 식별할 수 있습니다. 이 항목에서는 **배포자 속성 - \<배포자>** 대화 상자를 보여 줍니다.  
  
#### <a name="to-identify-the-oracle-publisher-at-the-sql-server-distributor"></a>SQL Server 배포자에서 Oracle 게시자를 식별하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 Oracle 게시자가 배포자로 사용할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **배포자 속성**을 클릭합니다.  
  
3.  **배포자 속성 - \<배포자>** 대화 상자의 **게시자** 페이지에서 **추가**를 클릭하고 **Oracle 게시자 추가**를 클릭합니다.  
  
4.  **서버에 연결** 대화 상자에서 **옵션** 단추를 클릭합니다.  
  
5.  **로그인** 탭에서 다음을 수행하세요.  
  
    1.  Oracle 데이터베이스 인스턴스 이름을 입력하거나 **서버 인스턴스** 콤보 상자에서 **더 찾아보기** 를 선택합니다.  
  
    2.  **Oracle 표준 인증** (권장) 또는 **Windows 인증**을 선택합니다.  
  
         **Windows 인증**을 선택하면 Windows 자격 증명을 사용한 연결을 허용하도록 Oracle 서버를 구성해야 하며(자세한 내용은 Oracle 설명서 참조), 복제 관리 사용자 스키마에 대해 지정한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 계정과 동일한 계정으로 로그인해야 합니다.  
  
    3.  **Oracle 표준 인증**을 선택하는 경우에는 구성하는 동안 Oracle 게시자에 만든 복제 관리 사용자 스키마의 로그인 및 암호를 입력합니다.  
  
6.  **연결 속성** 탭에서 게시자 유형으로 **게이트웨이** 또는 **전체**를 선택합니다.  
  
     **전체** 옵션은 Oracle 게시에 대해 지원되는 완전한 기능 집합을 스냅샷 및 트랜잭션 게시에 제공하도록 디자인되었습니다. **게이트웨이** 옵션은 복제가 시스템 간의 게이트웨이로 사용되는 경우 성능을 향상시킬 수 있도록 특정 디자인 최적화를 제공합니다. 동일한 테이블을 여러 트랜잭션 게시에 게시하려는 경우에는 **게이트웨이** 옵션을 사용할 수 없습니다. **게이트웨이**를 선택하면 트랜잭션 게시의 경우 특정 테이블이 한 번만 나타날 수 있지만 스냅샷 게시의 경우에는 이러한 제한이 없습니다.  
  
7.  **연결**을 클릭하면 Oracle 게시자에 연결되고 이 게시자가 복제용으로 구성됩니다. **서버에 연결** 대화 상자가 닫히고 **배포자 속성 - \<배포자>** 대화 상자로 돌아갑니다.  
  
    > [!NOTE]  
    >  네트워크 구성에 문제가 있는 경우 이 시점에 오류가 표시됩니다. Oracle 데이터베이스 연결에 문제가 있으면 [Troubleshooting Oracle Publishers](../non-sql/troubleshooting-oracle-publishers.md)의 "SQL Server 배포자가 Oracle 데이터베이스 인스턴스에 연결할 수 없습니다" 섹션을 참조하세요.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-create-a-publication-from-an-oracle-database"></a>Oracle 데이터베이스에서 게시를 만들려면  
  
1.  Oracle 게시자가 배포자로 사용할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장합니다.  
  
3.  **로컬 게시** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 Oracle 게시**를 클릭합니다.  
  
4.  새 게시 마법사의 **Oracle 게시자** 페이지에서 Oracle 게시자를 선택합니다. Oracle 게시자가 표시되지 않으면 **Oracle 게시자 추가**를 클릭하여 표시되는 이전 절차의 단계를 따르세요.  
  
5.  **게시 유형** 페이지에서 **스냅샷 게시** 또는 **트랜잭션 게시**를 선택합니다.  
  
6.  **아티클** 페이지에서 게시할 데이터베이스 개체를 선택합니다.  
  
     필요에 따라 테이블을 확장한 다음 하나 이상의 열에 대한 확인란의 선택을 취소하는 방법으로 테이블 열을 필터링하여 제외시킵니다. **아티클 속성** 을 클릭하여 아티클 속성을 보고 수정하며 필요에 따라 대체 데이터 형식 매핑을 지정합니다. 데이터 형식 매핑에 대한 자세한 내용은 [Oracle 게시자에 대한 데이터 형식 매핑 지정](specify-data-type-mappings-for-an-oracle-publisher.md)을 참조하세요.  
  
7.  **테이블 행 필터** 페이지에서 필요에 따라 필터를 적용하여 하나 이상의 테이블에서 데이터 하위 집합을 게시합니다.  
  
8.  모든 개체를 만들고 필요한 모든 데이터를 구독 데이터베이스에 추가한 경우에만 **스냅샷 에이전트** 페이지에서 **즉시 스냅샷 만들기** 의 선택을 취소합니다.  
  
9. **에이전트 보안** 페이지에서 스냅샷 에이전트(모든 게시의 경우) 및 로그 판독기 에이전트(트랜잭션 게시의 경우)에 대한 자격 증명을 지정합니다. 사용자가 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Windows 계정의 컨텍스트를 사용하여 에이전트를 실행하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 배포자에 연결합니다. 에이전트는 복제 관리 사용자 스키마로 지정한 계정의 컨텍스트를 사용하여 Oracle 데이터베이스에 연결합니다. 자세한 내용은 [Oracle 게시자 구성](../non-sql/configure-an-oracle-publisher.md)을 참조하세요.  
  
     각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../security/replication-agent-security-model.md) 및 [Replication Security Best Practices](../security/replication-security-best-practices.md)을 참조하세요.  
  
10. **마법사 동작** 페이지에서 필요에 따라 게시를 스크립팅합니다. 자세한 내용은 [Scripting Replication](../scripting-replication.md)을 참조하세요.  
  
11. **마법사 완료** 페이지에서 게시의 이름을 지정합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 Oracle 데이터베이스를 게시자로 구성한 경우 시스템 저장 프로시저를 사용하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자와 동일한 방법으로 트랜잭션 또는 스냅샷 게시를 만들 수 있습니다.  
  
#### <a name="to-create-an-oracle-publication"></a>Oracle 게시를 만들려면  
  
1.  Oracle 데이터베이스를 게시자로 구성합니다. 자세한 내용은 [Oracle 게시자 구성](../non-sql/configure-an-oracle-publisher.md)을 참조하세요.  
  
2.  원격 배포자가 없는 경우 원격 배포자를 구성합니다. 자세한 내용은 [Configure Publishing and Distribution](../configure-publishing-and-distribution.md)을 참조하세요.  
  
3.  Oracle 게시자가 사용할 원격 배포자에서 [sp_adddistpublisher&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)를 실행합니다. 에 **@publisher** Oracle 데이터베이스 인스턴스의 TNS (투명 한 네트워크 기판) 이름을 지정 하 고에 `ORACLE` `ORACLE GATEWAY` **@publisher_type**또는 값을 지정 합니다. Oracle 게시자에서 원격`Specify` 배포자에 연결할 때 사용하는 보안 모드를 다음 중 하나로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 합니다.  
  
    -   기본값인 Oracle 표준 인증을 사용하려면 **@security_mode** 에 **@security_mode**, **@login**에 구성 중 Oracle 게시자에 만든 복제 관리 사용자 스키마의 로그인, **@password**의 Oracle 데이터베이스에서 구독을 만드는 방법에 대해 설명합니다.  
  
        > [!IMPORTANT]  
        >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정해야 합니다.  
  
    -   Windows 자격 증명을 사용하려면 **@security_mode** 에 **@security_mode**의 Oracle 데이터베이스에서 구독을 만드는 방법에 대해 설명합니다.  
  
        > [!NOTE]  
        >  Windows 인증을 사용하려면 Windows 자격 증명을 사용한 연결을 허용하도록 Oracle 서버를 구성해야 하며(자세한 내용은 Oracle 설명서 참조), 복제 관리 사용자 스키마에 대해 지정한 Microsoft Windows 계정과 동일한 계정으로 로그인한 상태여야 합니다.  
  
4.  게시 데이터베이스에 대한 로그 판독기 에이전트 작업을 만듭니다.  
  
    -   게시된 데이터베이스에 대한 로그 판독기 에이전트 작업이 존재하는지 확실하지 않으면 배포 데이터베이스의 Oracle 게시자가 사용하는 배포자에서 [sp_helplogreader_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql)를 실행합니다. 에 대 한 **@publisher**Oracle 게시자의 이름을 지정 합니다. 결과 집합이 비어 있으면 로그 판독기 에이전트 작업을 만들어야 합니다.  
  
    -   게시 데이터베이스에 대한 로그 판독기 에이전트 작업이 이미 존재하면 5단계를 실행합니다.  
  
    -   배포 데이터베이스의 Oracle 게시자가 사용하는 배포자에서 [sp_addlogreader_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)를 실행합니다. 및 **@job_login** **@job_password**에 에이전트가 실행 되는 Windows 자격 증명을 지정 합니다.  
  
        > [!NOTE]  
        >  매개 **@job_login** 변수는 3 단계에서 제공 된 로그인과 일치 해야 합니다. 게시자 보안 정보를 제공하지 마세요. 로그 판독기 에이전트는 3단계에 제공된 보안 정보를 사용하여 게시자에 연결합니다.  
  
5.  배포 데이터베이스의 배포자에서 [sp_addpublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)을 실행하여 게시를 만듭니다. 자세한 내용은 [게시 만들기](create-a-publication.md)를 참조하세요.  
  
6.  배포 데이터베이스의 배포자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)을 실행합니다. 에 **@publication** 4 단계에서 사용 된 게시 이름을 지정 하 고 및 **@job_name** **@password**에 대 한 스냅숏 에이전트 실행 되는 Windows 자격 증명을 지정 합니다. 게시자에 연결할 때 Oracle 표준 인증을 사용하려면 **@security_mode** 에 **@publisher_security_mode** 을 지정하고 **@publisher_login** 및 **@publisher_password**의 Oracle 데이터베이스에서 구독을 만드는 방법에 대해 설명합니다. 이렇게 하면 게시에 대해 스냅샷 에이전트 작업이 만들어집니다.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자 구성](../non-sql/configure-an-oracle-publisher.md)   
 [데이터 및 데이터베이스 개체 게시](publish-data-and-database-objects.md)   
 [Oracle 게시자에 대한 트랜잭션 집합 작업 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Oracle 게시 개요](../non-sql/oracle-publishing-overview.md)   
 [Oracle 권한 부여 스크립트](../non-sql/script-to-grant-oracle-permissions.md)  
  
  
