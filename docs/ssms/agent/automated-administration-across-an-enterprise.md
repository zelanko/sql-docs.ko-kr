---
title: 기업 내 관리 자동화 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enterprise automatic administration [SQL Server]
- multiserver administration [SQL Server]
- SQL Server Agent jobs, multiserver administration
- jobs [SQL Server Agent], multiserver administration
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- master servers [SQL Server]
- multiple instances of SQL Server
- target servers [SQL Server]
ms.assetid: 44d8365b-42bd-4955-b5b2-74a8a9f4a75f
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 905a470c09c1fff750900764134846925d7899b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65095877"
---
# <a name="automated-administration-across-an-enterprise"></a>기업 내 관리 자동화
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 여러 인스턴스에 대한 관리 자동화를 *다중 서버 관리*라고 합니다. 다중 서버 관리를 사용하여 다음을 수행합니다.  
  
-   두 대 이상의 서버 관리  
  
-   데이터 웨어하우징을 위해 엔터프라이즈 서버 간의 정보 흐름 예약  
  
다중 서버 관리를 이용하려면 마스터 서버와 대상 서버가 적어도 하나씩 있어야 합니다. 마스터 서버는 대상 서버에 작업을 배포하거나 대상 서버에서 이벤트를 받습니다. 또한 마스터 서버에서는 대상 서버에서 실행되는 작업에 대한 작업 정의의 중앙 복사본을 저장합니다. 대상 서버는 주기적으로 마스터 서버에 연결되어 작업 일정을 업데이트합니다. 새 작업이 마스터 서버에 있는 경우 대상 서버는 작업을 다운로드합니다. 대상 서버는 작업을 완료한 후에 마스터 서버에 다시 연결하여 작업 상태를 보고합니다. 데이터베이스 관련 활동을 수행하는 경우 작업 정의가 동일해야 합니다.  
  
다음 그림은 마스터 서버와 대상 서버 간의 관계를 보여 줍니다.  
  
![다중 서버 관리 구성](../../ssms/agent/media/multisvr.gif "다중 서버 관리 구성")  
  
대기업에서 부서 서버를 관리하는 경우 다음을 정의할 수 있습니다.  
  
-   작업 단계를 사용하는 하나의 백업 작업  
  
-   백업 실패 시 알릴 운영자  
  
-   백업 작업의 실행 일정  
  
마스터 서버에 이 백업 작업을 한 번 쓴 다음 각 부서 서버를 대상 서버로 참여시킵니다. 모든 부서 서버는 참여할 때부터 동일한 백업 작업을 실행하지만 작업은 한 번만 정의합니다.  
  
> [!NOTE]  
> 다중 서버 관리 기능은 sysadmin 역할의 멤버를 위한 것입니다. 그러나 대상 서버에서 sysadmin 역할의 멤버는 마스터 서버에 의해 대상 서버에서 실행된 작업을 편집할 수 없습니다. 이 보안 조치는 작업 단계가 실수로 삭제되는 것과 대상 서버에서 작업이 중단되는 것을 방지합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[다중 서버 환경 만들기](../../ssms/agent/create-a-multiserver-environment.md)  
마스터 서버와 대상 서버를 만들고 관리하는 방법에 대해 설명합니다.  
  
[다중 서버 환경에 적합한 SQL Server 에이전트 서비스 계정 선택](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 관리자가 아닌 Windows 계정이나 로컬 시스템 계정을 사용할 경우 다중 서버 환경에 미치는 영향에 대한 정보를 포함합니다.  
  
[대상 서버의 암호화 옵션 설정](../../ssms/agent/set-encryption-options-on-target-servers.md)  
대상 서버에서 MsxEncryptChannelOptions [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 레지스트리 하위 키를 설정하는 방법에 대한 정보를 포함합니다.  
  
[기업 내 작업 관리](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
작업 상태를 확인하고, 작업의 대상 서버를 변경하고, 대상 서버 클럭을 동기화하고, 현재 작업 상태에 대해 마스터 서버를 폴링하는 방법에 대해 설명합니다.  
  
[프록시를 사용하는 다중 서버 작업 문제 해결](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
실패한 프록시 사용 다중 서버 작업의 문제 해결 방법에 대한 정보를 포함합니다.  
  
[서버 폴링](../../ssms/agent/poll-servers.md)  
암시적이고 명시적으로 대상 서버에서 마스터 서버를 폴링하여 작업 정보를 동기화하는 방법에 대해 설명합니다.  
  
[이벤트 관리](../../ssms/agent/manage-events.md)  
대상 서버에서 마스터 서버로 이벤트를 전달하는 방법에 대해 설명합니다.  
  
[기업 내의 자동화된 관리 튜닝](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
다중 서버 환경에서 자동화된 관리를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 자체 튜닝 기능을 사용하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 데이터베이스 엔진 설치 시 이전 버전과의 호환성 관련 항목](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
[서버 등록](../register-servers/register-servers.md)  
[sp_add_targetservergroup](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)  
[sp_delete_targetserver](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)  
[sp_delete_targetservergroup](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)  
[sp_help_downloadlist](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)  
[sp_help_jobserver](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)  
[sp_help_targetservergroup](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)  
[sp_resync_targetserver](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)  
[sp_update_targetservergroup](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)  
[sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
[syslogins](../../relational-databases/system-compatibility-views/sys-syslogins-transact-sql.md)  
[systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
  
