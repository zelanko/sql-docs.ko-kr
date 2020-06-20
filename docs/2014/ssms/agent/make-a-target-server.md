---
title: 대상 서버 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.tsxwiz.msx.f1
- sql12.ag.tsxwiz.cover.f1
- sql12.ag.tsxwiz.credentials.f1
- sql12.ag.tsxwiz.complete.f1
helpviewer_keywords:
- Target Server Wizard
- SQL Server Agent jobs, target servers
- target servers [SQL Server], creating
ms.assetid: 13aabe2d-67fe-4c67-8d49-2928dd705b7a
author: stevestein
ms.author: sstein
ms.openlocfilehash: bd60a19234d186bb0912978589fa60fd8e8a8c22
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008656"
---
# <a name="make-a-target-server"></a>대상 서버 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]또는 SMO(SQL Server 관리 개체)를 사용하여 대상 서버를 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **대상 서버를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 프록시와 연관된 단계가 있는 배포된 작업은 대상 서버의 프록시 계정 컨텍스트로 실행됩니다. 다음 조건이 만족되는지 또는 프록시와 연관된 작업 단계가 마스터 서버에서 대상으로 다운로드되지 않는지 확인하세요.  
  
-   마스터 서버 레지스트리 하위 키 **\ HKEY_LOCAL_MACHINE \software\microsoft\microsoft SQL Server \\ < *instance_name*> \sql server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD)는 1 (true)로 설정 됩니다. 기본적으로 이 하위 키는 0(false)으로 설정됩니다.  
  
-   프록시 계정이 작업 단계가 실행되는 마스터 서버 프록시 계정과 동일한 이름을 가진 대상 서버에 있는지 여부  
  
 마스터 서버에서 대상 서버로 다운로드할 때 프록시 계정을 사용하는 작업 단계가 실패한 경우 **msdb** 데이터베이스의 **sysdownloadlist** 테이블에 있는 **error_message** 열에서 다음 오류 메시지를 확인할 수 있습니다.  
  
-   "작업 단계에 프록시 계정이 필요하지만 일치하는 프록시를 대상 서버에서 사용할 수 없습니다."  
  
     이 오류를 해결하려면 **AllowDownloadedJobsToMatchProxyName** 레지스트리 하위 키를 1로 설정합니다.  
  
-   "프록시를 찾을 수 없습니다."  
  
     이 오류를 해결하려면 프록시 계정이 작업 단계가 실행되는 마스터 서버 프록시 계정과 동일한 이름을 가진 대상 서버에 있는지 확인합니다.  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 이 프로시저를 실행할 수 있는 권한은 기본적으로 `sysadmin` 고정 서버 역할의 멤버로 설정됩니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-make-a-target-server"></a>대상 서버를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음, 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리**를 가리킨 다음 **대상으로 만들기**를 클릭합니다. **대상 서버 만들기 마법사** 가 대상 서버를 만드는 프로세스를 안내합니다.  
  
3.  **마스터 서버 선택** 페이지에서 이 대상 서버가 작업을 받는 마스터 서버를 선택합니다.  
  
     **서버 선택**  
     마스터 서버에 연결합니다.  
  
     **이 서버에 대한 설명**  
     이 대상 서버에 대한 설명을 입력합니다. 대상 서버는 이 설명을 마스터 서버로 업로드합니다.  
  
4.  **마스터 서버 로그인 자격 증명** 페이지에서 필요한 경우 대상 서버에 새 로그인을 만듭니다.  
  
     **필요한 경우 새 로그인을 만들고 MSX에 대한 권한을 할당합니다.**  
     지정한 로그인이 없으면 대상 서버에 새 로그인을 만듭니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-make-a-target-server"></a>대상 서버를 만들려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 현재 서버를 AdventureWorks1 마스터 서버에 참여시킵니다. 현재 서버의 위치는 Building 21, Room 309, Rack 5입니다.  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
        N'Building 21, Room 309, Rack 5' ;   
    GO;  
    ```  
  
     자세한 내용은 [sp_msx_enlist &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)를 참조 하세요.  
  
##  <a name="using-sql-server-management-objects-smo"></a><a name="PowerShellProcedure"></a>SQL Server 관리 개체 사용 (SMO)  
  
## <a name="see-also"></a>참고 항목  
 [기업 내 관리 자동화](automated-administration-across-an-enterprise.md)  
