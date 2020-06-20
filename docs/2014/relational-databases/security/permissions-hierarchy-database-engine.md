---
title: 사용 권한 계층(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.server.permissions.f1--May use common.permissions
helpviewer_keywords:
- security [SQL Server], denying access
- hierarchies [SQL Server], permissions
- securables [SQL Server]
- security [SQL Server], permissions
- permissions [SQL Server], hierarchy
- security [SQL Server], granting access
ms.assetid: f6d20a55-ef03-4e14-85f9-009902889866
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9a04e5595e509de63b362b31b240e113e635581d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063164"
---
# <a name="permissions-hierarchy-database-engine"></a>사용 권한 계층(데이터베이스 엔진)
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 는 사용 권한으로 보호될 수 있는 엔터티의 계층적 컬렉션을 관리합니다. 이러한 엔터티를 *보안 개체*라고 합니다. 가장 두드러진 보안 개체는 서버와 데이터베이스이지만 별개의 사용 권한을 보다 세부적인 수준으로 설정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 적합한 권한이 부여되었는지 확인하여 보안 개체에 대한 보안 주체의 동작을 규제합니다.

 다음 그림에서는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 사용 권한 계층 간의 관계를 보여 줍니다.

 ![데이터베이스 엔진 권한 계층 구조 다이어그램](../../database-engine/media/wj-security-layers.gif "데이터베이스 엔진 권한 계층 구조 다이어그램")

## <a name="chart-of-sql-server-permissions"></a>SQL Server 사용 권한 차트
 Pdf 형식의 모든 사용 권한에 대 한 포스터 크기 차트를 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 보려면을 참조 하십시오 [https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf) .

## <a name="working-with-permissions"></a>사용 권한 작업
 익숙한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리인 GRANT, DENY 및 REVOKE를 사용하여 사용 권한을 조작할 수 있습니다. 사용 권한에 대한 정보는 [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) 및 [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) 카탈로그 뷰에 표시됩니다. 또한 기본 제공 함수를 사용한 사용 권한 정보 쿼리도 지원됩니다.

## <a name="see-also"></a>참고 항목
 [SQL Server](securing-sql-server.md) [사용 권한 &#40;데이터베이스 엔진&#41;](permissions-database-engine.md) [보안 개체](securables.md) [보안 주체 &#40;](authentication-access/principals-database-engine.md) 데이터베이스 엔진&#41;[transact-sql &#40;&#41;](/sql/t-sql/statements/grant-transact-sql) transact-sql &#40;[DENY](/sql/t-sql/statements/deny-transact-sql) [&#41;transact-sql](/sql/t-sql/statements/revoke-transact-sql) [&#40;&#41;HAS_PERMS_BY_NAME](/sql/t-sql/functions/has-perms-by-name-transact-sql) transact-sql &#40;&#41;[fn_builtin_permissions transact-sql &#40;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)&#41;server_permissions [transact-sql &#40;&#41;](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) database_permissions &#40;&#41;. [transact-sql](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql)


