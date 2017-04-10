---
title: "데이터베이스 메일 계정 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터베이스 메일 [SQL Server], 계정"
  - "계정 [데이터베이스 메일]"
ms.assetid: c07abbc6-fc6a-470b-8fa3-532f2e06b16a
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# 데이터베이스 메일 계정 만들기
  **데이터베이스 메일 구성 마법사** 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 데이터베이스 메일 계정을 만들 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [필수 구성 요소](#Prerequisites)  
  
-   **데이터베이스 메일 계정을 만들려면:** [데이터베이스 메일 구성 마법사](#SSMSProcedure), [Transact-SQL](#TsqlProcedure) 사용  
  
-   **후속 작업:**  [데이터베이스 메일을 구성하기 위한 다음 단계](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   전자 메일을 보내는 데 사용할 SMTP(Simple Mail Transfer Protocol) 서버의 이름과 포트 번호를 결정합니다. SMTP 서버에 인증이 필요한 경우 SMTP 서버의 사용자 이름과 암호를 결정합니다.  
  
-   필요에 따라 서버의 유형과 포트 번호도 지정할 수 있습니다. 보내는 메일의 서버 유형은 항상 'SMTP'입니다. 대부분의 SMTP 서버에서는 기본값인 포트 25를 사용합니다.  
  
##  <a name="SSMSProcedure"></a> 데이터베이스 메일 구성 마법사 사용  
 **마법사를 사용하여 데이터베이스 메일 계정을 만들려면**  
  
-   개체 탐색기에서 데이터베이스 메일을 구성할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 다음 서버 트리를 확장합니다.  
  
-   **관리** 노드를 확장합니다.  
  
-   데이터베이스 메일을 두 번 클릭하여 데이터베이스 메일 구성 마법사를 엽니다.  
  
-   **구성 태스크 선택** 페이지에서 **데이터베이스 메일 계정 및 프로필 관리**를 선택하고 **다음**을 클릭합니다.  
  
-   **프로필 및 계정 관리** 페이지에서 **새 계정 만들기** 를 선택하고 **다음**을 클릭합니다.  
  
-   **새 계정** 페이지에서 계정 이름, 설명, 메일 서버 정보 및 인증 유형을 지정합니다.  **다음**을 클릭합니다.  
  
-   **마법사 완료** 페이지에서 수행할 동작을 검토하고 **마침** 을 클릭하여 새 계정 만들기를 완료합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **Transact-SQL을 사용하여 데이터베이스 메일 계정을 만들려면**  
  
 **msdb.dbo.sysmail_add_account_sp** 저장 프로시저를 실행하여 계정을 만들고 다음 정보를 지정합니다.  
  
-   만들 계정의 이름  
  
-   계정에 대한 설명(옵션)  
  
-   보내는 전자 메일 메시지에 표시할 전자 메일 주소  
  
-   보내는 전자 메일 메시지에 표시할 표시 이름  
  
-   SMTP 서버의 이름  
  
-   SMTP 서버에 인증이 필요한 경우 SMTP 서버에 로그온하는 데 사용할 사용자 이름  
  
-   SMTP 서버에 인증이 필요한 경우 SMTP 서버에 로그온하는 데 사용할 암호  
  
 다음 예에서는 새 데이터베이스 메일 계정을 만듭니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
##  <a name="FollowUp"></a> 후속 작업: 데이터베이스 메일을 구성하기 위한 다음 단계  
  
-   [데이터베이스 메일 프로필 만들기](../../relational-databases/database-mail/create-a-database-mail-profile.md)  
  
  