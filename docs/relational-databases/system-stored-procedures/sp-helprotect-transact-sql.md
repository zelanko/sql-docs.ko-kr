---
title: sp_helprotect (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helprotect
- sp_helprotect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprotect
ms.assetid: faaa3e40-1c95-43c2-9fdc-c61a1d3cc0c3
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0c92f72b54b5b3d420e2e4cbdbfe616f9e6f090f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelprotect-transact-sql"></a>sp_helprotect(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 개체에 대한 사용자 권한 또는 문 사용 권한에 관한 정보가 포함된 보고서를 반환합니다.  
  
> [!IMPORTANT]  
>  **sp_helprotect** 에 도입 된 보안 개체에 대 한 정보를 반환 하지 않는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다. 사용 하 여 [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 및 [fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md) 대신 합니다.  
  
 고정 서버 역할 또는 고정 데이터베이스 역할에 항상 할당된 사용 권한을 나열하지 않습니다. 역할에서의 멤버 자격에 따라 사용 권한을 받는 로그인 또는 사용자를 포함하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helprotect [ [ @name = ] 'object_statement' ]   
     [ , [ @username = ] 'security_account' ]   
     [ , [ @grantorname = ] 'grantor' ]   
     [ , [ @permissionarea = ] 'type' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@name =** ] **'***object_statement***'**  
 보고서에 대한 사용 권한을 가진 현재 데이터베이스에 있는 개체 또는 문의 이름입니다. *object_statement* 은 **nvarchar(776)**, 기본값은 NULL 반환 하는 모든 개체 및 문 사용 권한. 값이 개체(테이블,  뷰,  저장 프로시저 또는 확장 저장 프로시저)인 경우에는 반드시 현재 데이터베이스의 유효한 개체여야 합니다. 개체 이름은 형식에서 소유자의 한정자를 포함할 수 있습니다 *소유자 ***.*** 개체*합니다.  
  
 경우 *object_statement* 는 문 CREATE 문일 수 있습니다.  
  
 [  **@username =** ] **'***security_account***'**  
 사용 권한이 반환되는 보안 주체의 이름입니다. *security_account* 은 **sysname**, 기본값은 NULL 반환 하는 모든 보안 주체는 현재 데이터베이스에 있습니다. *security_account* 현재 데이터베이스에 존재 해야 합니다.  
  
 [  **@grantorname =** ] **'***grantor***'**  
 사용 권한을 부여한 보안 주체의 이름입니다. *grantor* 은 **sysname**, 기본값은 NULL 반환 하는 보안 주체는 데이터베이스에 의해 부여 된 권한에 대 한 모든 정보입니다.  
  
 [ **@permissionarea =** ] **'***type***'**  
 개체 사용 권한을 표시 여부를 나타내는 문자열 (문자열 **o**), 문 사용 권한 (문자열 **s**), 또는 둘 다 (**os**). *형식* 은 **varchar (10)**, 기본값은 **os**합니다. *형식* 의 조합이 포함 될 수 **o** 및 **s**, 하거나 사용 하지 않고 쉼표 또는 사이 공백을 **o** 및 **s**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**소유자**|**sysname**|개체 소유자의 이름입니다.|  
|**개체**|**sysname**|개체 이름입니다.|  
|**피부 여자에 게**|**sysname**|사용 권한이 부여된 보안 주체의 이름입니다.|  
|**Grantor**|**sysname**|지정된 사람에게 사용 권한을 부여한 보안 주체의 이름입니다.|  
|**ProtectType**|**nvarchar(10)**|보호의 유형 이름입니다.<br /><br /> GRANT  REVOKE|  
|**작업**|**nvarchar(60)**|사용 권한의 이름입니다. 유효한 사용 권한 문은 개체의 유형에 따라 달라집니다.|  
|**열**|**sysname**|사용 권한의 유형입니다.<br /><br /> All  =  사용 권한이 개체의 모든 현재 열을 포함합니다.<br /><br /> New  =  사용 권한이 미래의 개체에서 (ALTER문을 사용하여)  변경할 수 있는 모든 새 열을 포함합니다.<br /><br /> All+New  =  All과 New의 조합입니다.<br /><br /> 사용 권한의 유형이 열에 적용되지 않는 경우에는 마침표를 반환합니다.|  
  
## <a name="remarks"></a>주의  
 다음 절차의 모든 매개 변수는 선택 사항입니다. 매개 변수 없이 `sp_helprotect`를 실행한 경우에는 현재 데이터베이스에 부여되었거나 거부된 모든 사용 권한을 표시합니다.  
  
 전부가 아니라 일부 매개 변수가 지정된 경우에는 명명된 매개 변수를 사용하여 특정 매개 변수를 식별하거나 `NULL`을 자리 표시자로 사용합니다. 예를 들어 사용 권한을 부여한 데이터베이스 소유자(`dbo`)에 관한 사용 권한을 모두 보고하려면 다음을 실행합니다.  
  
```  
EXEC sp_helprotect NULL, NULL, dbo;  
```  
  
 또는  
  
```  
EXEC sp_helprotect @grantorname = 'dbo';  
```  
  
 출력 보고서는 사용 권한 범주,  소유자,  개체,  피부여자,  사용 권한을 부여한 사용자,  보호 유형 범주,  보호 유형,  동작 및 열 시퀀스 ID  별로 정렬됩니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
 반환되는 정보는 메타데이터에 대한 액세스 제한 사항에 따라 달라집니다. 보안 주체에 사용 권한이 없는 엔터티는 나타나지 않습니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-the-permissions-for-a-table"></a>1. 테이블에 대한 사용 권한 나열  
 다음 예에서는 `titles` 테이블에 대한 사용 권한을 나열합니다.  
  
```  
EXEC sp_helprotect 'titles';  
```  
  
### <a name="b-listing-the-permissions-for-a-user"></a>2. 사용자에 대한 사용 권한 나열  
 다음 예에서는 `Judy`라는 사용자가 현재 데이터베이스에서 갖고 있는 모든 사용 권한을 나열합니다.  
  
```  
EXEC sp_helprotect NULL, 'Judy';  
```  
  
### <a name="c-listing-the-permissions-granted-by-a-specific-user"></a>3. 특정 사용자에 의해 부여된 사용 권한 나열  
 다음 예에서는 현재 데이터베이스에서 `Judy`라는 사용자에 의해 부여된 모든 사용 권한을 나열하고 누락된 매개 변수에 대해 `NULL`을 자리 표시자로 사용합니다.  
  
```  
EXEC sp_helprotect NULL, NULL, 'Judy';  
```  
  
### <a name="d-listing-the-statement-permissions-only"></a>4. 문 사용 권한만 나열  
 다음 예에서는 현재 데이터베이스의 모든 문 사용 권한을 나열하고 누락된 매개 변수에 대해 `NULL`을 자리 표시자로 사용합니다.  
  
```  
EXEC sp_helprotect NULL, NULL, NULL, 's';   
```  
  
### <a name="e-listing-the-permissions-for-a-create-statement"></a>e. CREATE 문에 대한 사용 권한 나열  
 다음 예에서는 CREATE  TABLE  사용 권한이 부여된 모든 사용자를 나열합니다.  
  
```  
EXEC sp_helprotect @name = 'CREATE TABLE';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
