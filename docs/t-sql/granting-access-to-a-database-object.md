---
title: "데이터베이스 개체에 대한 액세스 권한 부여 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "데이터베이스 개체에 대한 액세스 권한 부여"
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 데이터베이스 개체에 대한 액세스 권한 부여
관리자는 **Products** 테이블 및 **vw_Names** 뷰에서 SELECT를 실행하고 **pr_Names** 프로시저를 실행할 수 있지만 Mary는 이러한 작업을 수행할 수 없습니다. Mary에게 필요한 사용 권한을 부여하려면 GRANT 문을 사용합니다.  
  
### 절차 제목  
  
1.  다음 문을 실행하여 `Mary` 저장 프로시저에 대한 `EXECUTE` 권한을 `pr_Names` 에게 제공합니다.  
  
    ```  
    GRANT EXECUTE ON pr_Names TO Mary;  
    GO  
    ```  
  
이 시나리오에서 Mary는 이 저장 프로시저를 사용하여 **Products** 테이블에만 액세스할 수 있습니다. Mary가 SELECT 문을 뷰에 대해 실행할 수 있도록 하려면 또한 `GRANT SELECT ON vw_Names TO Mary`를 실행해야 합니다. 데이터베이스 개체에 대한 액세스 권한을 제거하려면 REVOKE 문을 사용합니다.  
  
> [!NOTE]  
> 테이블, 뷰 및 저장 프로시저를 동일한 스키마에서 소유하지 않을 경우 사용 권한을 부여하는 것은 더 복잡해집니다.  
  
## GRANT 정보  
저장 프로시저를 실행하려면 EXECUTE 권한이 있어야 합니다. 데이터를 액세스 및 변경하려면 SELECT, INSERT, UPDATE 및 DELETE 권한이 있어야 합니다. 또한 GRANT 문은 테이블 작성 권한과 같은 다른 사용 권한에도 사용됩니다.  
  
## 단원의 다음 태스크  
[요약: 데이터베이스 개체에 대한 사용 권한 구성](../t-sql/summary-configuring-permissions-on-database-objects.md)  
  
## 관련 항목:  
[GRANT&#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)  
[REVOKE&#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
  
  
  
