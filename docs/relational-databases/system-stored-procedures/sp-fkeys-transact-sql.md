---
title: sp_fkeys (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fkeys
- sp_fkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fkeys
ms.assetid: 18110444-d38d-4cff-90d2-d1fc6236668b
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fc012a7b05f2387756e25bfb86c93896d3f94190
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536663"
---
# <a name="spfkeys-transact-sql"></a>sp_fkeys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 환경에 대한 논리적 외래 키 정보를 반환합니다. 이 프로시저는 사용할 수 없는 외래 키를 포함한 외래 키 관계를 보여 줍니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_fkeys [ @pktable_name = ] 'pktable_name'   
     [ , [ @pktable_owner = ] 'pktable_owner' ]   
     [ , [ @pktable_qualifier = ] 'pktable_qualifier' ]   
     { , [ @fktable_name = ] 'fktable_name' }   
     [ , [ @fktable_owner = ] 'fktable_owner' ]   
     [ , [ @fktable_qualifier = ] 'fktable_qualifier' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @pktable_name=] '*pktable_name*'  
 카탈로그 정보를 반환하는 데 사용하는 기본 키가 있는 테이블 이름입니다. *pktable_name* 됩니다 **sysname**, 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. 이 매개 변수 또는 *fktable_name* 매개 변수 또는 둘 다 제공 해야 합니다.  
  
 [ @pktable_owner=] '*pktable_owner*'  
 카탈로그 정보를 반환 하는 데 사용 된 기본 키가 있는 테이블의 소유자 이름이입니다. *pktable_owner* 됩니다 **sysname**, 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. 하는 경우 *pktable_owner* 지정 하지 않으면 기본 DBMS의 기본 테이블 표시 규칙이 적용 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 사용자가 지정한 이름의 테이블을 소유하고 있는 경우 해당 테이블의 열이 반환됩니다. 하는 경우 *pktable_owner* 지정 하지 않으면 현재 사용자 지정 된 테이블을 소유 하지 않는 한 *pktable_name*, 프로시저는 지정 된 테이블을 *pktable_name* 데이터베이스 소유자가 소유 합니다. 테이블이 있으면 테이블의 열이 반환됩니다.  
  
 [ @pktable_qualifier =] '*pktable_qualifier*'  
 기본 키가 있는 테이블 한정자의 이름입니다. *pktable_qualifier* 는 sysname 이며 기본값은 NULL입니다. 다양 한 DBMS 제품에서는 테이블에 대해 세 부분으로 이루어진 이름 (*qualifier.owner.name*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 한정자는 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
 [ @fktable_name=] '*fktable_name*'  
 카탈로그 정보를 반환하는 데 사용되는 외래 키가 있는 테이블 이름입니다. *fktable_name* 는 sysname 이며 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. 이 매개 변수 또는 *pktable_name* 매개 변수 또는 둘 다 제공 해야 합니다.  
  
 [ @fktable_owner =] '*fktable_owner*'  
 카탈로그 정보를 반환하는 데 사용되는 외래 키가 있는 테이블 이름입니다. *fktable_owner* 됩니다 **sysname**, 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. 하는 경우 *fktable_owner* 지정 하지 않으면 기본 DBMS의 기본 테이블 표시 규칙이 적용 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 사용자가 지정한 이름의 테이블을 소유하고 있는 경우 해당 테이블의 열이 반환됩니다. 하는 경우 *fktable_owner* 지정 하지 않으면 현재 사용자 지정 된 테이블을 소유 하지 않는 한 *fktable_name*, 프로시저는 지정 된 테이블을 *fktable_name* 데이터베이스 소유자가 소유 합니다. 테이블이 있으면 테이블의 열이 반환됩니다.  
  
 [ @fktable_qualifier=] '*fktable_qualifier*'  
 외래 키가 있는 테이블 한정자의 이름입니다. *fktable_qualifier* 됩니다 **sysname**, 기본값은 NULL입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 한정자는 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|PKTABLE_QUALIFIER|**sysname**|기본 키가 있는 테이블의 한정자 이름입니다. 이 필드는 NULL이 될 수 있습니다.|  
|PKTABLE_OWNER|**sysname**|기본 키가 있는 테이블의 소유자 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|PKTABLE_NAME|**sysname**|기본 키가 있는 테이블의 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|PKCOLUMN_NAME|**sysname**|반환되는 TABLE_NAME의 각 열에 대한 기본 키 열의 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|FKTABLE_QUALIFIER|**sysname**|외래 키가 있는 테이블의 한정자 이름입니다. 이 필드는 NULL이 될 수 있습니다.|  
|FKTABLE_OWNER|**sysname**|외래 키가 있는 테이블의 소유자 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|FKTABLE_NAME|**sysname**|외래 키가 있는 테이블의 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|FKCOLUMN_NAME|**sysname**|반환되는 TABLE_NAME의 각 열에 대한 외래 키 열의 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|KEY_SEQ|**smallint**|기본 키가 여러 열로 구성된 경우 열의 시퀀스 번호입니다. 이 필드는 항상 값을 반환합니다.|  
|UPDATE_RULE|**smallint**|SQL 작업이 업데이트일 때 외래 키에 적용되는 동작입니다.  가능한 값은 다음과 같습니다.<br /> 0=CASCADE는 외래 키를 변경합니다.<br /> 1=NO ACTION은 외래 키가 있으면 변경합니다.<br />   2 = null 설정 <br /> 3 = 기본값 설정 |  
|DELETE_RULE|**smallint**|SQL 작업이 삭제일 때 외래 키에 적용되는 동작입니다. 가능한 값은 다음과 같습니다.<br /> 0=CASCADE는 외래 키를 변경합니다.<br /> 1=NO ACTION은 외래 키가 있으면 변경합니다.<br />   2 = null 설정 <br /> 3 = 기본값 설정 |  
|FK_NAME|**sysname**|외래 키 식별자입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건 이름을 반환합니다.|  
|PK_NAME|**sysname**|기본 키 식별자입니다. 데이터 원본에 적용할 수 없는 경우 NULL입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 PRIMARY KEY 제약 조건 이름을 반환합니다.|  
  
 반환 된 결과 FKTABLE_QUALIFIER, FKTABLE_OWNER, FKTABLE_NAME 및 KEY_SEQ로 정렬 됩니다.  
  
## <a name="remarks"></a>Remarks  
 외래 키를 사용할 수 없는 테이블을 포함하는 응용 프로그램 코딩은 다음과 같은 방법으로 구현됩니다.  
  
-   테이블에 관한 작업을 하는 동안 제약 조건 확인(ALTER TABLE NOCHECK 또는 CREATE TABLE NOT FOR REPLICATION)을 일시적으로 사용하지 못하게 한 다음 나중에 다시 사용할 수 있도록 합니다.  
  
-   트리거 또는 응용 프로그램 코드를 사용하여 강제로 연결합니다.  
  
기본 키 테이블 이름은 제공되고 외래 키 테이블 이름이 NULL인 경우 sp_fkeys는 외래 키를 포함한 모든 테이블을 지정된 테이블로 반환합니다. 외래 키 테이블 이름은 제공되고 기본 키 테이블 이름이 NULL인 경우 sp_fkeys는 외래 키 테이블의 외래 키에 기본 키/외래 키 관계로 연관된 모든 테이블을 반환합니다.  
  
Sp_fkeys 저장 프로시저는 ODBC의 SQLForeignKeys와 동일합니다.  
  
## <a name="permissions"></a>사용 권한  
 필요한 `SELECT` 스키마에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `HumanResources.Department` 데이터베이스의 `AdventureWorks2012` 테이블에 대한 외래 키 목록을 검색합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `DimDate` 데이터베이스의 `AdventureWorksPDW2012` 테이블에 대한 외래 키 목록을 검색합니다. 때문에 아무 행도 반환 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 외래 키를 지원 하지 않습니다.  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate;  
```  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_pkeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

