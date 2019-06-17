---
title: 데이터베이스 개체 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: dbb94fdf-c85b-477b-8e84-f830d259bade
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a23d307cc33e5b8e59111819b245bc9df1df67df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63063123"
---
# <a name="deleting-database-objects"></a>데이터베이스 개체 삭제
  이 자습서의 모든 추적 내용을 제거하려면 데이터베이스를 삭제하기만 하면 됩니다. 그러나 이 항목에서는 자습서에서 수행한 모든 동작을 되돌리는 단계를 진행합니다.  
  
### <a name="removing-permissions-and-objects"></a>사용 권한 및 개체 제거  
  
1.  개체를 삭제하기 전에 사용자가 올바른 데이터베이스에 있는지 확인합니다.  
  
    ```  
    USE TestData;  
    GO  
    ```  
  
2.  `REVOKE` 문을 사용하여 저장 프로시저에 대한 `Mary` 의 실행 권한을 제거합니다.  
  
    ```  
    REVOKE EXECUTE ON pr_Names FROM Mary;  
    GO  
  
    ```  
  
3.  `DROP` 문을 사용하여 `Mary` 가 `TestData` 데이터베이스에 액세스할 수 있는 권한을 제거합니다.  
  
    ```  
    DROP USER Mary;  
    GO  
  
    ```  
  
4.  `DROP` 문을 사용하여 `Mary` 가 이 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]인스턴스에 액세스할 수 있는 권한을 제거합니다.  
  
    ```  
    DROP LOGIN [<computer_name>\Mary];  
    GO  
  
    ```  
  
5.  `DROP` 문을 사용하여 `pr_Names`저장 프로시저를 제거합니다.  
  
    ```  
    DROP PROC pr_Names;  
    GO  
  
    ```  
  
6.  `DROP` 문을 사용하여 `vw_Names`뷰를 제거합니다.  
  
    ```  
    DROP View vw_Names;  
    GO  
  
    ```  
  
7.  `DELETE` 문을 사용하여 `Products` 테이블에서 모든 행을 제거합니다.  
  
    ```  
    DELETE FROM Products;  
    GO  
  
    ```  
  
8.  `DROP` 문을 사용하여 `Products` 테이블을 제거합니다.  
  
    ```  
    DROP Table Products;  
    GO  
  
    ```  
  
9. 사용자가 `TestData` 데이터베이스에 있는 동안에는 이 데이터베이스를 제거할 수 없습니다. 따라서 먼저 컨텍스트를 다른 데이터베이스로 전환한 다음 `DROP` 문을 사용하여 `TestData` 데이터베이스를 제거합니다.  
  
    ```  
    USE MASTER;  
    GO  
    DROP DATABASE TestData;  
    GO  
  
    ```  
  
 이것으로 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 작성 자습서를 마칩니다. 이 자습서는 간략한 개요이므로 사용된 문에 대한 모든 옵션을 설명하지는 않습니다. 효율적인 데이터베이스 구조를 디자인 및 작성하고 데이터에 대한 보안 액세스를 구성하려면 이 자습서의 예제 데이터베이스보다 복잡한 데이터베이스가 필요합니다.  
  
## <a name="return-to-sql-server-tools-portal"></a>SQL Server 도구 포털로 돌아가기  
 [자습서: Transact-SQL 문 작성](tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>관련 항목  
 [REVOKE&#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DROP USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-user-transact-sql)   
 [DROP LOGIN&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-login-transact-sql)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)   
 [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)   
 [DELETE&#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)   
 [DROP TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql)   
 [DROP DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)  
  
  
