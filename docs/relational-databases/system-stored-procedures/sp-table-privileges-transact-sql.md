---
title: sp_table_privileges (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_table_privileges
- sp_table_privileges_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_table_privileges
ms.assetid: 0512e688-4fc0-4557-8dc8-016672c1e3fe
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 96e042da46762540d510e6d41f275696439f8099
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sptableprivileges-transact-sql"></a>sp_table_privileges(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 테이블에 대한 INSERT, DELETE, UPDATE, SELECT, REFERENCES와 같은 테이블 사용 권한의 목록을 반환합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_table_privileges [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @table_name=] '*table_name*'  
 카탈로그 정보를 반환하는 데 사용되는 테이블입니다. *table_name* 은 **nvarchar (**384**)**, 기본값은 없습니다. 와일드카드 패턴 일치가 지원됩니다.  
  
 [ @table_owner=] '*table_owner*'  
 카탈로그 정보를 반환하는 데 사용하는 테이블의 소유자입니다. *table_owner*은 **nvarchar (**384**)**, 기본값은 NULL입니다. 와일드카드 패턴 일치가 지원됩니다. 소유자를 지정하지 않은 경우 기본 DBMS의 기본 테이블 표시 유형 규칙이 적용됩니다.  
  
 현재 사용자가 지정된 이름의 테이블을 소유한 경우 해당 테이블의 열이 반환됩니다. 경우 *소유자* 지정 하지 않으면 현재 사용자가 지정 된 테이블을 소유 하지 *이름*,이 프로시저는 지정 된 테이블에 대 한 찾습니다 *table_name* 소유한는 데이터베이스 소유자입니다. 테이블이 있을 경우 해당 테이블의 열이 반환됩니다.  
  
 [ @table_qualifier=] '*table_qualifier*'  
 테이블 한정자의 이름입니다. *table_qualifier* 은 **sysname**, 기본값은 NULL입니다. 다양 한 DBMS 제품에서는 테이블에 대 한 세 부분으로 구성 된 이름 (*qualifier.owner.name*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
 [ @fUsePattern=] '*fUsePattern*'  
 된 밑줄 (_), 백분율 (%), 대괄호 ([및]) 문자 와일드 카드 문자로 해석할지 여부를 결정 합니다. 유효한 값은 0(패턴 일치 해제)과 1(패턴 일치 설정)입니다. *fUsePattern* 은 **비트**, 기본값은 1입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|테이블 한정자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 이 필드는 NULL이 될 수 있습니다.|  
|TABLE_OWNER|**sysname**|테이블 소유자 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|TABLE_NAME|**sysname**|테이블 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|GRANTOR|**sysname**|나열된 GRANTEE에 대해 이 TABLE_NAME에 대한 권한을 부여한 데이터베이스 사용자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 항상 TABLE_OWNER와 같습니다. 이 필드는 항상 값을 반환합니다. 또한 GRANTOR 열은 데이터베이스 소유자(TABLE_OWNER) 또는 데이터베이스 소유자가 GRANT 문의 WITH GRANT OPTION 절을 사용하여 사용 권한을 부여한 사용자가 될 수 있습니다.|  
|GRANTEE|**sysname**|나열된 GRANTOR에 의해 이 TABLE_NAME에 대한 사용 권한을 부여 받은 데이터베이스 사용자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],이 열은 항상 sys.database_principalssystem 보기에서 데이터베이스 사용자를 포함 합니다. 이 필드는 항상 값을 반환합니다.|  
|PRIVILEGE|**sysname**|사용할 수 있는 테이블 사용 권한 중의 하나입니다. 테이블 사용 권한은 다음 값(또는 구현이 정의될 때 데이터 원본에 의해 지원되는 다른 값) 중 하나일 수 있습니다.<br /><br /> SELECT = GRANTEE는 하나 이상의 열에 대한 데이터를 검색할 수 있습니다.<br /><br /> INSERT = GRANTEE는 하나 이상의 열에 대한 새 행에 데이터를 제공할 수 있습니다.<br /><br /> UPDATE = GRANTEE는 하나 이상의 열에 대한 기존 데이터를 수정할 수 있습니다.<br /><br /> DELETE = GRANTEE는 테이블에서 행을 제거할 수 있습니다.<br /><br /> REFERENCES = GRANTEE는 기본 키/외래 키 관계에 있는 외래 테이블의 열을 참조할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본 키/외래 키 관계는 테이블 제약 조건에 의해 정의됩니다.<br /><br /> 지정된 테이블 권한으로 GRANTEE에 지정된 동작의 범위는 데이터 원본에 따라 결정됩니다. 예를 들어 UPDATE 권한은 GRANTEE가 한 데이터 원본 내 테이블의 모든 열 그리고 다른 데이터 원본에서 GRANTOR가 UPDATE 권한을 가진 열만을 업데이트하도록 허용할 수 있습니다.|  
|IS_GRANTABLE|**sysname**|다른 사용자에게 권한을 부여하는 GRANTEE를 허용할 것인지 여부를 나타냅니다. "권한 부여 권한(grant with grant)"이라고도 부릅니다. YES, NO 또는 NULL이 될 수 있습니다. 알 수 없는 값(또는 NULL)은 "권한 부여 권한"을 적용할 수 없는 데이터 원본을 의미합니다.|  
  
## <a name="remarks"></a>주의  
 sp_table_privileges 저장 프로시저는 ODBC에서 SQLTablePrivileges와 같습니다. 반환된 결과는 TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME 및 PRIVILEGE 순으로 정렬됩니다.  
  
## <a name="permissions"></a>Permissions  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이름이 `Contact`로 시작하는 모든 테이블에 대한 권한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_table_privileges   
   @table_name = 'Contact%';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
