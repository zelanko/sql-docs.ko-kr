---
title: "정책 범주에 데이터베이스 구독 또는 구독 취소 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.dmf.groupsubscription.f1
ms.assetid: d2c31769-7098-428e-ad9c-ef56541b7c52
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a1a01148b8d68f096b1e4cfba9fde209c7127c4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="subscribe-or-unsubscribe-a-database--to-a-policy-category"></a>정책 범주에 데이터베이스 구독 또는 구독 취소
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 데이터베이스에 정책 범주를 구독하거나 구독 취소하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 데이터베이스에 정책 범주를 구독하거나 구독 취소하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-subscribe-or-unsubscribe-a-database-to-a-policy-category"></a>데이터베이스에 정책 범주를 구독하거나 구독 취소하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 범주 구독을 관리할 데이터베이스를 포함하는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **데이터베이스** 폴더를 확장합니다.  
  
3.  범주 구독을 관리할 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **정책**을 가리킨 다음 **범주**를 선택합니다.  
  
     **범주** 대화 상자에서 사용 가능한 옵션은 다음과 같습니다.  
  
     열 확장  
     정책 범주를 확장하려면 클릭합니다. 그러면 범주에 포함된 모든 정책이 표시됩니다.  
  
     **이름**  
     정책 범주의 이름입니다.  
  
     **구독**  
     대상이 정책 범주로 구독되는지 여부를 나타냅니다. 이 확인란을 해제하면 **데이터베이스 구독 위임**에 대한 정책 범주가 설정됩니다. 즉, 서버의 모든 데이터베이스에 정책 범주가 적용됩니다.  
  
     **정책**  
     정책 그룹이 확장되면 정책 범주의 정책이 표시됩니다.  
  
     **설정**  
     정책의 사용 여부를 나타냅니다.  
  
     **실행 모드**  
     정책의 실행 모드를 표시합니다.  
  
     **기록**  
     로그 파일 뷰어를 열어 정책 기록을 보려면 기록 보기 하이퍼링크를 클릭합니다.  
  
4.  정책 기반 관리 범주를 구독하려면 **가입** 열 아래의 범주 확인란을 선택합니다. 범주에서 구독을 취소하려면 해당 확인란의 선택을 취소합니다.  
  
5.  완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-subscribe-a-database-to-a-policy-category"></a>데이터베이스에 정책 범주를 구독하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    -- Adds a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 자세한 내용은 [sp_syspolicy_subscribe_to_policy_category&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql.md)를 참조하세요.  
  
#### <a name="to-unsubscribe-a-database-to-a-policy-category"></a>데이터베이스에서 정책 범주를 구독 취소하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    -- Deletes a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 자세한 내용은 [sp_syspolicy_unsubscribe_from_policy_category&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)를 참조하세요.  
  
  
