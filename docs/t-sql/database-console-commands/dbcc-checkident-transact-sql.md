---
title: DBCC CHECKIDENT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKIDENT
- DBCC CHECKIDENT
- CHECKIDENT_TSQL
- DBCC_CHECKIDENT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- checking identity values
- reseeding identity values
- resetting identity values
- identity values [SQL Server]
- identity values [SQL Server], checking
- modifying identity values
- current identity values
- DBCC CHECKIDENT statement
- identity values [SQL Server], reseeding
- reporting current identity values
ms.assetid: 2c00ee51-2062-4e47-8b19-d90f524c6427
caps.latest.revision: "63"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0a370a89e175a00f33d26992cfc5c6aaecbd7436
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-checkident-transact-sql"></a>DBCC CHECKIDENT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지정한 테이블의 현재 ID 값을 검사하고 필요에 따라 변경합니다. DBCC CHECKIDENT를 사용하여 ID 열의 새 현재 ID 값을 수동으로 설정할 수도 있습니다.  
   
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DBCC CHECKIDENT   
 (   
    table_name  
        [, { NORESEED | { RESEED [, new_reseed_value ] } } ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
 *table_name*  
 현재 ID 값을 검사할 테이블의 이름입니다. 지정한 테이블에는 ID 열이 있어야 합니다. 테이블 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. 예: 'Person.AddressType' 또는 [Person.AddressType] 두 개 또는 세 부분으로 된 이름은 구분 해야 합니다.   
  
 NORESEED  
 현재 ID 값을 변경하지 않도록 지정합니다.  
  
 RESEED  
 현재 ID 값을 변경하도록 지정합니다.  
  
 *new_reseed_value*  
 ID 열의 현재 값으로 사용할 새 값입니다.  
  
 WITH NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>주의  
 현재 ID 값의 구체적인 수정 사항은 매개 변수 지정에 따라 달라집니다.  
  
|DBCC CHECKIDENT 명령|ID 수정 사항|  
|-----------------------------|---------------------------------------------|  
|DBCC CHECKIDENT ( *table_name*, NORESEED)|현재 ID 값을 다시 설정하지 않습니다. DBCC CHECKIDENT는 ID 열의 현재 ID 값과 현재 최대값을 반환합니다. 두 값이 같지 않으면 ID 값을 다시 설정하여 잠재적 오류를 방지하고 값이 간격 없이 순서대로 지정되도록 해야 합니다.|  
|DBCC CHECKIDENT ( *table_name* )<br /><br /> 또는<br /><br /> DBCC CHECKIDENT ( *table_name*, RESEED)|테이블의 현재 ID 값이 ID 열에 저장된 최대 ID 값보다 작을 경우 ID 열의 최대값을 사용하여 다시 설정됩니다. 뒷부분에 나오는 '예외' 섹션을 참조하십시오.|  
|DBCC CHECKIDENT ( *table_name*, RESEED, *new_reseed_value* )|현재 id 값으로 설정 되 고 *new_reseed_value*합니다. 테이블을 만든 또는 DBCC CHECKIDENT를 실행 한 후 삽입 된 첫 번째 행에 사용 하 여 TRUNCATE TABLE 문을 사용 하 여 모든 행을 분리 하므로 테이블에 삽입 된 행이 없는 경우 *new_reseed_value* id로 합니다.<br /><br /> 와 다음 행이 삽입 행 테이블에 있는 경우에 *new_reseed_value* 값입니다. 버전에서 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 앞에서 삽입 한 다음 행을 사용 하 여 *new_reseed_value* + [현재 증분](../../t-sql/functions/ident-incr-transact-sql.md) 값입니다.<br /><br /> 테이블이 비어 있지 않은 경우 ID 값을 ID 열의 최대값보다 작은 숫자로 설정하면 다음 조건 중 하나가 발생할 수 있습니다.<br /><br /> -Id 열에 PRIMARY KEY 또는 UNIQUE 제약 조건이 있는 경우 오류 메시지 2627 생성 되는 id 값은 기존 값과 충돌 하기 때문에 테이블에 삽입 작업을 나중에 생성 됩니다.<br /><br /> -PRIMARY KEY 또는 UNIQUE 제약 조건이 없는 경우, 나중에 삽입 작업 id 값이 중복 됩니다.|  
  
## <a name="exceptions"></a>예외  
 다음 표에서는 DBCC CHECKIDENT가 자동으로 현재 ID 값을 다시 설정하지 않는 조건을 보여 주고 해당 값을 다시 설정하는 방법을 제공합니다.  
  
|조건|다시 설정 방법|  
|---------------|-------------------|  
|현재 ID 값이 테이블의 최대값보다 큰 경우|DBCC checkident (*table_name*, NORESEED) 열의 현재 최대값을 확인 한 다음 해당 값을 지정 하는 *new_reseed_value* 을 DBCC checkident (*table_ 이름*, RESEED,*new_reseed_value*) 명령입니다.<br /><br /> -또는-<br /><br /> DBCC checkident (*table_name*, RESEED,*new_reseed_value*)와 *new_reseed_value* 매우 낮은 값으로 설정 하 고 DBCC CHECKIDENT를 실행 한 다음 ( *table_name*, RESEED) 하 고 값을 수정 합니다.|  
|모든 행이 테이블에서 삭제되는 경우|DBCC checkident (*table_name*, RESEED,*new_reseed_value*)와 *new_reseed_value* 원하는 시작 값으로 설정 합니다.|  
  
## <a name="changing-the-seed-value"></a>초기값 변경  
 초기값은 테이블에 로드되는 제일 첫 번째 행에 대한 ID 열에 삽입되는 값입니다. 현재 ID 값이 테이블 또는 뷰에서 생성된 마지막 ID 값인 경우 이후의 모든 행에는 현재 ID 값과 증가값이 포함됩니다.  
  
 DBCC CHECKIDENT는 다음과 같은 태스크를 수행하는 데 사용할 수 없습니다.  
  
-   테이블 또는 뷰에서 ID 열을 만드는 동안 지정된 원래 초기값을 변경합니다.  
  
-   테이블 또는 뷰에서 기존 행의 초기값을 다시 설정합니다.  
  
 원래 초기값을 변경하고 기존 행의 초기값을 다시 설정하려면 ID 열을 삭제하고 새로운 초기값을 지정하여 다시 만들어야 합니다. 테이블에 데이터가 포함된 경우 지정된 초기값 및 증가값을 사용하여 기존 행에 ID 번호가 추가됩니다. 행이 업데이트되는 순서는 보장되지 않습니다.  
  
## <a name="result-sets"></a>결과 집합  
 ID 열이 포함된 테이블의 경우 DBCC CHECKIDENT는 옵션 지정 여부에 관계없이 모든 작업에 대해 다음 메시지를 반환합니다. 새 초기값을 지정할 때는 예외입니다.  
  
`Checking identity information: current identity value '\<current identity value>', current column value '\<current column value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
 DBCC CHECKIDENT가 사용 하는 다시 시드를 사용 하 여 새 초기값을 지정 하는 경우 *new_reseed_value*, 다음 메시지가 반환 됩니다.  
  
`Checking identity information: current identity value '\<current identity value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Permissions  
 호출자는 테이블을 포함 하는 스키마를 소유 하거나의 멤버는 **sysadmin** 고정 서버 역할의 **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-resetting-the-current-identity-value-if-it-is-needed"></a>1. 필요에 따라 현재 ID 값 다시 설정  
 다음 예에서는 필요에 따라 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 지정된 테이블의 현재 ID 값을 다시 설정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType');  
GO  
```  
  
### <a name="b-reporting-the-current-identity-value"></a>2. 현재 ID 값 보고  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 지정된 테이블의 현재 ID 값을 보고하고, ID 값이 잘못되었더라도 그 값을 수정하지 않습니다.  
  
```  
USE AdventureWorks2012;   
GO  
DBCC CHECKIDENT ('Person.AddressType', NORESEED);   
GO  
  
```  
  
### <a name="c-forcing-the-current-identity-value-to-a-new-value"></a>3. 현재 ID 값을 새로운 값으로 설정  
 다음 예에서는 `AddressTypeID` 테이블에 있는 `AddressType` 열의 현재 ID 값을 10으로 강제 설정합니다. 이 테이블에는 기존 행이 있으므로 다음에 삽입되는 행은 열에 대해 정의된 현재 새 증분 값에 1을 더한 11을 값으로 사용합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType', RESEED, 10);  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목:  
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
[ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)  
[USE&#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
[IDENT_SEED &#40; Transact SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)  
[IDENT_INCR &#40; Transact SQL &#41;](../../t-sql/functions/ident-incr-transact-sql.md)  
  
  
