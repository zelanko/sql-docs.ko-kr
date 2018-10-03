---
title: default full-text language 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- default full-text language option
ms.assetid: 0fa8785b-0830-4a52-aff5-fcf8268b72fc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 575acd7d4fb264ebb8cba218c1e37b45e9af5a33
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062963"
---
# <a name="configure-the-default-full-text-language-server-configuration-option"></a>default full-text language 서버 구성 옵션 구성
  이 항목에서는 구성 하는 방법에 설명 합니다 `default full-text language` 서버 구성 옵션에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용 하 여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. `default full-text language` 옵션 전체 텍스트 인덱스에 대 한 기본 언어 값을 지정 합니다. 언어 분석은 전체 텍스트 인덱싱된 모든 데이터에 대해 수행되고 해당 데이터 언어에 따라 달라집니다. 이 옵션의 기본값은 서버의 언어입니다. 지역화 된 버전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 집합을 설치 합니다 `default full-text language` 적절 한 일치 하는 경우 서버의 언어 옵션입니다. 지역화 되지 않은 버전용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `default full-text language` 옵션이 영어입니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **기본 전체 텍스트 언어 옵션을 구성하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [기본 전체 텍스트 언어 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   값을 `default full-text language` 옵션은 언어를 통해 열에 없는 언어를 지정 하는 경우 전체 텍스트 인덱스에 사용 됩니다 **language_term** CREATE FULLTEXT INDEX 문이나 ALTER FULLTEXT INDEX 문에서 옵션입니다. 기본 전체 텍스트 언어가 지원되지 않거나 언어 분석 패키지를 사용할 수 없으면 CREATE 또는 ALTER 작업이 실패하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 지정된 언어가 올바르지 않다는 내용의 오류 메시지를 반환합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
-   `default full-text language` 옵션은 LCID 값이 필요 합니다. 지원되는 LCID 및 해당 관련 언어 목록을 보려면 [sys.fulltext_languages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)서버 구성 옵션을 구성하는 방법을 설명합니다. ISV(Independent Software Vendor) 등에서 제공하는 다른 언어를 사용할 수도 있습니다. 특정 언어를 찾을 수 없으면 전체 텍스트 검색 엔진에서 주 언어로 자동 전환합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
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
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예제에서는 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 를 사용하여 `default full-text` 옵션의 값을 Dutch(`1043`)로 설정하는 방법을 보여 줍니다.  
  
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
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)서버 구성 옵션을 구성하는 방법을 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 기본 전체 텍스트 언어 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.fulltext_languages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
