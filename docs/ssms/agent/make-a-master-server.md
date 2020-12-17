---
description: Make a Master Server
title: Make a Master Server
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.msxwiz.operator.f1
- sql13.ag.msxwiz.login.f1
- sql13.ag.msxwiz.target.f1
- sql13.ag.msxwiz.complete.f1
- sql13.ag.msxwiz.cover.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 2d135926a87fe6350ace308a6efd44a93accfcd4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97409156"
---
# <a name="make-a-master-server"></a>Make a Master Server
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 마스터 서버 [!INCLUDE[tsql](../../includes/tsql-md.md)]를 만드는 방법에 대해 설명합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
프록시와 연관된 단계가 있는 배포된 작업은 대상 서버의 프록시 계정 컨텍스트로 실행됩니다. 다음 조건이 만족되는지 또는 프록시와 연관된 작업 단계가 마스터 서버에서 대상으로 다운로드되지 않는지 확인하세요.  
  
-   마스터 서버 레지스트리 하위 키 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD)을 1(true)로 설정합니다. 기본적으로 이 하위 키는 0(false)으로 설정됩니다.  
  
-   프록시 계정이 작업 단계가 실행되는 마스터 서버 프록시 계정과 동일한 이름을 가진 대상 서버에 있는지 여부  
  
마스터 서버에서 대상 서버로 다운로드할 때 프록시 계정을 사용하는 작업 단계가 실패한 경우 **msdb** 데이터베이스의 **sysdownloadlist** 테이블에 있는 **error_message** 열에서 다음 오류 메시지를 확인할 수 있습니다.  
  
-   "작업 단계에 프록시 계정이 필요하지만 일치하는 프록시를 대상 서버에서 사용할 수 없습니다."  
  
    이 오류를 해결하려면 **AllowDownloadedJobsToMatchProxyName** 레지스트리 하위 키를 1로 설정합니다.  
  
-   "프록시를 찾을 수 없습니다."  
  
    이 오류를 해결하려면 프록시 계정이 작업 단계가 실행되는 마스터 서버 프록시 계정과 동일한 이름을 가진 대상 서버에 있는지 확인합니다.  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
이 프로시저를 실행할 수 있는 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-make-a-master-server"></a>마스터 서버를 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]의 인스턴스에 연결한 다음, 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리** 를 가리킨 다음 **마스터로 만들기** 를 클릭합니다. **마스터 서버 마법사** 는 마스터 서버를 만들고 대상 서버를 추가하는 프로세스를 안내합니다.  
  
3.  **마스터 서버 운영자** 페이지에서 마스터 서버 운영자를 구성합니다. 전자 메일 또는 호출기를 사용하여 운영자에게 알림을 보내려면 전자 메일을 보내도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성해야 합니다. **net send** 를 사용하여 운영자에게 알림을 보내려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 설치된 서버에서 메신저 서비스가 실행되고 있어야 합니다.  
  
    **전자 메일 주소**  
    운영자의 전자 메일 주소를 설정합니다.  
  
    **호출기 주소**  
    운영자의 호출기 전자 메일 주소를 설정합니다.  
  
    **Net Send 주소**  
    운영자에 대한 **net send** 주소를 설정합니다.  
  
4.  **대상 서버** 페이지에서 마스터 서버의 대상 서버를 선택합니다.  
  
    **등록된 서버**  
    Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 등록된 서버 중 대상 서버가 아닌 서버를 나열합니다.  
  
    **대상 서버**  
    대상 서버를 나열합니다.  
  
    **>**  
    선택한 서버를 대상 서버 목록으로 이동합니다.  
  
    **>>**  
    모든 서버를 대상 서버 목록으로 이동합니다.  
  
    **<**  
    선택한 서버를 대상 서버 목록에서 제거합니다.  
  
    **<<**  
    모든 서버를 대상 서버 목록에서 제거합니다.  
  
    **연결 추가**  
    서버를 등록하지 않고 대상 서버 목록에 추가합니다.  
  
    **연결**  
    선택한 서버의 연결 속성을 변경합니다.  
  
5.  **마스터 서버 로그인 자격 증명** 페이지에서 대상 서버에 대해 새 로그인을 만들지 여부와 필요한 경우 해당 로그인에 마스터 서버에 대한 권한을 부여할지 여부를 지정할 수 있습니다.  
  
    **필요한 경우 새 로그인을 만들고 MSX에 대한 권한을 할당합니다.**  
    지정한 로그인이 없으면 대상 서버에 새 로그인을 만듭니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-make-a-master-server"></a>마스터 서버를 만들려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde_md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예에서는 현재 서버를 AdventureWorks1 마스터 서버에 참여시킵니다. 현재 서버의 위치는 Building 21, Room 309, Rack 5입니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
자세한 내용은 [sp_msx_enlist(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[다중 서버 환경 만들기](../../ssms/agent/create-a-multiserver-environment.md)  
[기업 내 관리 자동화](../../ssms/agent/automated-administration-across-an-enterprise.md)  
