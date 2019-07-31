---
ms.openlocfilehash: 327fd6bac9bc1036a0dd07f7b955ee92cb7e40c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223545"
---
  SQL Server 2005부터 스키마 동작이 변경되었습니다. 이에 따라 스키마가 데이터베이스 사용자와 같다고 가정하는 코드에서 올바른 결과가 반환되지 않을 수 있습니다. 다음 DDL 문이 사용된 적이 있는 데이터베이스에서는 sysobjects를 비롯한 이전 카탈로그 뷰를 사용하면 안 됩니다. CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION 등의 DDL 문이 사용된 데이터베이스에서 사용하지 않아야 합니다. 이러한 데이터베이스에서는 새 카탈로그 뷰를 대신 사용해야 합니다. 새 카탈로그 뷰에서는 SQL Server 2005에 도입된 보안 주체와 스키마의 분리를 고려하고 있습니다. 카탈로그 뷰에 대한 자세한 내용은 [카탈로그 뷰&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)를 참조하세요.
   