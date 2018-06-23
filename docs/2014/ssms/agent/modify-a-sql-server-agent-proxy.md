---
title: SQL Server 에이전트 프록시 수정 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- proxies [SQL Server Agent], modifying
- modifying SQL Server Agent proxy
ms.assetid: 6e1dfbaa-8089-4813-940c-d5a2e13d8552
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 028f92bc953f1baecae1a68bcdc822a0aa84e8fa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172088"
---
# <a name="modify-a-sql-server-agent-proxy"></a>Modify a SQL Server Agent Proxy
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시를 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 SQL Server 에이전트 프록시를 수정합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시는 자격 증명을 사용하여 Windows 사용자 계정에 대한 정보를 저장합니다. 자격 증명에 지정된 사용자에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 컴퓨터에 대한 "일괄 작업으로 로그온" 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 프록시에 대한 하위 시스템 액세스 권한을 확인하고 작업 단계가 실행될 때마다 프록시에 대한 액세스 권한을 부여합니다. 프록시에 하위 시스템에 대한 액세스 권한이 없으면 작업 단계가 실패합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 프록시에 지정된 사용자를 가장하여 작업 단계를 실행합니다.  
  
-   사용자의 로그인에 프록시에 대한 액세스 권한이 있거나 사용자가 프록시에 대한 액세스 권한이 있는 역할에 속하는 경우 해당 사용자는 작업 단계에서 프록시를 사용할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 고정 서버 역할의 멤버만 프록시 계정을 만들거나 수정하거나 삭제할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-includessnoversionincludesssnoversion-mdmd-agent-proxy"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시를 수정하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 수정하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정이 포함된 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **프록시** 폴더를 확장합니다.  
  
4.  더하기 기호를 클릭하여 프록시에 대한 하위 시스템 노드(예: **ActiveX 스크립트**)를 확장합니다.  
  
5.  수정하려는 프록시 계정을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  *proxy_name***프록시 계정 속성** 대화 상자에서 필요에 따라 프록시 계정을 변경합니다. 이 대화 상자의 옵션에 대한 자세한 내용은 [SQL Server 에이전트 프록시 만들기](create-a-sql-server-agent-proxy.md)를 참조하세요.  
  
7.  완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-modify-a-includessnoversionincludesssnoversion-mdmd-agent-proxy"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시를 수정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Disables the proxy named 'Catalog application proxy'.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 0;  
    GO  
    ```  
  
 자세한 내용은 참조 [sp_update_proxy &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-proxy-transact-sql)합니다.  
  
  
