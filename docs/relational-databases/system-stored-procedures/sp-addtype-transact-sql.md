---
title: sp_addtype (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addtype
- sp_addtype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addtype
ms.assetid: ed72cd8e-5ff7-4084-8458-2d8ed279d817
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eefd9b73f4e249df57aa03ef0453a864eab2fd77
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838851"
---
# <a name="spaddtype-transact-sql"></a>sp_addtype(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  별칭 데이터 형식을 만듭니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addtype [ @typename = ] type,   
    [ @phystype = ] system_data_type   
    [ , [ @nulltype = ] 'null_type' ] ;  
```  
  
## <a name="arguments"></a>인수  
 [  **@typename=** ] *형식*  
 별칭 데이터 형식의 이름입니다. 별칭 데이터 형식 이름에 대 한 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md) 각 데이터베이스에서 고유 해야 합니다. *형식* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@phystype=**] *system_data_type*  
 실제 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 별칭 데이터 형식의 기반이 되는 데이터 형식을 제공 합니다. *system_data_type* 됩니다 **sysname**기본값은 없고 수 이며 다음이 값 중 하나일 수:  
  
||||  
|-|-|-|  
|**bigint**|**binary(n)**|**bit**|  
|**char(n)**|**datetime**|**decimal**|  
|**float**|**image**|**int**|  
|**money**|**nchar(n)**|**ntext**|  
|**numeric**|**nvarchar(n)**|**real**|  
|**smalldatetime**|**smallint**|**smallmoney**|  
|**sql_variant**|**text**|**tinyint**|  
|**uniqueidentifier**|**varbinary(n)**|**varchar(n)**|  
  
 중간 공백 또는 구두점이 있는 매개 변수는 모두 따옴표로 묶어야 합니다. 사용 가능한 데이터 형식에 대 한 자세한 내용은 참조 하세요. [데이터 형식 &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)합니다.  
  
 *n*  
 선택된 데이터 형식의 길이를 표시하는 음이 아닌 정수입니다.  
  
 *P*  
 소수점 왼쪽과 오른쪽에 저장할 수 있는 최대 총 십진 자릿수를 표시하는 음이 아닌 정수입니다. 자세한 내용은 [decimal 및 numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)을 참조하세요.  
  
 *S*  
 소수점 오른쪽에 저장할 수 있는 최대 십진 자릿수를 표시하는 음이 아닌 정수이며 전체 자릿수보다 작거나 같아야 합니다. 자세한 내용은 [decimal 및 numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)을 참조하세요.  
  
 [  **@nulltype =** ] **'***null_type***'**  
 별칭 데이터 형식의 NULL 값 처리 방식을 나타냅니다. *null_type* 은 **varchar (** 8 **)**, 기본값은 NULL 사용 하 여 작은따옴표 ('NULL', 'NOT NULL' 또는 'NONULL')로 묶어야 하 고 있습니다. 하는 경우 *null_type* 하 여 명시적으로 정의 되지 않은 **sp_addtype**, 현재의 기본 null 허용 여부로 설정 됩니다. GETANSINULL 시스템 함수를 사용하면 현재의 기본 NULL 허용 여부를 확인할 수 있습니다. 이것은 SET 문 또는 ALTER DATABASE를 사용하여 조정될 수 있습니다. NULL 허용 여부는 명시적으로 정의해야 합니다. 하는 경우 **@phystype** 는 **비트**, 및 **@nulltype** 지정 하지 않으면 기본값은 NULL입니다.  
  
> [!NOTE]  
>  합니다 *null_type* 매개 변수에이 데이터 형식의 기본 null 허용 여부를 정의 합니다. 테이블을 만드는 동안 별칭 데이터 형식을 사용할 때 NULL 허용 여부를 명시적으로 정의하면 정의된 NULL 허용 여부보다 우선적으로 적용됩니다. 자세한 내용은 [ALTER TABLE &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md) 하 고 [CREATE TABLE &#40;Transact SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 별칭 데이터 형식 이름은 데이터베이스 내에서 고유해야 하지만 이름이 서로 다른 별칭 데이터 형식은 같은 정의를 사용할 수 있습니다.  
  
 실행 **sp_addtype** 에 표시 되는 별칭 데이터 형식을 만듭니다 합니다 **sys.types** 카탈로그 뷰는 특정 데이터베이스에 대 한 합니다. 별칭 데이터 형식에는 모든 새 사용자 정의 데이터베이스에서 사용할 수 있어야 하면 추가 되도록 **모델**합니다. 별칭 데이터 형식을 만든 다음 이 형식을 CREATE TABLE 또는 ALTER TABLE에서 사용할 수 있으며 별칭 데이터 형식에 기본값 및 규칙을 바인딩할 수 있습니다. 사용 하 여 만든 모든 스칼라 별칭 데이터 형식은 **sp_addtype** 에 포함 된 합니다 **dbo** 스키마입니다.  
  
 별칭 데이터 형식은 데이터베이스의 기본 데이터 정렬을 상속합니다. 에 정의 된 열의 데이터 정렬 및 별칭 형식의 변수를 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE, ALTER TABLE 및 DECLARE @*local_variable* 문입니다. 데이터베이스의 기본 데이터 정렬을 변경하면 해당 형식의 새 열과 변수에만 적용되고 기존 열과 변수의 데이터 정렬은 변경되지 않습니다.  
  
> [!IMPORTANT]  
>  이전 버전과 호환성을 위해 합니다 **공개** 데이터베이스 역할에는 사용 하 여 만들어진 별칭 데이터 형식에 대 한 REFERENCES 권한이 자동으로 부여 됩니다 **sp_addtype**합니다. 별칭 데이터 형식 대신 CREATE TYPE 문을 사용 하 여 만든 경우 유의 **sp_addtype**, 없습니다 이러한 권한이 자동으로 부여 합니다.  
  
 별칭 데이터 형식을 사용 하 여 정의할 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **타임 스탬프**, **테이블**를 **xml**, **varchar (max)** 합니다 **nvarchar (max)** 나 **varbinary (max)** 데이터 형식입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **db_owner** 하거나 **db_ddladmin** 고정된 데이터베이스 역할.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-an-alias-data-type-that-does-not-allow-for-null-values"></a>1. NULL 값을 허용하지 않는 별칭 데이터 형식 만들기  
 다음 예제에서는 명명 된 별칭 데이터 형식 `ssn` (사회 보장 번호) 기반으로 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-제공 **varchar** 데이터 형식입니다. `ssn` 데이터 형식은 11자리의 주민 등록 번호(999-99-9999)를 보유하는 열에 사용됩니다. 이 열은 NULL이 될 수 없습니다.  
  
 `varchar(11)`는 문장 부호(괄호)를 포함하고 있으므로 작은따옴표로 묶어야 합니다.  
  
```  
USE master;  
GO  
EXEC sp_addtype ssn, 'varchar(11)', 'NOT NULL';  
GO  
```  
  
### <a name="b-creating-an-alias-data-type-that-allows-for-null-values"></a>2. NULL 값을 허용하는 별칭 데이터 형식 만들기  
 다음 예에서는 NULL 값을 허용하는 `datetime`라는 별칭 데이터 형식(`birthday` 기반)을 만듭니다.  
  
```  
USE master;  
GO  
EXEC sp_addtype birthday, datetime, 'NULL';  
```  
  
### <a name="c-creating-additional-alias-data-types"></a>3. 추가 별칭 데이터 형식 만들기  
 다음 예에서는 국내 및 국제 전화 및 팩스 번호 모두에 대해 두 개의 추가 별칭 데이터 형식인 `telephone` 및 `fax`를 만듭니다.  
  
```  
USE master;  
GO  
EXEC sp_addtype telephone, 'varchar(24)', 'NOT NULL';  
GO  
EXEC sp_addtype fax, 'varchar(24)', 'NULL';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindefault&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_droptype &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
