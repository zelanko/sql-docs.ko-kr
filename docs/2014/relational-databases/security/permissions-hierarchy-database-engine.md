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
manager: craigg
ms.openlocfilehash: 607ac55fe426cd086ce31ade33d3e772e7a3d9a9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487155"
---
# <a name="permissions-hierarchy-database-engine"></a>사용 권한 계층(데이터베이스 엔진)
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 는 사용 권한으로 보호될 수 있는 엔터티의 계층적 컬렉션을 관리합니다. 이러한 엔터티를 *보안 개체*라고 합니다. 가장 두드러진 보안 개체는 서버와 데이터베이스이지만 별개의 사용 권한을 보다 세부적인 수준으로 설정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 적합한 권한이 부여되었는지 확인하여 보안 개체에 대한 보안 주체의 동작을 규제합니다.

 다음 그림에서는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 사용 권한 계층 간의 관계를 보여 줍니다.

 ![데이터베이스 엔진 권한 계층 구조 다이어그램](../../database-engine/media/wj-security-layers.gif "데이터베이스 엔진 권한 계층 구조 다이어그램")

## <a name="chart-of-sql-server-permissions"></a>SQL Server 사용 권한 차트
 PDF 형식으로 모든 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 권한의 포스터 크기 차트는 을 참조하십시오. [https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf)

## <a name="working-with-permissions"></a>사용 권한 작업
 익숙한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리인 GRANT, DENY 및 REVOKE를 사용하여 사용 권한을 조작할 수 있습니다. 사용 권한에 대한 정보는 [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) 및 [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) 카탈로그 뷰에 표시됩니다. 또한 기본 제공 함수를 사용한 사용 권한 정보 쿼리도 지원됩니다.

## <a name="see-also"></a>참고 항목
 [SQL Server](securing-sql-server.md) 권한 &#40;[데이터베이스 엔진&#41;](permissions-database-engine.md) [보안](securables.md) 성 보안 보안 엔진 보안 보안 보안 엔진 보안 보안 보안&#41;보안 보안 보안 엔진 &#40;데이터베이스 [엔진](authentication-access/principals-database-engine.md) &#40;그랜트 &#40;[거래-SQL&#41;](/sql/t-sql/statements/grant-transact-sql) [해지 &#40;거래-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql) &#40;HAS_PERMS_BY_NAME HAS_PERMS_BY_NAME [거래-SQL&#41;&#41;](/sql/t-sql/statements/deny-transact-sql) &#40;HAS_PERMS_BY_NAME HAS_PERMS_BY_NAME 거래-SQL&#41;[sys.fn_builtin_permissions 거래-SQL&#41;sys.&#40;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql) &#40;server_permissions [sys.server_permissions sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) 거래-SQL&#41;sys.database_permissions [거래-SQL](/sql/t-sql/functions/has-perms-by-name-transact-sql)&#41;[sys.&#40;](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) database_permissions&#41;


