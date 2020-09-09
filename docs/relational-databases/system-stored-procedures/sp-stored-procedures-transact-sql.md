---
description: sp_stored_procedures(Transact-SQL)
title: sp_stored_procedures (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_stored_procedures_TSQL
- sp_stored_procedures
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stored_procedures
ms.assetid: fe52dd83-000a-4665-83fb-7a0024193dec
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 41c28dd8a9dff8c95f6656aace6d80eb8d289e7c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541158"
---
# <a name="sp_stored_procedures-transact-sql"></a>sp_stored_procedures(Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 환경에서 저장 프로시저의 목록을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_stored_procedures [ [ @sp_name = ] 'name' ]   
    [ , [ @sp_owner = ] 'schema']   
    [ , [ @sp_qualifier = ] 'qualifier' ]  
    [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @sp_name = ] 'name'` 카탈로그 정보를 반환 하는 데 사용 되는 프로시저의 이름입니다. *name* 은 **nvarchar (390)** 이며 기본값은 NULL입니다. 와일드카드 패턴 일치가 지원됩니다.  
  
`[ @sp_owner = ] 'schema'` 프로시저가 속한 스키마의 이름입니다. *schema* 는 **nvarchar (384)** 이며 기본값은 NULL입니다. 와일드카드 패턴 일치가 지원됩니다. *Owner* 를 지정 하지 않은 경우 기본 DBMS의 기본 프로시저 표시 유형 규칙이 적용 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 현재 스키마에 지정된 이름을 가진 프로시저가 포함된 경우 해당 프로시저가 반환됩니다. 불완전한 저장 프로시저가 지정된 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 다음 순서로 프로시저를 검색합니다.  
  
-   현재 데이터베이스의 **sys** 스키마  
  
-   일괄 처리나 동적 SQL에서 실행된 경우 호출자의 기본 스키마 또는 불완전한 프로시저 이름이 다른 프로시저 정의의 본문 안에 나타나는 경우 이러한 다른 프로시저를 포함하는 스키마가 다음에 검색됩니다.  
  
-   현재 데이터베이스의 **dbo** 스키마  
  
`[ @qualifier = ] 'qualifier'` 프로시저 한정자의 이름입니다. *한정자* 는 **sysname**이며 기본값은 NULL입니다. 다양 한 DBMS 제품에서 형식의 테이블에 대해 세 부분으로 구성 된 이름 (_한정자_)을 지원**합니다.** _스키마_**.** _이름_. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *한정자* 는 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
`[ @fUsePattern = ] 'fUsePattern'` 밑줄 (_), 백분율 (%) 또는 대괄호 ([])가 와일드 카드 문자로 해석 되는지 여부를 결정 합니다. *fUsePattern* 는 **bit**이며 기본값은 1입니다.  
  
 **0** = 패턴 일치가 해제 되어 있습니다.  
  
 **1** = 패턴 일치가 on입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|프로시저 한정자 이름입니다. 이 열은 NULL이 될 수 있습니다.|  
|**PROCEDURE_OWNER**|**sysname**|프로시저 소유자 이름입니다. 이 열은 항상 값을 반환합니다.|  
|**PROCEDURE_NAME**|**nvarchar (134)**|프로시저 이름입니다. 이 열은 항상 값을 반환합니다.|  
|**NUM_INPUT_PARAMS**|**int**|나중에 사용하기 위해 예약되어 있습니다.|  
|**NUM_OUTPUT_PARAMS**|**int**|나중에 사용하기 위해 예약되어 있습니다.|  
|**NUM_RESULT_SETS**|**int**|나중에 사용하기 위해 예약되어 있습니다.|  
|**설명**|**varchar (254)**|프로시저에 대한 설명입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 열의 값을 반환하지 않습니다.|  
|**PROCEDURE_TYPE**|**smallint**|프로시저 유형입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 항상 2.0을 반환합니다. 이 값은 다음 중 하나일 수 있습니다.<br /><br /> 0 = SQL_PT_UNKNOWN<br /><br /> 1 = SQL_PT_PROCEDURE<br /><br /> 2 = SQL_PT_FUNCTION|  
  
## <a name="remarks"></a>설명  
 상호 운용성을 최대로 높이려면 게이트웨이 클라이언트가 퍼센트(%) 및 밑줄(_) 와일드카드 문자 등의 SQL 표준 패턴 일치만을 가정해야 합니다.  
  
 특정 저장 프로시저에 대한 현재 사용자의 실행 액세스에 관한 사용 권한 정보가 반드시 확인되는 것은 아니므로 액세스가 보장되지 않습니다. 세 부분으로 구성된 이름만 사용됩니다. 즉, 원격 저장 프로시저(네 부분으로 구성된 이름)와 로컬 저장 프로시저가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 실행되면 로컬 저장 프로시저만 반환되고 원격 저장 프로시저는 반환되지 않습니다. 서버 특성 ACCESSIBLE_SPROC **sp_server_info**결과 집합에서 Y 인 경우 현재 사용자가 실행할 수 있는 저장 프로시저만 반환 됩니다.  
  
 **sp_stored_procedures** 는 ODBC의 **sqlprocedures** 와 동일 합니다. 반환 되는 결과는 **PROCEDURE_QUALIFIER**, **PROCEDURE_OWNER**및 **PROCEDURE_NAME**순으로 정렬 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-all-stored-procedures-in-the-current-database"></a>A. 현재 데이터베이스의 모든 저장 프로시저 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 모든 저장 프로시저를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_stored_procedures;  
```  
  
### <a name="b-returning-a-single-stored-procedure"></a>B. 단일 저장 프로시저 반환  
 다음 예에서는 `uspLogError` 저장 프로시저의 결과 집합을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
sp_stored_procedures N'uspLogError', N'dbo', N'AdventureWorks2012', 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;카탈로그 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
