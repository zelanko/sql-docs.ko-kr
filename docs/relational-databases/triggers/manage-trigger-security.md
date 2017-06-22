---
title: "트리거 보안 관리 | Microsoft 문서"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d86813b142cbd85527fb1e4e1c11d87884258ecf
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="manage-trigger-security"></a>트리거 보안 관리
  기본적으로 두 DML 및 DDL 트리거는 트리거를 호출하는 사용자의 컨텍스트에서 모두 실행됩니다. 트리거 호출자는 트리거를 실행시키는 문을 실행하는 사용자입니다. 예를 들어 **Mary** 라는 사용자가 DML 트리거 **DML_trigMary** 를 실행시키는 DELETE 문을 실행하면 **DML_trigMary** 내에 있는 코드는 **Mary**에 대한 사용자 권한 컨텍스트에서 실행됩니다. 이러한 기본 동작은 데이터베이스나 서버 인스턴스에 악의적인 코드를 침투시키려는 사용자가 이용할 수 있습니다. 예를 들어 다음 DDL 트리거는 `JohnDoe`라는 사용자가 만든 것입니다.  
  
 `CREATE TRIGGER DDL_trigJohnDoe`  
  
 `ON DATABASE`  
  
 `FOR ALTER_TABLE`  
  
 `AS`  
  
 `GRANT CONTROL SERVER TO JohnDoe ;`  
  
 `GO`  
  
 이 트리거는 `GRANT CONTROL SERVER` sysadmin **고정 서버 역할의 멤버처럼** 문을 실행할 권한이 있는 사용자가 `ALTER TABLE` 문을 실행하면 바로 `JohnDoe` 에게 `CONTROL SERVER` 권한이 부여됨을 의미합니다. 즉, `JohnDoe` 는 `CONTROL SERVER` 권한을 자신에게 부여할 수 없지만 자신에게 이 권한을 부여한 트리거 코드가 에스컬레이션된 권한으로 실행될 수 있도록 설정했습니다. DML과 DDL 트리거 모두 이러한 유형의 보안 위협에 노출되어 있습니다.  
  
## <a name="trigger-security-best-practices"></a>트리거 보안을 위한 가장 적절한 방법  
 다음 방법을 사용하여 트리거 코드가 에스컬레이션된 권한으로 실행되는 것을 방지할 수 있습니다.  
  
-   [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) 및 [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md) 카탈로그 뷰를 쿼리하여 데이터베이스 및 서버 인스턴스에 있는 DML 및 DDL 트리거를 확인합니다. 다음 쿼리는 현재 데이터베이스에 모든 DML 및 데이터베이스 수준 DDL 트리거를 반환하고 서버 인스턴스에 모든 서버 수준 DDL 트리거를 반환합니다.  
  
    ```  
    SELECT type, name, parent_class_desc FROM sys.triggers  
    UNION  
    SELECT type, name, parent_class_desc FROM sys.server_triggers ;  
    ```  
  
-   [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) 를 사용하여 트리거가 에스컬레이션된 권한으로 실행되는 경우 데이터베이스나 서버의 무결성에 손상을 줄 수 있는 트리거를 비활성화할 수 있습니다. 다음 문은 현재 데이터베이스에서 모든 데이터베이스 수준 DDL 트리거를 비활성화합니다.  
  
    ```  
    DISABLE TRIGGER ALL ON DATABASE  
    ```  
  
     이 문은 서버 인스턴스에서 모든 서버 수준 DDL 트리거를 비활성화합니다.  
  
    ```  
    DISABLE TRIGGER ALL ON ALL SERVER  
    ```  
  
     이 문은 현재 데이터베이스에서 모든 DML 트리거를 비활성화합니다.  
  
    ```  
    DECLARE @schema_name sysname, @trigger_name sysname, @object_name sysname ;  
    DECLARE @sql nvarchar(max) ;  
    DECLARE trig_cur CURSOR FORWARD_ONLY READ_ONLY FOR  
        SELECT SCHEMA_NAME(schema_id) AS schema_name,  
            name AS trigger_name,  
            OBJECT_NAME(parent_object_id) as object_name  
        FROM sys.objects WHERE type in ('TR', 'TA') ;  
  
    OPEN trig_cur ;  
    FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        SELECT @sql = 'DISABLE TRIGGER ' + QUOTENAME(@schema_name) + '.'  
            + QUOTENAME(@trigger_name) +  
            ' ON ' + QUOTENAME(@schema_name) + '.'   
            + QUOTENAME(@object_name) + ' ; ' ;  
        EXEC (@sql) ;  
        FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
    END  
    GO  
  
    -- Verify triggers are disabled. Should return an empty result set.  
    SELECT * FROM sys.triggers WHERE is_disabled = 0 ;  
    GO  
  
    CLOSE trig_cur ;  
    DEALLOCATE trig_cur;  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DML 트리거](../../relational-databases/triggers/dml-triggers.md)   
 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)  
  
  
