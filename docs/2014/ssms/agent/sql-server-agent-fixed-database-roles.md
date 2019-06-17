---
title: SQL Server 에이전트 고정 데이터베이스 역할 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dcb939b8eb04fafce163a395b05eb0e272977283
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245989"
---
# <a name="sql-server-agent-fixed-database-roles"></a>SQL Server 에이전트 고정 데이터베이스 역할
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자에게 **에이전트에 대한 보다 세부적인 액세스 제어 기능을 제공하는 다음과 같은** msdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 고정 데이터베이스 역할을 제공합니다. 다음 역할은 액세스 권한이 적은 것부터 순서대로 나열되어 있습니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할 중 하나의 멤버가 아닌 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 연결한 경우 개체 탐색기의 **SQL Server 에이전트** 노드가 표시되지 않습니다. 사용자가 **에이전트를 사용하려면 이러한 고정 데이터베이스 역할 중 하나의 멤버이거나** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>SQL Server 에이전트 고정 데이터베이스 역할의 사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 데이터베이스 역할 사용 권한은 상호 공통적 특성을 갖고 있으며, 사용 권한이 많은 역할은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 개체(예: 경고, 운영자, 작업, 일정 및 프록시)에 대해 사용 권한이 적은 역할의 사용 권한을 상속합니다. 예를 들어 사용 권한이 가장 적은 **SQLAgentUserRole** 의 멤버에 proxy_A에 대한 액세스가 부여된 경우 **SQLAgentReaderRole** 및 **SQLAgentOperatorRole** 의 멤버는 proxy_A에 대한 액세스가 명시적으로 부여되지 않았더라도 이 프록시에 대한 액세스를 자동으로 갖습니다. 이러한 방식은 보안 문제를 발생시킬 수 있으며 이에 대해서는 각 역할에 대한 다음 섹션에서 설명됩니다.  
  
### <a name="sqlagentuserrole-permissions"></a>SQLAgentUserRole 사용 권한  
 **SQLAgentUserRole** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 중 가장 사용 권한이 적은 역할입니다. 이 역할에는 운영자, 로컬 작업 및 작업 일정에 대한 사용 권한만 있습니다. **SQLAgentUserRole** 의 멤버는 자신이 소유하는 로컬 작업 및 작업 일정에 대한 사용 권한만 갖습니다. 이 역할의 멤버는 다중 서버 작업(마스터 및 대상 서버 작업)을 사용할 수 없으며 자신이 소유하지 않는 작업에 대한 액세스를 얻기 위해 작업 소유권을 변경할 수 없습니다. **SQLAgentUserRole** 멤버는 **의** 작업 단계 속성 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자에서만 사용 가능한 프록시 목록을 볼 수 있습니다. **SQLAgentUserRole** 멤버에게는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기의 **작업**노드만 표시됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles** 멤버에 프록시 액세스 권한을 부여하기 전에 보안 문자를 신중히 고려해야 합니다 **.** **SQLAgentReaderRole** 및 **SQLAgentOperatorRole** 은 자동으로 **SQLAgentUserRole**의 멤버가 됩니다. 즉, **SQLAgentReaderRole** 및 **SQLAgentOperatorRole** 의 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **에 부여된 모든** 에이전트 프록시에 대한 액세스를 가지며 이러한 프록시를 사용할 수 있습니다.  
  
 다음 표에서는 **에이전트 개체에 대한** SQLAgentUserRole [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 권한을 요약합니다.  
  
|작업|연산자|로컬 작업<br /><br /> (소유한 작업만 해당)|작업 일정<br /><br /> (소유한 작업만 해당)|프록시|  
|------------|---------------|----------------------------------------|------------------------------------------------|-------------|  
|생성/수정/삭제|아니요|예 <sup>1</sup>|사용자 계정 컨트롤|아니요|  
|목록 보기(열거)|예 <sup>2</sup>|사용자 계정 컨트롤|사용자 계정 컨트롤|예 <sup>3</sup>|  
|설정/해제|아니요|예|사용자 계정 컨트롤|해당 사항 없음|  
|속성 보기|아니요|예|예|아니요|  
|실행/중지/시작|해당 사항 없음|사용자 계정 컨트롤|해당 사항 없음|해당 사항 없음|  
|작업 기록 보기|해당 사항 없음|사용자 계정 컨트롤|해당 사항 없음|해당 사항 없음|  
|작업 기록 삭제|해당 사항 없음|아니요 <sup>4</sup>|해당 사항 없음|해당 사항 없음|  
|연결/분리|해당 사항 없음|해당 사항 없음|사용자 계정 컨트롤|해당 사항 없음|  
  
 <sup>1</sup> 작업 소유권을 변경할 수 없습니다.  
  
 <sup>2</sup> 에서 사용 하기 위해 사용할 수 있는 운영자 목록을 가져올 수 있습니다 **sp_notify_operator** 하며 **작업 속성** Management Studio 대화 상자.  
  
 <sup>3</sup> 에서만 사용할 수 있는 프록시를 나열 합니다 **작업 단계 속성** Management Studio 대화 상자.  
  
 <sup>4</sup> 멤버인 **SQLAgentUserRole** 명시적으로 권한을 부여 해야 합니다 EXECUTE에 **sp_purge_jobhistory** 자신이 소유한 작업에 대 한 작업 기록을 삭제 하려면. 이 멤버는 다른 작업에 대한 작업 기록은 삭제할 수 없습니다.  
  
### <a name="sqlagentreaderrole-permissions"></a>SQLAgentReaderRole 사용 권한  
 **SQLAgentReaderRole** 에는 모든 **SQLAgentUserRole** 사용 권한 뿐만 아니라 사용 가능한 다중 서버 작업, 해당 속성 및 해당 기록 목록을 볼 수 있는 권한이 포함됩니다. 이 역할의 멤버는 또한 자신이 소유하는 작업과 작업 일정뿐만 아니라 사용 가능한 모든 작업과 작업 일정 및 해당 속성 목록을 볼 수 있습니다. **SQLAgentReaderRole** 멤버는 자신이 소유하지 않는 작업에 대한 액세스를 얻기 위해 작업 소유권을 변경할 수 없습니다. **SQLAgentReaderRole** 멤버에게는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기의 **작업**노드만 표시됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles** 멤버에 프록시 액세스 권한을 부여하기 전에 보안 문자를 신중히 고려해야 합니다 **.** **SQLAgentReaderRole** 의 멤버는 자동으로 **SQLAgentUserRole**의 멤버가 됩니다. 즉, **SQLAgentReaderRole** 의 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **에 부여된 모든** 에이전트 프록시에 대한 액세스를 가지며 이러한 프록시를 사용할 수 있습니다.  
  
 다음 표에서는 **에이전트 개체에 대한** SQLAgentReaderRole [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 권한을 요약합니다.  
  
|작업|연산자|로컬 작업|다중 서버 작업|작업 일정|프록시|  
|------------|---------------|----------------|----------------------|-------------------|-------------|  
|생성/수정/삭제|아니요|예 <sup>1</sup> (소유한 작업만 해당)|아니요|예(소유한 작업만 해당)|아니요|  
|목록 보기(열거)|예 <sup>2</sup>|사용자 계정 컨트롤|예|사용자 계정 컨트롤|예 <sup>3</sup>|  
|설정/해제|아니요|예(소유한 작업만 해당)|아니요|예(소유한 작업만 해당)|해당 사항 없음|  
|속성 보기|아니요|예|예|예|아니요|  
|속성 편집|아니요|예(소유한 작업만 해당)|아니요|예(소유한 작업만 해당)|아니요|  
|실행/중지/시작|해당 사항 없음|예(소유한 작업만 해당)|아니요|해당 사항 없음|해당 사항 없음|  
|작업 기록 보기|해당 사항 없음|사용자 계정 컨트롤|사용자 계정 컨트롤|해당 사항 없음|해당 사항 없음|  
|작업 기록 삭제|해당 사항 없음|아니요 <sup>4</sup>|아니요|해당 사항 없음|해당 사항 없음|  
|연결/분리|해당 사항 없음|해당 사항 없음|해당 사항 없음|예(소유한 작업만 해당)|해당 사항 없음|  
  
 <sup>1</sup> 작업 소유권을 변경할 수 없습니다.  
  
 <sup>2</sup> 에서 사용 하기 위해 사용할 수 있는 운영자 목록을 가져올 수 있습니다 **sp_notify_operator** 하며 **작업 속성** Management Studio 대화 상자.  
  
 <sup>3</sup> 에서만 사용할 수 있는 프록시를 나열 합니다 **작업 단계 속성** Management Studio 대화 상자.  
  
 <sup>4</sup> 멤버인 **SQLAgentReaderRole** 명시적으로 권한을 부여 해야 합니다 EXECUTE에 **sp_purge_jobhistory** 자신이 소유한 작업에 대 한 작업 기록을 삭제 하려면. 이 멤버는 다른 작업에 대한 작업 기록은 삭제할 수 없습니다.  
  
### <a name="sqlagentoperatorrole-permissions"></a>SQLAgentOperatorRole 사용 권한  
 **SQLAgentOperatorRole** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 중 가장 사용 권한이 많은 역할입니다. 여기에는 **SQLAgentUserRole** 및 **SQLAgentReaderRole**의 모든 사용 권한이 포함됩니다. 이 역할의 멤버는 또한 운영자 및 프록시의 속성을 볼 수 있으며 서버에서 사용 가능한 프록시와 경고를 열거할 수 있습니다.  
  
 **SQLAgentOperatorRole** 멤버는 로컬 작업 및 일정에 대한 추가 사용 권한을 갖습니다. 이 멤버는 모든 로컬 작업을 실행, 중지 또는 시작할 수 있으며 서버의 모든 로컬 작업에 대한 작업 기록을 삭제할 수 있습니다. 또한 서버의 모든 로컬 작업과 일정을 설정 또는 해제할 수 있습니다. 로컬 작업이나 일정을 설정 또는 해제하려면 이 역할의 멤버가 **sp_update_job** 및 **sp_update_schedule**저장 프로시저를 사용해야 합니다. **SQLAgentOperatorRole** 멤버는 작업 또는 일정 이름이나 식별자를 지정하는 매개 변수와 **@enabled** 매개 변수만 지정할 수 있습니다. 다른 매개 변수를 지정하면 해당 저장 프로시저 실행이 실패합니다. **SQLAgentOperatorRole** 멤버는 자신이 소유하지 않는 작업에 대한 액세스를 얻기 위해 작업 소유권을 변경할 수 없습니다.  
  
 **개체 탐색기의**작업 **,** 경고 **,** 운영자 **및** 프록시 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 **SQLAgentOperatorRole**의 멤버에게 표시됩니다. 이 역할의 멤버에게는 **오류 로그** 노드만 표시되지 않습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles** 멤버에 프록시 액세스 권한을 부여하기 전에 보안 문자를 신중히 고려해야 합니다 **.** **SQLAgentOperatorRole** 의 멤버는 자동으로 **SQLAgentUserRole** 및 **SQLAgentReaderRole**의 멤버가 됩니다. 즉, **SQLAgentOperatorRole** 의 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **또는** SQLAgentReaderRole **에 부여된 모든** 에이전트 프록시에 대한 액세스를 가지며 이러한 프록시를 사용할 수 있습니다.  
  
 다음 표에서는 **에이전트 개체에 대한** SQLAgentOperatorRole [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 권한을 요약합니다.  
  
|작업|,|연산자|로컬 작업|다중 서버 작업|작업 일정|프록시|  
|------------|------------|---------------|----------------|----------------------|-------------------|-------------|  
|생성/수정/삭제|아니오|아니요|예 <sup>2</sup> (소유한 작업만 해당)|아니요|예(소유한 작업만 해당)|아니요|  
|목록 보기(열거)|사용자 계정 컨트롤|예 <sup>1</sup>|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|  
|설정/해제|아니요|아니요|예 <sup>3</sup>|아니요|예 <sup>4</sup>|해당 사항 없음|  
|속성 보기|사용자 계정 컨트롤|예|예|예|예|사용자 계정 컨트롤|  
|속성 편집|아니요|아니요|예(소유한 작업만 해당)|아니요|예(소유한 작업만 해당)|아니요|  
|실행/중지/시작|해당 사항 없음|해당 사항 없음|사용자 계정 컨트롤|아니요|해당 사항 없음|해당 사항 없음|  
|작업 기록 보기|해당 사항 없음|해당 사항 없음|사용자 계정 컨트롤|사용자 계정 컨트롤|해당 사항 없음|해당 사항 없음|  
|작업 기록 삭제|해당 사항 없음|해당 사항 없음|사용자 계정 컨트롤|아니요|해당 사항 없음|해당 사항 없음|  
|연결/분리|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|예(소유한 작업만 해당)|해당 사항 없음|  
  
 <sup>1</sup> 에서 사용 하기 위해 사용할 수 있는 운영자 목록을 가져올 수 있습니다 **sp_notify_operator** 하며 **작업 속성** Management Studio 대화 상자.  
  
 <sup>2</sup> 작업 소유권을 변경할 수 없습니다.  
  
 <sup>3</sup> **SQLAgentOperatorRole** 멤버 저장된 프로시저를 사용 하 여 소유 하지 않은 로컬 작업을 사용 하지 않도록 설정 하거나 설정할 수 있습니다 **sp_update_job** 에 대 한 값을 지정 하는 **@enabled** 하며 **@job_id** (또는 **@job_name** ) 매개 변수입니다. 이 역할의 멤버가 이 저장 프로시저에 다른 매개 변수를 지정하는 경우 프로시저 실행이 실패합니다.  
  
 <sup>4</sup> **SQLAgentOperatorRole** 멤버 저장된 프로시저를 사용 하 여 소유 하지 않은 일정을 사용 하지 않도록 설정 하거나 설정할 수 있습니다 **sp_update_schedule** 에 대 한 값을 지정 하는 **@enabled** 하며 **@schedule_id** (또는 **@name** ) 매개 변수입니다. 이 역할의 멤버가 이 저장 프로시저에 다른 매개 변수를 지정하는 경우 프로시저 실행이 실패합니다.  
  
## <a name="assigning-users-multiple-roles"></a>사용자에게 다중 역할 할당  
 **sysadmin** 고정 서버 역할의 멤버는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 기능에 액세스할 수 있습니다. 사용자가 **sysadmin** 역할의 멤버가 아니지만 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할의 멤버인 경우 이러한 역할에 대한 공통적 사용 권한 모델을 고려해야 합니다. 사용 권한이 많은 역할은 항상 사용 권한이 적은 역할의 모든 사용 권한을 포함하기 때문에 두 개 이상의 역할의 멤버는 해당 사용자가 멤버로 속한 사용 권한이 가장 많은 역할과 관련된 사용 권한을 자동으로 갖습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 보안 구현](implement-sql-server-agent-security.md)   
 [sp_update_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)   
 [sp_update_schedule &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql)   
 [sp_notify_operator &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)   
 [sp_purge_jobhistory &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)  
  
  
