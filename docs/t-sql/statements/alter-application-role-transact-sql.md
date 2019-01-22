---
title: ALTER APPLICATION ROLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_APPLICATION_ROLE_TSQL
- ALTER APPLICATION ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying application roles
- passwords [SQL Server], application roles
- ALTER APPLICATION ROLE statement
- application roles [SQL Server], modifying
ms.assetid: c6cd5d0f-18f4-49be-b161-64d9c5569086
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b272b3b5df01931cfabf1f19945bba477cc680bc
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54326714"
---
# <a name="alter-application-role-transact-sql"></a>ALTER APPLICATION ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  응용 프로그램 역할의 이름, 암호 또는 기본 스키마를 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER APPLICATION ROLE application_role_name   
    WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
    NAME = new_application_role_name   
    | PASSWORD = 'password'  
    | DEFAULT_SCHEMA = schema_name  
```  
  
## <a name="arguments"></a>인수  
 *application_role_name*  
 수정할 응용 프로그램 역할의 이름입니다.  
  
 NAME =*new_application_role_name*  
 응용 프로그램 역할의 새 이름을 지정합니다. 이 이름은 데이터베이스의 다른 보안 주체를 참조하는 데 사용된 이름이 아니어야 합니다.  
  
 PASSWORD ='*password*'  
 응용 프로그램 역할의 암호를 지정합니다. *password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다. 항상 강력한 암호를 사용해야 합니다.  
  
 DEFAULT_SCHEMA =*schema_name*  
 서버에서 개체 이름을 확인할 때 첫 번째로 검색할 스키마를 지정합니다. *schema_name*은 데이터베이스에 존재하지 않는 스키마일 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 새 응용 프로그램 역할 이름이 데이터베이스에 이미 있는 경우 문이 실패합니다. 응용 프로그램 역할의 이름, 암호 또는 기본 스키마가 변경된 경우에도 역할과 연결된 ID는 변경되지 않습니다.  
  
> [!IMPORTANT]  
>  암호 만료 정책은 응용 프로그램 역할 암호에 적용되지 않습니다. 따라서 강력한 암호를 선택할 때는 특히 주의해야 합니다. 애플리케이션 역할을 호출하는 애플리케이션은 해당 암호를 저장해야 합니다.  
  
 응용 프로그램 역할은 sys.database_principals 카탈로그 뷰에 표시됩니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 스키마 동작이 이전 버전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 동작에서 변경되었습니다. 스키마가 데이터베이스 사용자와 같다고 가정하는 코드에서 올바른 결과가 반환되지 않을 수도 있습니다. sysobjects를 비롯한 이전 카탈로그 뷰는 CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION 등의 DDL 문이 사용된 데이터베이스에서 사용하지 않아야 합니다. 이러한 문이 사용된 데이터베이스에서는 새 카탈로그 뷰를 사용해야 합니다. 새 카탈로그 뷰는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 보안 주체와 스키마 분리를 고려합니다. 카탈로그 뷰에 대한 자세한 내용은 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 ALTER ANY APPLICATION ROLE 권한이 필요합니다. 기본 스키마를 변경하려면 응용 프로그램 역할에 대한 ALTER 권한도 필요합니다. 응용 프로그램 역할은 자체 기본 스키마를 변경할 수 있지만 응용 프로그램 역할의 이름이나 암호는 변경할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-name-of-application-role"></a>1. 응용 프로그램 역할의 이름 변경  
 다음 예에서는 응용 프로그램 역할의 이름을 `weekly_receipts`에서 `receipts_ledger`로 변경합니다.  
  
```  
USE AdventureWorks2012;  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987Gbv8$76sPYY5m23' ,   
    DEFAULT_SCHEMA = Sales;  
GO  
ALTER APPLICATION ROLE weekly_receipts   
    WITH NAME = receipts_ledger;  
GO  
```  
  
### <a name="b-changing-the-password-of-application-role"></a>2. 응용 프로그램 역할의 암호 변경  
 다음 예에서는 `receipts_ledger` 응용 프로그램 역할의 암호를 변경합니다.  
  
```  
ALTER APPLICATION ROLE receipts_ledger   
    WITH PASSWORD = '897yUUbv867y$200nk2i';  
GO  
```  
  
### <a name="c-changing-the-name-password-and-default-schema"></a>3. 이름, 암호 및 기본 스키마 변경  
 다음 예에서는 `receipts_ledger` 응용 프로그램 역할의 이름, 암호 및 기본 스키마를 동시에 변경합니다.  
  
```  
ALTER APPLICATION ROLE receipts_ledger   
    WITH NAME = weekly_ledger,   
    PASSWORD = '897yUUbv77bsrEE00nk2i',   
    DEFAULT_SCHEMA = Production;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [애플리케이션 역할](../../relational-databases/security/authentication-access/application-roles.md)   
 [CREATE APPLICATION ROLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
