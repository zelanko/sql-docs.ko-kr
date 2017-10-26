---
title: "서버 인증 모드 변경 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08b2ad077cbd029cf1fa4b2ff0243c078467c17a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="change-server-authentication-mode"></a>서버 인증 모드 변경
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 서버 인증 모드를 변경하는 방법에 대해 설명합니다. 설치하는 동안 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 **Windows 인증 모드** 또는 **SQL Server 및 Windows 인증 모드**로 설정됩니다. 설치 후 언제든지 인증 모드를 변경할 수 있습니다.  
  
 설치 중에 **Windows 인증 모드** 를 선택하면 sa 로그인이 해제되며 설치 프로그램에서 암호를 할당합니다. 나중에 인증 모드를 **SQL Server 및 Windows 인증 모드**로 변경해도 sa 로그인은 계속 해제되어 있습니다. sa 로그인을 사용하려면 ALTER LOGIN 문을 사용하여 sa 로그인을 설정하고 새 암호를 할당합니다. sa 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용한 서버 연결만 허용합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 서버 인증 모드를 변경합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
 sa 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정으로 잘 알려져 있으며 종종 악의적인 사용자의 대상이 됩니다. 응용 프로그램에서 요청하지 않는 한 sa 계정을 사용하지 마십시오. sa 로그인에 대해 강력한 암호를 사용하는 것이 중요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-change-security-authentication-mode"></a>보안 인증 모드를 변경하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **보안** 페이지의 **Server 인증**에서 새 서버 인증 모드를 선택한 후에 **확인**을 클릭합니다.  
  
3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 대화 상자에서 **확인** 을 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
4.  개체 탐색기에서 해당 서버를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행되고 있으면 에이전트도 다시 시작해야 합니다.  
  
#### <a name="to-enable-the-sa-login"></a>sa 로그인을 사용하려면  
  
1.  개체 탐색기에서 **보안**, 로그인을 차례로 확장하고 **sa**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **일반** 페이지에서 로그인에 대한 암호를 만들고 확인할 수 있습니다.  
  
3.  **상태** 페이지의 **로그인** 섹션에서 **사용**을 클릭한 다음 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **sa 로그인을 사용하려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 sa 로그인을 사용하도록 설정하고 새 암호를 설정합니다.  
  
    ```  
    ALTER LOGIN sa ENABLE ;  
    GO  
    ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
    GO  
  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [강력한 암호](../../relational-databases/security/strong-passwords.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [시스템 관리자가 잠겨 있는 경우 SQL Server에 연결](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
  

