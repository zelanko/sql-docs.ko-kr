---
title: 복제 에이전트 보안 모델 | Microsoft 문서
ms.custom: ''
ms.date: 10/07/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, security
- agents [SQL Server replication], security
- Distribution Agent, security
- logins [SQL Server replication], permissions for agents
- security [SQL Server replication], agent security model
- Log Reader Agent, security
- Queue Reader Agent, security
- Merge Agent, security
- replication [SQL Server], agents and profiles
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f34b5accc278a55946546c149c00bffd3a02a693
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811998"
---
# <a name="replication-agent-security-model"></a>복제 에이전트 보안 모델
  복제 에이전트 보안 모델을 사용하여 복제 에이전트를 실행 및 연결하는 계정을 세밀하게 제어할 수 있습니다. 즉, 각 에이전트에 대해 다른 계정을 지정할 수 있습니다. 계정을 지정하는 방법은 [복제의 로그인 및 암호 관리](manage-logins-and-passwords-in-replication.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  **sysadmin** 고정 서버 역할의 멤버가 복제를 구성할 경우 복제 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 계정을 가장하도록 구성할 수 있습니다. 이는 복제 에이전트의 로그인과 암호를 지정하여 수행할 수 있지만 이 방법은 사용하지 않는 것이 좋습니다. 대신 이 항목의 뒷부분에 나오는 "에이전트에 필요한 사용 권한" 섹션에서 설명하는 최소 사용 권한이 있는 각 에이전트에 대해 계정을 지정(최상의 보안 방법)하는 것이 좋습니다.  
  
 복제 에이전트는 모든 실행 파일처럼 Windows 계정의 컨텍스트에서 실행됩니다. 이 에이전트는 이 계정을 사용하여 Windows 통합 보안 연결을 설정합니다. 에이전트를 실행하는 계정은 에이전트를 시작하는 방법에 따라 달라집니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업에서 에이전트 시작(기본값) - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업을 사용하여 복제 에이전트를 시작하면 복제를 구성할 때 지정한 계정의 컨텍스트에서 에이전트가 실행됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 및 복제에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "SQL Server 에이전트의 에이전트 보안" 섹션을 참조하십시오. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 실행하는 계정에 필요한 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 구성](../../../ssms/agent/configure-sql-server-agent.md)을 참조하세요.  
  
-   MS-DOS 명령줄에서 직접 또는 스크립트를 통해 시작 - 명령줄에서 에이전트를 실행하는 사용자 계정의 컨텍스트에서 에이전트가 실행됩니다.  
  
-   RMO(복제 관리 개체) 또는 ActiveX 컨트롤을 사용하는 응용 프로그램에서 에이전트 시작 - RMO 또는 ActiveX 컨트롤을 호출하는 응용 프로그램의 컨텍스트에서 에이전트가 실행됩니다.  
  
    > [!NOTE]  
    >  ActiveX 컨트롤은 더 이상 사용되지 않습니다.  
  
 Windows 통합 보안의 컨텍스트에서 연결을 설정하는 것이 좋습니다. 이전 버전과의 호환성을 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보안을 사용할 수도 있습니다. 가장 적절한 방법에 대한 자세한 내용은 [Replication Security Best Practices](replication-security-best-practices.md)을 참조하십시오.  
  
## <a name="permissions-that-are-required-by-agents"></a>에이전트에 필요한 사용 권한  
 에이전트를 실행 및 연결하는 계정에는 여러 가지 사용 권한이 필요합니다. 다음 표에서는 이러한 사용 권한에 대해 설명합니다. 각 에이전트를 다른 Windows 계정으로 실행하는 것이 좋으며 이러한 계정에는 필요한 사용 권한만 부여해야 합니다. 여러 에이전트와 관련이 있는 PAL(게시 액세스 목록)에 대한 자세한 내용은 [게시자 보안 설정](secure-the-publisher.md)을 참조하세요.  
  
> [!NOTE]  
>  일부 Windows 운영 체제의 UAC(사용자 계정 컨트롤)에서 스냅숏 공유에 대한 관리 액세스를 거부할 수 있습니다. 따라서 스냅숏 에이전트, 배포 에이전트 및 병합 에이전트에서 사용하는 Windows 계정에 스냅숏 공유 권한을 명시적으로 부여해야 합니다. Windows 계정이 Administrators 그룹의 멤버인 경우에도 이 작업을 수행해야 합니다. 자세한 내용은 [스냅숏 폴더 보안 설정](secure-the-snapshot-folder.md)을 참조하세요.  
  
|에이전트|사용 권한|  
|-----------|-----------------|  
|스냅숏 에이전트|에이전트를 실행하는 Windows 계정을 사용하여 배포자에 연결합니다. 이 계정은 다음과 같아야 합니다.<br /><br /> -적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.<br /><br /> -스냅숏 공유에 대해 쓰기, 읽기 및 수정 권한이 있어야 합니다.<br /><br /> <br /><br /> 게시자 연결에 사용되는 계정은 적어도 게시 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.|  
|로그 판독기 에이전트|에이전트를 실행하는 Windows 계정을 사용하여 배포자에 연결합니다. 이 계정은 적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.<br /><br /> 게시자 연결에 사용되는 계정은 적어도 게시 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.<br /><br /> 선택 하는 경우는 `sync_type` 옵션 *복제만 지원*를 *backup을 사용 하 여 초기화*, 또는 *lsn에서 초기화*, 후 로그 판독기 에이전트를 실행 해야 합니다 실행 `sp_addsubscription`설치 스크립트가 배포 데이터베이스에 기록 되도록 합니다. 로그 판독기 에이전트는 **sysadmin** 고정 서버 역할의 멤버인 계정으로 실행되어야 합니다. 경우는 `sync_type` 옵션을 설정 *자동*, 특별 한 로그 판독기 에이전트 동작이 필요 하지 않습니다.|  
|밀어넣기 구독에 대한 배포 에이전트|에이전트를 실행하는 Windows 계정을 사용하여 배포자에 연결합니다. 이 계정은 다음과 같아야 합니다.<br /><br /> -적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.<br /><br /> -PAL의 멤버여야 합니다.<br /><br /> -스냅숏 공유에 대해 읽기 권한이 있어야 합니다.<br /><br /> -SQL Server 이외 구독자에 대한 구독인 경우에는 구독자용 OLE DB 공급자의 설치 디렉터리에 대해 읽기 권한이 있어야 합니다.<br /><br /> -LOB 데이터를 복제할 때 배포 에이전트에는 복제 **C:\Program Files\Microsoft SQL Server\XX\COMfolder** 에 대한 쓰기 권한이 있어야 합니다. 여기서 XX는 인스턴스 ID를 나타냅니다.<br /><br /> <br /><br /> 구독자 연결에 사용되는 계정은 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버이거나 SQL Server 이외 구독자에 대한 구독인 경우에는 동등한 권한이 있어야 합니다.<br /><br /> 참고: 사용 하는 경우 `-subscriptionstreams >= 2` 부여 해야 하는 배포 에이전트에는 `View Server State` 교착 상태를 검색할 구독자에 대 한 권한이 있습니다.|  
|끌어오기 구독에 대한 배포 에이전트|에이전트를 실행하는 Windows 계정을 사용하여 구독자에 연결합니다. 이 계정은 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다. 배포자 연결에 사용되는 계정은 다음과 같아야 합니다.<br /><br /> -PAL의 멤버여야 합니다.<br /><br /> -스냅숏 공유에 대해 읽기 권한이 있어야 합니다.<br /><br /> -LOB 데이터를 복제할 때 배포 에이전트에는 복제 **C:\Program Files\Microsoft SQL Server\XX\COMfolder** 에 대한 쓰기 권한이 있어야 합니다. 여기서 XX는 인스턴스 ID를 나타냅니다.<br /><br /> <br /><br /> 참고: 사용 하는 경우 `-subscriptionstreams >= 2` 부여 해야 하는 배포 에이전트에는 `View Server State` 교착 상태를 검색할 구독자에 대 한 권한이 있습니다.|  
|밀어넣기 구독에 대한 병합 에이전트|에이전트를 실행하는 Windows 계정을 사용하여 게시자 및 배포자에 연결합니다. 이 계정은 다음과 같아야 합니다.<br /><br /> -적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.<br /><br /> -PAL의 멤버여야 합니다.<br /><br /> -게시 데이터베이스의 사용자와 연결된 로그인이어야 합니다.<br /><br /> -스냅숏 공유에 대해 읽기 권한이 있어야 합니다.<br /><br /> <br /><br /> 구독자 연결에 사용되는 계정은 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.|  
|끌어오기 구독에 대한 병합 에이전트|에이전트를 실행하는 Windows 계정을 사용하여 구독자에 연결합니다. 이 계정은 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다. 게시자 및 배포자 연결에 사용되는 계정은 다음과 같아야 합니다.<br /><br /> -PAL의 멤버여야 합니다.<br /><br /> -게시 데이터베이스의 사용자와 연결된 로그인이어야 합니다.<br /><br /> -배포 데이터베이스의 사용자와 연결된 로그인이어야 합니다. 이 사용자는 `Guest` 사용자일 수 있습니다.<br /><br /> -스냅숏 공유에 대해 읽기 권한이 있어야 합니다.|  
|큐 판독기 에이전트|에이전트를 실행하는 Windows 계정을 사용하여 배포자에 연결합니다. 이 계정은 적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.<br /><br /> 게시자 연결에 사용되는 계정은 적어도 게시 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.<br /><br /> 구독자 연결에 사용되는 계정은 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.|  
  
## <a name="agent-security-under-sql-server-agent"></a>SQL Server 에이전트의 에이전트 보안  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] 프로시저 또는 RMO를 사용하여 복제를 구성하면 기본적으로 각 에이전트에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업이 생성됩니다. 그런 다음 계속, 일정대로 또는 요청 시 실행되는지 여부에 관계없이 에이전트가 작업 단계의 컨텍스트에서 실행됩니다. **의** 작업 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]폴더에서 이러한 작업을 볼 수 있습니다. 다음 표에서는 작업 이름을 나열합니다.  
  
|에이전트|작업 이름|  
|-----------|--------------|  
|스냅숏 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|  
|병합 게시 파티션에 대한 스냅숏 에이전트|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|  
|로그 판독기 에이전트|**\<Publisher>-\<PublicationDatabase>-\<integer>**|  
|끌어오기 구독에 대한 병합 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|  
|밀어넣기 구독에 대한 병합 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|밀어넣기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>** <sup>1</sup>|  
|끌어오기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>** <sup>2</sup>|  
|SQL Server 이외 구독자의 밀어넣기 구독에 대한 배포 에이전트|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|큐 판독기 에이전트|**[\<Distributor>].\<integer>**|  
  
 <sup>1</sup> Oracle 게시에 밀어넣기 구독의 경우 작업 이름은  **\<게시자 >-\<게시자**> 대신  **\<게시자 >-\< PublicationDatabase >** 합니다.  
  
 <sup>2</sup> Oracle 게시에 끌어오기 구독의 경우 작업 이름은  **\<게시자 >-\<DistributionDatabase**> 대신  **\<게시자 >-\< PublicationDatabase >** 합니다.  
  
 복제를 구성할 때는 에이전트를 실행해야 하는 계정을 지정합니다. 그러나 모든 작업 단계는 *프록시*의 보안 컨텍스트에서 실행되므로 복제는 사용자가 지정하는 에이전트 계정에 대해 다음 매핑을 내부적으로 수행합니다.  
  
-    [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](/sql/t-sql/statements/create-credential-transact-sql) 문을 사용하여 계정이 자격 증명에 먼저 매핑됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 프록시는 자격 증명을 사용하여 Windows 사용자 계정에 대한 정보를 저장합니다.  
  
-   [sp_add_proxy](/sql/relational-databases/system-stored-procedures/sp-add-proxy-transact-sql) 저장 프로시저가 호출되고 자격 증명을 사용하여 프록시가 생성됩니다.  
  
> [!NOTE]  
>  이 정보는 적절한 보안 컨텍스트로 에이전트를 실행하는 작업과 관련된 사항을 이해하는 데 도움을 주기 위한 것입니다. 이미 생성된 자격 증명이나 프록시와는 직접 상호 작용하지 않아도 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [보안 및 보호&#40;복제&#41;](security-and-protection-replication.md)   
 [스냅숏 폴더 보안 설정](secure-the-snapshot-folder.md)  
  
  
