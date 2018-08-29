---
title: 보안 주체에게 사용 권한 부여 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Grant permission to a principal
ms.assetid: 4107389d-05b6-4aa3-9fa8-95b40cdf05dc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a96147180fb0b76869bcf97b6a327f64dd5d6e26
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036044"
---
# <a name="grant-a-permission-to-a-principal"></a>보안 주체에게 사용 권한 부여
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 보안 주체에 권한을 부여하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 보안 주체에 대한 사용 권한을 부여합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 사용 권한을 보다 쉽게 관리할 수 있도록 다음과 같은 최선의 구현 방법을 고려하세요.  
  
-   개별 로그인 또는 사용자 대신 역할에 사용 권한을 부여합니다. 사용자가 바뀌는 경우 떠나는 사용자를 역할에서 제거하고 새 사용자를 역할에 추가합니다. 새로운 사용자는 해당 역할에 연결된 많은 사용 권한을 자동으로 갖게 됩니다. 조직 내 여러 사람에게 동일한 사용 권한이 필요한 경우 각 사람을 역할에 추가함으로써 동일한 사용 권한을 부여할 수 있습니다.  
  
-   유사한 보안 개체(테이블, 뷰 및 프로시저)를 스키마가 소유하도록 구성한 후 해당 스키마에 대한 사용 권한을 부여합니다. 예를 들어 급여 스키마는 여러 테이블, 뷰 및 저장 프로시저를 소유할 수 있습니다. 스키마에 액세스 권한을 부여하면 급여 기능을 수행하는 데 필요한 모든 사용 권한을 동시에 부여할 수 있습니다. 사용 권한을 부여받을 수 있는 보안 개체에 대한 자세한 내용은 [Securables](../securables.md)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다. **sysadmin** 고정 서버 역할의 멤버는 모든 사용 권한을 부여할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-grant-permission-to-a-principal"></a>보안 주체에 사용 권한을 부여하려면  
  
1.  개체 탐색기에서 사용 권한을 부여하려는 개체가 포함된 데이터베이스를 확장합니다.  
  
    > [!NOTE]  
    >  이러한 단계는 특히 저장 프로시저에 대한 권한 부여를 처리하지만 비슷한 단계에서도 다른 보안 개체뿐만 아니라 테이블, 뷰, 함수 및 어셈블리에 사용 권한을 추가할 수 있습니다. 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)를 참조하세요.  
  
2.  **프로그래밍 기능** 폴더를 확장합니다.  
  
3.  **저장 프로시저** 폴더를 확장합니다.  
  
4.  저장 프로시저를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
5.  *저장 프로시저 속성 –***stored_procedure_name* 대화 상자에서 페이지를 선택하고 **사용 권한**을 선택합니다. 이 페이지에서는 저장 프로시저에 사용자 또는 역할을 추가하고 해당 사용자 또는 역할이 포함할 사용 권한을 지정할 수 있습니다.  
  
6.  완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-grant-permission-to-a-principal"></a>보안 주체에 사용 권한을 부여하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Grants EXECUTE permission on stored procedure HumanResources.uspUpdateEmployeeHireInfo to an application role called Recruiting11.   
    USE AdventureWorks2012;  
    GO  
    GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
        TO Recruiting11;  
    GO  
    ```  
  
 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql) 및 [GRANT 개체 사용 권한&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [보안 주체&#40;데이터베이스 엔진&#41;](principals-database-engine.md)  
  
  
