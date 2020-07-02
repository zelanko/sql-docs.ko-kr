---
title: 어셈블리 삭제 | Microsoft Docs
description: 더 이상 필요 하지 않을 때 SQL Server에서 어셈블리를 삭제 하거나 삭제할 수 있습니다. DROP ASSEMBLY를 사용 하 여 어셈블리 및 관련 파일을 제거 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- assemblies [CLR integration], removing
- dropping assemblies
ms.assetid: 03481034-dc91-4488-ab24-ba44243e2690
author: rothja
ms.author: jroth
ms.openlocfilehash: 94482a0776f69dd3477c298b519dc5b47fa7dcd1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727655"
---
# <a name="dropping-an-assembly"></a>어셈블리 삭제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  CREATE ASSEMBLY 문을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 등록한 어셈블리에서 제공하는 기능이 더 이상 필요 없는 경우 이 어셈블리를 삭제할 수 있습니다. 어셈블리를 삭제하면 데이터베이스에서 어셈블리뿐 아니라 디버그 파일 등의 모든 관련 파일이 제거됩니다. 어셈블리를 삭제하려면 DROP ASSEMBLY 문을 다음 구문으로 사용합니다.  
  
```  
DROP ASSEMBLY MyDotNETAssembly  
```  
  
 DROP ASSEMBLY는 현재 실행되고 있는 어셈블리를 참조하는 코드를 방해하지 않지만 DROP ASSEMBLY를 실행한 후 해당 어셈블리 코드를 호출하려고 하면 실패합니다.  
  
 어셈블리가 데이터베이스에 있는 다른 어셈블리에서 참조되거나 현재 데이터베이스의 CLR(공용 언어 런타임) 함수, 프로시저, 트리거, UDT(사용자 정의 형식) 또는 UDA(사용자 정의 집계)에서 사용되면 DROP ASSEMBLY가 오류를 반환합니다. 먼저 DROP AGGREGATE, DROP FUNCTION, DROP PROCEDURE, DROP TRIGGER 및 DROP TYPE 문을 사용하여 어셈블리에 포함된 관리되는 데이터베이스 개체를 삭제합니다.  
  
## <a name="removing-a-udt-from-the-database"></a>데이터베이스에서 UDT 제거  
 DROP TYPE 문은 현재 데이터베이스에서 UDT를 제거합니다. UDT를 삭제한 경우 DROP ASSEMBLY 문을 사용하여 데이터베이스에서 어셈블리를 삭제할 수 있습니다.  
  
 다음과 같이 개체가 UDT에 종속되어 있으면 DROP TYPE 문이 실패합니다.  
  
-   UDT를 사용하여 정의한 열이 포함된 데이터베이스의 테이블  
  
-   데이터베이스에 WITH SCHEMABINDING 절로 만든 함수, 저장 프로시저 또는 트리거가 있고 이러한 루틴이 UDT의 변수 또는 매개 변수를 사용하는 경우  
  
### <a name="finding-udt-dependencies"></a>UDT 종속성 찾기  
 따라서 먼저 모든 종속 개체를 삭제한 다음 DROP TYPE 문을 실행해야 합니다. 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리는 **AdventureWorks** 데이터베이스에서 UDT를 사용 하는 모든 열과 매개 변수를 찾습니다.  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;   
```  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 어셈블리 관리](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [어셈블리 변경](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [어셈블리 만들기](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [DROP AGGREGATE &#40;Transact-sql&#41;](../../../t-sql/statements/drop-aggregate-transact-sql.md)   
 [DROP FUNCTION &#40;Transact-sql&#41;](../../../t-sql/statements/drop-function-transact-sql.md)   
 [DROP PROCEDURE &#40;Transact-sql&#41;](../../../t-sql/statements/drop-procedure-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-trigger-transact-sql.md)   
 [DROP TYPE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-type-transact-sql.md)  
  
  
