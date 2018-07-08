---
title: 저장 프로시저에 대한 사용 권한 부여 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], permissions
ms.assetid: a7d15816-a788-4099-ad91-dc4b26618299
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4e811af7aa55fc6ced619d1a69347867bf2aef05
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150404"
---
# <a name="grant-permissions-on-a-stored-procedure"></a>저장 프로시저에 대한 사용 권한 부여
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 저장 프로시저에 대한 사용 권한을 부여하는 방법에 대해 설명합니다. 데이터베이스의 기존 사용자, 데이터베이스 역할 또는 응용 프로그램 역할에 사용 권한을 부여할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **저장 프로시저에 대한 사용 권한을 부여하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 시스템 프로시저나 시스템 함수에 대한 사용 권한을 부여할 수 없습니다. 이 경우 [GRANT Object Permissions](/sql/t-sql/statements/grant-object-permissions-transact-sql) 를 사용하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다. 프로시저가 속한 스키마에 대한 ALTER 권한 또는 프로시저에 대한 CONTROL 권한이 필요합니다. 자세한 내용은 [GRANT 개체 사용 권한&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql)을 사용하여 저장 프로시저에 대한 사용 권한을 부여하는 방법에 대해 설명합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-grant-permissions-on-a-stored-procedure"></a>저장 프로시저에 대한 사용 권한을 부여하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 프로시저가 속한 데이터베이스를 확장한 다음 **프로그래밍 기능**을 확장합니다.  
  
3.  **저장 프로시저**를 확장하고 사용 권한을 부여할 프로시저를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **저장 프로시저 속성**에서 **사용 권한** 페이지를 선택합니다.  
  
5.  사용자, 데이터베이스 역할 또는 응용 프로그램 역할에 사용 권한을 부여하려면 **검색**을 클릭합니다.  
  
6.  **사용자 또는 역할 선택**에서 **개체 유형** 을 클릭하여 원하는 사용자 및 역할을 추가하거나 지웁니다.  
  
7.  **찾아보기** 를 클릭하여 사용자 또는 역할의 목록을 표시합니다. 사용 권한을 부여할 사용자 또는 역할을 선택합니다.  
  
8.  **명시적 사용 권한** 표에서 지정된 사용자 또는 역할에 부여할 사용 권한을 선택합니다. 사용 권한에 대한 설명은 [사용 권한&#40;데이터베이스 엔진&#41;](../security/permissions-database-engine.md)을 참조하세요.  
  
 **허용** 을 선택하면 지정된 사용 권한이 피부여자에게 제공됩니다. **허용 권한 소유** 를 선택하면 피부여자가 지정된 사용 권한을 다른 보안 주체에 부여할 수도 있습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-grant-permissions-on-a-stored-procedure"></a>저장 프로시저에 대한 사용 권한을 부여하려면  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `EXECUTE` 이라는 응용 프로그램 역할에 대해 저장 프로시저 `HumanResources.uspUpdateEmployeeHireInfo` 에 대한 `Recruiting11`권한을 부여합니다.  
  
```tsql  
USE AdventureWorks2012;   
GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)   
 [GRANT 개체 사용 권한&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql)   
 [저장 프로시저 만들기](../stored-procedures/create-a-stored-procedure.md)   
 [저장 프로시저 수정](modify-a-stored-procedure.md)   
 [저장 프로시저 삭제](../stored-procedures/delete-a-stored-procedure.md)   
 [저장 프로시저 이름 바꾸기](rename-a-stored-procedure.md)  
  
  
