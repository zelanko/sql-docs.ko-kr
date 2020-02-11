---
title: SQL Server 에이전트 보안 구현 | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 52537ac126115fbde3d7d0fb1a13f61f1d25cf15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63137527"
---
# <a name="implement-sql-server-agent-security"></a>SQL Server 에이전트 보안 구현
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트를 사용 하면 데이터베이스 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시에 의해 결정 되는 해당 작업 단계를 수행 하는 데 필요한 사용 권한만 있는 보안 컨텍스트에서 각 작업 단계를 실행할 수 있습니다. 특정 작업 단계의 사용 권한을 설정하려면 필요 사용 권한을 가진 프록시를 만든 다음 해당 프록시를 작업 단계에 할당하십시오. 프록시는 둘 이상의 작업 단계에 대해 지정할 수 있습니다. 동일 사용 권한이 필요한 작업 단계에 대해서는 동일한 프록시를 사용합니다.  
  
 다음 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 작업을 만들거나 실행할 수 있도록 사용자에게 부여해야 하는 데이터베이스 역할에 대해 설명합니다.  
  
## <a name="granting-access-to-sql-server-agent"></a>SQL Server 에이전트에 액세스 부여  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하려면 사용자가 다음 고정 데이터베이스 역할 중 하나 이상의 멤버여야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할은 **msdb** 데이터베이스에 저장 됩니다. 기본적으로 사용자는 이러한 데이터베이스 역할의 멤버가 아닙니다. 이러한 역할의 멤버는 명시적으로 부여되어야 합니다. 
  **sysadmin** 고정 서버 역할의 멤버인 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 대해 모든 권한을 가지며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하기 위해 이러한 고정 데이터베이스 역할의 멤버일 필요가 없습니다. 이러한 데이터베이스 역할 또는 **sysadmin** 역할의 멤버가 아닌 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결할 때 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에이전트 노드를 사용할 수 없습니다.  
  
 이러한 데이터베이스 역할의 멤버는 자신이 소유하는 작업을 보고 실행할 수 있으며 기존 프록시 계정으로 실행되는 작업 단계를 만들 수 있습니다. 이러한 각 역할과 관련된 특정 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 
  **sysadmin** 고정 서버 역할의 멤버에게는 프록시 계정을 만들고 수정하고 삭제할 수 있는 권한이 있습니다. 
  **sysadmin** 역할의 멤버는 프록시를 지정하지 않는 작업 단계를 만들 수 있는 권한이 있지만 그 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 시작하는 데 사용되는 계정인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정으로 실행합니다.  
  
## <a name="guidelines"></a>지침  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 구현에 대한 보안을 향상시키려면 다음 지침을 따르십시오.  
  
-   프록시에 대한 전용 사용자 계정을 만들고 이러한 프록시 사용자 계정만 사용하여 작업 단계를 실행합니다.  
  
-   프록시 사용자 계정에 필요한 사용 권한만 부여합니다. 특정 프록시 계정에 할당된 작업 단계를 실행하는 데 실제로 필요한 사용 권한만 부여합니다.  
  
-   Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Administrators **그룹의 멤버인 Microsoft Windows 계정을 사용하여** 에이전트 서비스를 실행하지 않습니다.  
  
-   프록시는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명 저장소만큼만 안전합니다.  
  
-   사용자 쓰기 작업으로 NT 이벤트 로그에 쓸 수 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 통해 경고를 올립니다.  
  
-   NT 관리 계정은 서비스 계정 또는 프록시 계정으로 지정하지 않습니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 서로의 자산에 대한 액세스 권한이 있습니다. 두 서비스가 단일 프로세스 공간을 공유하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 sysadmin입니다.  
  
-   TSX를 MSF에 등록할 때 MSX sysadmins는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 TSX 인스턴스에 대한 총 제어 권한을 가져옵니다.  
  
-   ACE는 확장 파일이며 그 자체를 호출할 수 없습니다. ACE는 Microsoft.SqlServer.Chainer.Setup.exe라는 Chainer ScenarioEngine.exe에서 호출되거나 다른 호스트 프로세스에서 호출될 수 있습니다.  
  
-   ACE는 해당 API의 DLL이 ACE에서 호출되기 때문에 SSDP에서 소유된 다음 구성 DLL에 따라 달라집니다.  
  
    -   **SCO** -가상 계정에 대 한 새 SCO 유효성 검사를 포함 하는 Microsoft.  
  
    -   **Cluster** -Microsoft. SqlServer.. d l l .dll  
  
    -   **SFC** -microsoft.sqlserver.configuration.sqlconfigbase.dll. dll  
  
    -   **확장명** -Microsoft. c o n. c l o. c o d .dll  
  
## <a name="see-also"></a>참고 항목  
 [미리 정의된 역할](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [Transact-sql&#41;sp_addrolemember &#40;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)   
 [Transact-sql&#41;sp_droprolemember &#40;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)   
 [SQL Server 데이터베이스 엔진 및 Azure SQL Database 보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
