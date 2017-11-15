---
title: "저장 프로시저 실행 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.executeprocedure.general.f1
- sql13.swb.executeprocedure.f1
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- extended stored procedures [SQL Server], executing
- system stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- user-defined stored procedures [SQL Server]
ms.assetid: a0b1337d-2059-4872-8c62-3f967d8b170f
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: fe339b35fb469842419fbc9e0d9b52be0c66595e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="execute-a-stored-procedure"></a>저장 프로시저 실행

 > 이전 버전의 SQL Server와 관련 된 콘텐츠를 참조 하십시오. [저장 프로시저를 실행할](https://msdn.microsoft.com/en-US/library/ms189915(SQL.120).aspx)합니다.

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 저장 프로시저를 실행하는 방법에 대해 설명합니다.  
  
 두 가지 방법으로 저장 프로시저를 실행할 수 있습니다. 가장 일반적인 첫 번째 방법은 응용 프로그램 또는 사용자가 프로시저를 호출하는 것입니다. 두 번째 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작될 때 자동 실행되도록 프로시저를 설정하는 것입니다. 응용 프로그램이나 사용자가 프로시저를 호출할 때 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 또는 EXEC 키워드가 호출에서 명시적으로 지정됩니다. 또는 프로시저가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 첫 번째 문이면 키워드를 사용하지 않고 프로시저를 호출하고 실행할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **저장 프로시저를 실행하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   시스템 프로시저 이름을 일치시킬 때 호출 데이터베이스 데이터 정렬이 사용됩니다. 따라서 프로시저 호출에서 대/소문자를 구분하여 시스템 프로시저 이름을 항상 정확하게 지정해야 합니다. 예를 들어 다음 코드는 대/소문자를 구분하는 데이터 정렬을 사용하는 데이터베이스 컨텍스트에서 실행할 경우 실패합니다.  
  
    ```tsql  
    EXEC SP_heLP; -- Will fail to resolve because SP_heLP does not equal sp_help  
    ```  
  
     정확한 시스템 프로시저 이름을 표시하려면 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 및 [sys.system_parameters](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md) 카탈로그 뷰를 쿼리합니다.  
  
-   사용자 정의 프로시저의 이름이 시스템 프로시저의 이름과 같으면 사용자 정의 프로시저가 실행되지 않을 수도 있습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   시스템 저장 프로시저 실행  
  
     시스템 프로시저는 접두사 **sp_**로 시작합니다. 시스템 프로시저는 모든 사용자 정의 데이터베이스와 시스템 정의 데이터베이스에 논리적으로 나타나기 때문에 프로시저 이름을 완전히 한정하지 않고도 모든 데이터베이스에서 시스템 프로시저를 실행할 수 있습니다. 그러나 이름 충돌이 발생하지 않도록 **sys** 스키마 이름으로 모든 시스템 프로시저 이름을 스키마로 한정하는 것이 좋습니다. 다음 예에서는 권장되는 시스템 프로시저 호출 방법을 보여 줍니다.  
  
    ```tsql  
    EXEC sys.sp_who;  
    ```  
  
-   사용자 정의 저장 프로시저 실행  
  
     사용자 정의 프로시저를 실행할 때 프로시저 이름을 스키마 이름으로 한정하는 것이 좋습니다. 이렇게 하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 여러 스키마를 검색할 필요가 없기 때문에 성능이 약간 향상됩니다. 또한 데이터베이스에 여러 스키마에서 이름이 동일한 프로시저가 있는 경우 잘못된 프로시저를 실행하는 문제가 방지됩니다.  
  
     다음 예에서는 권장되는 사용자 정의 프로시저 실행 방법을 보여 줍니다. 프로시저는 하나의 입력 매개 변수를 받아들입니다. 입력 및 출력 매개 변수를 지정하는 방법은 [매개 변수 지정](../../relational-databases/stored-procedures/specify-parameters.md)을 참조하세요.  
  
    ```tsql  
    USE AdventureWorks2012;  
    GO  
    EXEC dbo.uspGetEmployeeManagers @BusinessEntityID = 50;  
    ```  
  
     -또는-  
  
    ```tsql  
    EXEC AdventureWorks2012.dbo.uspGetEmployeeManagers 50;  
    GO  
    ```  
  
     정규화되지 않은 사용자 정의 프로시저를 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 다음 순서로 프로시저를 검색합니다.  
  
    1.  현재 데이터베이스의 **sys** 스키마  
  
    2.  일괄 처리나 동적 SQL에서 실행된 경우 호출자의 기본 스키마. 또는 다른 프로시저 정의 본문에 한정되지 않은 프로시저 이름이 있는 경우 이 다른 프로시저를 포함하는 스키마가 다음으로 검색됩니다.  
  
    3.  현재 데이터베이스의 **dbo** 스키마  
  
-   저장 프로시저 자동 실행  
  
     자동 실행되도록 표시된 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작될 때마다 실행되며 **master** 데이터베이스는 이 시작 프로세스 중에 복구됩니다. 자동 실행되도록 프로시저를 설정하면 데이터베이스 유지 관리 작업을 수행하거나 프로시저가 백그라운드 프로세스로 계속 실행되도록 하는 데 유용할 수 있습니다. 또는 프로시저가 전역 임시 테이블을 만드는 작업처럼 **tempdb**에서 시스템 또는 유지 관리 태스크를 수행하도록 하는 것이 자동 실행을 사용하는 또 다른 방법입니다. 이렇게 하면 **시작 중에** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다시 만들어질 때 이러한 임시 테이블이 항상 존재합니다.  
  
     자동 실행되는 프로시저는 **sysadmin** 고정 서버 역할의 멤버와 같은 권한을 사용하여 작동합니다. 프로시저에서 생성되는 오류 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 기록됩니다.  
  
     시작 프로시저의 개수에는 제한이 없지만 각 시작 프로시저는 실행하는 동안 하나의 작업자 스레드를 소비합니다. 따라서 시작할 때 여러 프로시저를 실행해야 하지만 동시에 실행할 필요가 없다면 한 프로시저만 시작 프로시저로 지정하고 그 프로시저에서 다른 프로시저를 호출하도록 만듭니다. 이렇게 하면 하나의 작업자 스레드만 사용됩니다.  
  
    > [!TIP]  
    >  자동 실행되는 프로시저의 결과 집합은 반환하지 마세요. 프로시저는 응용 프로그램이나 사용자가 아닌 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 의해 실행되므로 결과 집합을 반환할 대상이 없습니다.  
  
-   자동 실행 설정, 해제 및 제어  
  
     시스템 관리자(**sa**)만 프로시저가 자동 실행되도록 표시할 수 있습니다. 또한 프로시저는 **master** 데이터베이스에 있고 **sa**에 의해 소유되어야 하며 입력 또는 출력 매개 변수를 가질 수 없습니다.  
  
     [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) 을 사용하여 다음을 수행할 수 있습니다.  
  
    1.  기존 프로시저를 시작 프로시저로 지정합니다.  
  
    2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작할 때 프로시저가 실행되지 않도록 합니다.  
  
###  <a name="Security"></a> 보안  
 자세한 내용은 [EXECUTE AS&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md) 및 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요.  
  
####  <a name="Permissions"></a> 사용 권한  
 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)을 사용하여 저장 프로시저를 실행하는 방법에 대해 설명합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-execute-a-stored-procedure"></a>저장 프로시저를 실행하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결하고 해당 인스턴스를 확장한 다음 **데이터베이스**를 확장합니다.  
  
2.  원하는 데이터베이스를 확장하고 **프로그래밍 기능**을 확장한 다음 **저장 프로시저**를 확장합니다.  
  
3.  원하는 사용자 정의 저장 프로시저를 마우스 오른쪽 단추로 클릭하고 **저장 프로시저 실행**을 클릭합니다.  
  
4.  **프로시저 실행** 대화 상자에서 각 매개 변수의 값과 null 값을 전달해야 하는지 여부를 지정합니다.  
  
     **매개 변수**  
     매개 변수의 이름을 나타냅니다.  
  
     **데이터 형식**  
     매개 변수의 데이터 형식을 나타냅니다.  
  
     **출력 매개 변수**  
     매개 변수가 출력 매개 변수인지 여부를 나타냅니다.  
  
     **Null 값 전달**  
     매개 변수의 값으로 NULL 값을 전달합니다.  
  
     **값**  
     프로시저를 호출할 때 매개 변수의 값을 입력합니다.  
  
5.  저장 프로시저를 실행하려면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-execute-a-stored-procedure"></a>저장 프로시저를 실행하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 하나의 매개 변수를 예상하는 저장 프로시저를 실행하는 방법을 보여 줍니다. 또한 `uspGetEmployeeManagers` 매개 변수로 지정된 값인  `6` 을 사용하여 `@EmployeeID` 저장 프로시저를 실행합니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
#### <a name="to-set-or-clear-a-procedure-for-executing-automatically"></a>자동 실행되도록 프로시저를 설정하거나 해제하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) 을 사용하여 자동 실행되도록 프로시저를 설정하는 방법을 보여 줍니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';  
```  
  
#### <a name="to-stop-a-procedure-from-executing-automatically"></a>프로시저가 자동 실행되는 것을 중지하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) 을 사용하여 프로시저가 자동 실행되는 것을 중지하는 방법을 보여 줍니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';  
```  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
  
## <a name="see-also"></a>참고 항목  
 [매개 변수 지정](../../relational-databases/stored-procedures/specify-parameters.md)   
 [scan for startup procs 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [저장 프로시저&#40;데이터베이스 엔진&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  
