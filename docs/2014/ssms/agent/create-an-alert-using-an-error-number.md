---
title: 오류 번호를 사용하여 경고 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- alerts [SQL Server], error numbers
ms.assetid: 03dd7fac-5073-4f86-babd-37e45a86023c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f0884a37c443f863cf0c1001bae1242852db3ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63135367"
---
# <a name="create-an-alert-using-an-error-number"></a>오류 번호를 사용하여 경고 만들기
  이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 항목에서는 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용 하 여 특정 번호의 오류가 발생할 때 발생 하는 에이전트 경고를 만드는 방법에 대해 설명 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **오류 번호를 사용 하 여 경고를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 전체 경고 시스템을 간편하게 그래픽 방식으로 관리할 수 있도록 해 줄 뿐만 아니라 경고 인프라를 구성하는 데 있어서도 권장되는 방법입니다.  
  
-   master 데이터베이스에서 **xp_logevent** 로 생성된 이벤트가 발생합니다. 따라서 경고에 대한 **xp_logevent** 이 **@database_name** 또는 NULL이 아닌 경우 **xp_logevent** 는 경고를 트리거하지 않습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버만 **sp_add_alert**를 실행할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>오류 번호를 사용하여 경고를 만들려면  
  
1.  
  **개체 탐색기** 에서 더하기 기호를 클릭하여 오류 번호로 경고를 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **경고** 를 마우스 오른쪽 단추로 클릭하고 **새 경고**를 선택합니다.  
  
4.  **새 경고** 대화 상자의 **이름** 상자에 이 경고의 이름을 입력합니다.  
  
5.  
  **사용** 확인란을 선택하여 경고를 실행할 수 있도록 합니다. 기본적으로 **사용** 이 선택됩니다.  
  
6.  **유형** 목록에서 **SQL Server 이벤트 경고**를 선택합니다.  
  
7.  **이벤트 경고 정의**아래의 **데이터베이스 이름** 목록에서 데이터베이스를 선택하여 경고를 특정 데이터베이스로 제한합니다.  
  
8.  
  **경고 발생 기준**에서 **오류 번호**를 클릭한 다음 경고에 알맞은 오류 번호를 입력합니다. 또는 **심각도** 를 클릭한 다음 경고를 발생시킬 특정 심각도를 선택합니다.  
  
9. **메시지에 다음 텍스트가 포함될 때 경고 발생** 에 해당하는 확인란을 선택하여 경고를 특정 문자 시퀀스로 제한한 다음 **메시지 텍스트**에 대한 키워드나 문자열을 입력합니다. 최대 문자 수는 100자입니다.  
  
10. **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>오류 번호를 사용하여 경고를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
 자세한 내용은 [sp_add_alert &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)를 참조 하세요.  
  
  
