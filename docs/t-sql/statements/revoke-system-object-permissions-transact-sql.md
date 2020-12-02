---
description: REVOKE 시스템 개체 사용 권한(Transact-SQL)
title: REVOKE System Object Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, system objects
- permissions [SQL Server], system objects
ms.assetid: 84983238-dd7d-45bd-99bb-52c9d8e96a87
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c7485325af023c264193fcc8ce8a449553dcb0b9
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91498045"
---
# <a name="revoke-system-object-permissions-transact-sql"></a>REVOKE 시스템 개체 사용 권한(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  보안 주체의 저장 프로시저, 확장 저장 프로시저, 함수 및 뷰와 같은 시스템 개체에 대한 권한을 취소합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
REVOKE { SELECT | EXECUTE } ON [sys.]system_object FROM principal   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 [**sys.** ] .  
 **sys** 한정자는 카탈로그 뷰 및 동적 관리 뷰를 참조하는 경우에만 필요합니다.  
  
 *system_object*  
 사용 권한을 취소할 개체를 지정합니다.  
  
 *principal*  
 사용 권한을 취소할 보안 주체를 지정합니다.  
  
## <a name="remarks"></a>설명  
 이 문을 사용하면 특정 저장 프로시저, 확장 저장 프로시저, 테이블 반환 함수, 스칼라 함수, 뷰, 카탈로그 뷰, 호환성 뷰, INFORMATION_SCHEMA 뷰, 동적 관리 뷰 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 설치된 시스템 테이블에 대한 사용 권한을 취소할 수 있습니다. 이러한 각 시스템 개체는 리소스 데이터베이스(**mssqlsystemresource**)에 고유한 레코드로 존재합니다. 리소스 데이터베이스는 읽기 전용입니다. 개체에 대한 링크는 모든 데이터베이스의 **sys** 스키마에 레코드로 표시됩니다.  
  
 기본 이름 확인은 정규화되지 않은 프로시저 이름을 리소스 데이터베이스로 확인합니다. 따라서 **sys.** 한정자는 카탈로그 뷰 및 동적 관리 뷰를 지정하는 경우에만 필요합니다.  
  
> [!CAUTION]  
>  시스템 개체에 대한 사용 권한을 취소하면 이러한 개체에 종속된 애플리케이션이 실패합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]는 카탈로그 뷰를 사용하며 카탈로그 뷰에 대한 기본 사용 권한을 변경하면 정상적으로 작동하지 않을 수 있습니다.  
  
 트리거 및 시스템 개체의 열에 대한 사용 권한은 취소할 수 없습니다.  
  
 시스템 개체에 대한 사용 권한은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 시 유지됩니다.  
  
 시스템 개체는 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `EXECUTE`으로부터 `sp_addlinkedserver`에 대한 `public` 권한을 취소합니다.  
  
```sql  
REVOKE EXECUTE ON sys.sp_addlinkedserver FROM public;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [GRANT 시스템 개체 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [DENY 시스템 개체 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
