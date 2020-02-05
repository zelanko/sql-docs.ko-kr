---
title: GRANT System Object Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], system objects
- system objects [SQL Server]
- GRANT statement, system objects
ms.assetid: 9d4e89f4-478f-419a-8b50-b096771e3880
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cd783ac6f5f6d8c7a9e561614dbe2c06053f758a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68050673"
---
# <a name="grant-system-object-permissions-transact-sql"></a>GRANT 시스템 개체 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  시스템 저장 프로시저, 확장 저장 프로시저, 함수 및 뷰와 같은 시스템 개체에 대한 권한을 부여합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GRANT { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>인수  
 [ sys.] .  
 sys 한정자는 카탈로그 뷰 및 동적 관리 뷰를 참조하는 경우에만 필요합니다.  
  
 *system_object*  
 사용 권한을 부여할 개체를 지정합니다.  
  
 *principal*  
 사용 권한을 부여할 보안 주체를 지정합니다.  
  
## <a name="remarks"></a>설명  
 이 문을 사용하면 특정 저장 프로시저, 확장 저장 프로시저, 테이블 반환 함수, 스칼라 함수, 뷰, 카탈로그 뷰, 호환성 뷰, INFORMATION_SCHEMA 뷰, 동적 관리 뷰 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 설치된 시스템 테이블에 대한 사용 권한을 부여할 수 있습니다. 이러한 각 시스템 개체는 서버의 리소스 데이터베이스(mssqlsystemresource)에 고유한 레코드로 존재합니다. 리소스 데이터베이스는 읽기 전용입니다. 개체에 대한 링크는 모든 데이터베이스의 sys 스키마에 레코드로 표시됩니다. 시스템 개체를 실행하거나 선택할 수 있는 사용 권한을 부여, 거부 및 취소할 수 있습니다.  
  
 개체를 실행하거나 선택할 수 있는 사용 권한을 부여할 경우 해당 개체를 사용하는 데 필요한 모든 사용 권한이 포함되는 것은 아닙니다. 대부분의 개체는 추가 사용 권한이 필요한 작업을 수행합니다. 예를 들어 sp_addlinkedserver에 대한 EXECUTE 권한이 부여된 사용자는 sysadmin 고정 서버 역할의 멤버가 아닌 경우 연결된 서버를 만들 수 없습니다.  
  
 기본 이름 확인은 정규화되지 않은 프로시저 이름을 리소스 데이터베이스로 확인합니다. 따라서 sys 한정자는 카탈로그 뷰 및 동적 관리 뷰를 지정하는 경우에만 필요합니다.  
  
 트리거 및 시스템 개체의 열에 대한 사용 권한은 부여할 수 없습니다.  
  
 시스템 개체에 대한 사용 권한은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 시 유지됩니다.  
  
 시스템 개체는 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 카탈로그 뷰에 표시됩니다. 시스템 개체에 대한 사용 권한은 마스터 데이터베이스의 [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 다음 쿼리는 시스템 개체의 사용 권한에 대한 정보를 반환합니다.  
  
```  
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-granting-select-permission-on-a-view"></a>A. 뷰에 대한 SELECT 권한 부여  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 나열된 뷰를 선택할 수 있는 `Sylvester1` 로그인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한을 부여합니다. 그런 다음 이 사용자가 소유하지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대한 메타데이터를 보는 데 필요한 추가 사용 권한을 부여합니다.  
  
```  
USE AdventureWorks2012;  
GRANT SELECT ON sys.sql_logins TO Sylvester1;  
GRANT VIEW SERVER STATE to Sylvester1;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-an-extended-stored-procedure"></a>B. 확장 저장 프로시저에 대한 EXECUTE 권한 부여  
 다음 예에서는 `EXECUTE`에 대한 `xp_readmail` 권한을 `Sylvester1`에 부여합니다.  
  
```  
GRANT EXECUTE ON xp_readmail TO Sylvester1;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [REVOKE 시스템 개체 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)   
 [DENY 시스템 개체 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
