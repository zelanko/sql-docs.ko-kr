---
title: "default full-text language 서버 구성 옵션 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- languages [full-text search]
- default full-text language option
ms.assetid: 0fa8785b-0830-4a52-aff5-fcf8268b72fc
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e910e8adf908fefc54f40b939bce107b3a32009b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="configure-the-default-full-text-language-server-configuration-option"></a>default full-text language 서버 구성 옵션 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 기본 전체 텍스트 언어 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법을 설명합니다. **기본 전체 텍스트 언어** 옵션은 전체 텍스트 인덱스에 대한 기본 언어 값을 지정합니다. 언어 분석은 전체 텍스트 인덱싱된 모든 데이터에 대해 수행되고 해당 데이터 언어에 따라 달라집니다. 이 옵션의 기본값은 서버의 언어입니다. 지역화된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 경우 일치하는 언어가 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 **default full-text language** 옵션을 서버 언어로 설정합니다. 지역화되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 경우 **default full-text language** 옵션이 영어입니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **기본 전체 텍스트 언어 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [기본 전체 텍스트 언어 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   CREATE FULLTEXT INDEX 문이나 ALTER FULLTEXT INDEX 문에서 LANGUAGE **language_term** 옵션을 통해 열에 언어가 지정되지 않은 경우 **기본 전체 텍스트 언어** 옵션의 값이 전체 텍스트 인덱스에 사용됩니다. 기본 전체 텍스트 언어가 지원되지 않거나 언어 분석 패키지를 사용할 수 없으면 CREATE 또는 ALTER 작업이 실패하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 지정된 언어가 올바르지 않다는 내용의 오류 메시지를 반환합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
-   **기본 전체 텍스트 언어** 옵션에는 LCID 값이 필요합니다. 지원되는 LCID 및 해당 관련 언어 목록을 보려면 [sys.fulltext_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)서버 구성 옵션을 구성하는 방법을 설명합니다. ISV(Independent Software Vendor) 등에서 제공하는 다른 언어를 사용할 수도 있습니다. 특정 언어를 찾을 수 없으면 전체 텍스트 검색 엔진에서 주 언어로 자동 전환합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>기본 전체 텍스트 언어 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **고급** 노드를 클릭합니다.  
  
3.  기타의 **기본 전체 텍스트 언어** 를 사용하여 전체 텍스트가 인덱싱된 열의 기본 언어 값을 지정할 수 있습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>기본 전체 텍스트 언어 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예제에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 사용하여 `default full-text` 옵션의 값을 Dutch(`1043`)로 설정하는 방법을 보여 줍니다.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'default full-text language', 1043 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 구성하는 방법을 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 기본 전체 텍스트 언어 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.fulltext_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  

