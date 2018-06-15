---
title: DDL 트리거 구현 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: triggers
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, implementing
ms.assetid: f44e5340-1d18-40e9-828e-0ffcca091ae3
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b380884e3b80ea9d88f20ebd6f031d3dcf8e0cd5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33011450"
---
# <a name="implement-ddl-triggers"></a>DDL 트리거 구현
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  이 항목에서는 DDL 트리거 생성, DDL 트리거 수정, DDL 트리거 해제 또는 삭제 방법에 대한 정보를 제공합니다.  
  
## <a name="creating-ddl-triggers"></a>DDL 트리거 만들기  
 DDL 트리거는 DDL 트리거에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER 문을 사용하여 만듭니다.  
  
 **DDL 트리거를 만들려면**  
  
-   [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
> [!IMPORTANT]  
>  나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 트리거에서 결과 집합을 반환하는 기능이 제거됩니다. 결과 집합을 반환하는 트리거는 트리거가 작동하지 않는 응용 프로그램에 예기치 않은 동작을 유발할 수도 있습니다. 향후 개발 작업에서는 트리거에서 결과 집합을 반환하지 않도록 하고 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 트리거가 결과 집합을 반환하지 않도록 하려면 [disallow results from triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) 옵션을 1로 설정합니다. 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 옵션이 기본적으로 1로 설정됩니다.  
  
## <a name="modifying-ddl-triggers"></a>DDL 트리거 수정  
 트리거를 삭제하고 다시 만들거나 기존 트리거를 한 단계로 다시 정의하여 DDL 트리거 정의를 수정할 수 있습니다.  
  
 DDL 트리거가 참조하는 개체의 이름을 변경하는 경우 트리거 텍스트에 새 개체 이름이 반영되도록 트리거를 수정해야 합니다. 따라서 개체 이름을 바꾸기 전에는 먼저 개체의 종속성을 표시하여 영향을 받는 트리거가 있는지 확인해야 합니다.  
  
 트리거 정의를 암호화하도록 트리거가 수정될 수도 있습니다.  
  
 **트리거를 수정하려면**  
  
-   [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
 **트리거의 종속 관계를 보려면**  
  
-   [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
-   [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
-   [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
## <a name="disabling-and-dropping-ddl-triggers"></a>DDL 트리거 비활성화 및 삭제  
 더 이상 필요 없는 DDL 트리거는 비활성화하거나 삭제할 수 있습니다.  
  
 DDL 트리거를 비활성화해도 해당 트리거가 삭제되지 않으며 현재 데이터베이스의 개체로 남아 있습니다. 그러나 해당 트리거가 프로그래밍된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하는 경우에도 트리거는 발생되지 않습니다. DDL 트리거를 해제했다가 다시 설정할 수 있습니다. DDL 트리거를 설정하면 처음 만들었을 때와 동일한 방법으로 트리거가 발생됩니다. DDL 트리거를 만들면 기본적으로 설정됩니다.  
  
 DDL 트리거를 삭제하면 현재 데이터베이스에서 삭제됩니다. DDL 트리거가 적용된 개체 또는 데이터는 영향을 받지 않습니다.  
  
 **DDL 트리거를 비활성화하려면**  
  
-   [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)  
  
-   [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **DDL 트리거를 활성화하려면**  
  
-   [ENABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)  
  
-   [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **DDL 트리거를 삭제하려면**  
  
-   [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)  
  
  
