---
title: 운영자의 응답 가능 여부 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- canceling operators
- reactivating operators
- removing operators
- deleting operators
- available operators [SQL Server]
- dropping operators
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
- disabling operators
- operators (users) [Database Engine], changing availability with Management Studio
ms.assetid: 10d58b92-b67b-47e2-af9c-9f9fd6968bba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 11e5b26a9e2a953aff319b41749d2c12be1a880e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63017101"
---
# <a name="change-an-operator39s-availability"></a>운영자의 응답 가능 여부 변경
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 운영자의 경고 알림 수신 일정을 변경하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **운영자의 응답 가능 여부를 변경하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 고정 서버 역할의 멤버만이 운영자를 편집할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-change-an-operators-availability"></a>운영자의 응답 가능 여부를 변경하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 사용하거나 사용하지 않도록 설정할 운영자가 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **운영자** 폴더를 확장합니다.  
  
4.  사용하거나 사용하지 않도록 설정할 운영자를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음 **일반** 탭을 클릭합니다.  
  
5.  _operator_name_**속성** 대화 상자에서 **사용** 확인란을 선택하거나 선택을 취소합니다.  
  
6.  **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-change-an-operators-availability"></a>운영자의 응답 가능 여부를 변경하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- disables the 'Fran??ois Ajenstat' operator  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'Fran??ois Ajenstat',  
        @enabled = 0;  
    GO  
    ```  
  
 자세한 내용은 [sp_update_operator &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-operator-transact-sql)합니다.  
  
  
