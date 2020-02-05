---
title: 정책 기반 관리의 일반 속성 구성
description: SSMS(SQL Server Management Studio) 또는 T-SQL(Transact-SQL)을 사용하여 정책 기반 관리의 속성을 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.PolicyManagement.f1
helpviewer_keywords:
- Policy-Based Management, configure properties
ms.assetid: 6d1e0e37-29ea-408a-a055-384984d884be
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c2d431fd1b04f046fb00f131a1a77a146570b50f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558158"
---
# <a name="configure-the-general-properties-of-policy-based-management"></a>정책 기반 관리의 일반 속성 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 정책 기반 관리에 대한 속성을 구성하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 정책 기반 관리를 구성하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 PolicyAdministratorRole 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-policy-based-management"></a>정책 기반 관리를 구성하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 정책 기반 관리 속성을 구성하려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  **정책 관리자** 를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     다음 옵션은 **정책 관리 속성** 대화 상자에서 사용할 수 있습니다.  
  
     **Enabled**  
     정책 기반 관리 사용 여부를 지정합니다.  
  
     **HistoryRetentionInDays**  
     정책 평가 기록을 보관할 일 수를 지정합니다. 이 값이 0(기본값)이면 기록이 자동으로 제거되지 않습니다.  
  
     **LogOnSuccess**  
     정책 기반 관리에서 성공한 정책 평가를 기록할지 여부를 지정합니다.  
  
    -   이 값이 false(기본값)이면 실패한 정책 평가만 기록됩니다.  
  
    -   이 값이 true이면 성공한 정책 평가와 실패한 정책 평가가 모두 기록됩니다.  
  
4.  완료되었으면 **확인**을 클릭합니다.  

##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-policy-based-management"></a>정책 기반 관리를 구성하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- enables Policy-Based Management   
    USE msdb;  
    GO  
    EXEC dbo.sp_syspolicy_configure   
         @name = N'Enabled',   
         @value = 1;  
    GO  
    ```  
  
 자세한 내용은 [sp_syspolicy_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md)를 참조하세요.  
  
  
