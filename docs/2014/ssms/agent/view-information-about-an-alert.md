---
title: 경고에 대한 정보 보기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9324249df2f96bf7ddf2a94b199cdfcfe003cb55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181936"
---
# <a name="view-information-about-an-alert"></a>View Information About an Alert
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고에 대한 정보를 보는 방법을 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 경고에 대한 정보를 봅니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버가 경고의 정보를 볼 수 있습니다. 다른 사용자는 **msdb** 데이터베이스의 **SQLAgentOperatorRole** 고정 데이터베이스 역할을 부여 받아야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-information-about-an-alert"></a>경고에 대한 정보를 보려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 경고에 대한 정보를 보려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **경고** 폴더를 확장합니다.  
  
4.  보려는 정보가 포함된 경고를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     *alert_name***경고 속성** 대화 상자에 포함된 사용 가능한 옵션에 대한 자세한 내용은 다음을 참조하세요.  
  
    -   [속성-새 경고를 경고 &#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
    -   [속성-새 경고를 경고 &#40;응답 페이지&#41;](alert-properties-new-alert-response-page.md)  
  
    -   [경고 속성: 새 경고 &#40;옵션 페이지&#41;](alert-properties-new-alert-options-page.md)  
  
    -   [경고 속성&#40;기록 페이지&#41;](alert-properties-history-page.md)  
  
5.  완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-information-about-an-alert"></a>경고에 대한 정보를 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- reports information about the Demo: Sev. 25 Errors alert  
    -- This example assumes that the 'Demo: Sev. 25 Errors' alert exists.  
    USE msdb ;  
    GO  
  
    EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors'  
    GO  
    ```  
  
 자세한 내용은 참조 [sp_help_alert &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-alert-transact-sql)합니다.  
  
  
