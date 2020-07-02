---
title: sp_tableoption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tableoption_TSQL
- sp_tableoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tableoption
ms.assetid: 0a57462c-1057-4c7d-bce3-852cc898341d
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 84e6c530b4887502346b69adcf2590bce9d0e8fc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718686"
---
# <a name="sp_tableoption-transact-sql"></a>sp_tableoption(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  사용자 정의 테이블의 옵션 값을 설정합니다. sp_tableoption를 사용 하 여 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **text**, **ntext**, **image**또는 large 사용자 정의 형식 열이 있는 테이블의 행 내부 동작을 제어할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 text in row 기능이 제거됩니다. 대량 값 데이터를 저장 하려면 **varchar (max)**, **nvarchar (max)** 및 **varbinary (max)** 데이터 형식을 사용 하는 것이 좋습니다.  
  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_tableoption [ @TableNamePattern = ] 'table'   
     , [ @OptionName = ] 'option_name'   
     ,[ @OptionValue =] 'value'  
```  
  
## <a name="arguments"></a>인수  
 [ @TableNamePattern =] '*테이블*'  
 사용자 정의 데이터베이스 테이블의 정규화 또는 비정규화된 이름입니다. 데이터베이스 이름을 포함한 정규화된 테이블 이름인 경우 데이터베이스 이름이 반드시 현재 데이터베이스의 이름이어야 합니다. 여러 테이블에 대한 테이블 옵션을 동시에 설정할 수 없습니다. *테이블* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
 [ @OptionName =] '*option_name*'  
 테이블 옵션 이름입니다. *option_name* 는 **varchar (35)** 이며 기본값은 NULL이 아닙니다. *option_name* 는 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|table lock on bulk load|기본값이 해제되면 사용자 정의 테이블에 대량 로드 처리를 수행하여 행 잠금을 얻습니다. 기본값이 설정되면 사용자 정의 테이블에 대량 로드 처리를 수행하여 대량 업데이트 잠금을 얻습니다.|  
|insert row lock|더 이상 지원되지 않습니다.<br /><br /> 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 잠금 동작에 영향을 주지 않으며 기존 스크립트 및 프로시저와의 호환성을 위해 포함됩니다.|  
|text in row|OFF 또는 0(해제, 기본값)이면 현재 동작을 바꾸지 않으며 행에 BLOB이 없습니다.<br /><br /> 지정 된 경우 @OptionValue (enabled) 또는 24에서 7000 사이의 정수 값을 지정 하면 새 **text**, **ntext**또는 **image** 문자열이 데이터 행에 직접 저장 됩니다. BLOB 값이 업데이트 될 때 기존의 모든 BLOB (binary large object: **text**, **ntext**또는 **image** 데이터)는 text in row 형식으로 변경 됩니다. 자세한 내용은 설명 부분을 참조하세요.|  
|large value types out of row|1 = **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml** 및 초대형 UDT (사용자 정의 형식) 열은 루트에 대 한 16 바이트 포인터와 함께 행 외부에 저장 됩니다.<br /><br /> 0 = **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml** 및 large UDT 값은 최대 8000 바이트까지 데이터 행에 직접 저장 되며, 값이 레코드에 맞을 수 있습니다. 값이 레코드에 맞지 않으면 포인터는 행 내부에 저장되고 나머지는 행 외부 LOB 스토리지 공간에 저장됩니다. 0이 기본값입니다.<br /><br /> Large UDT (사용자 정의 형식)는 이상에 적용 됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] <br /><br /> [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 의 TEXTIMAGE_ON 옵션을 사용 하 여 대량 데이터 형식의 저장소 위치를 지정할 수 있습니다. |  
|vardecimal storage format|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> TRUE, ON 또는 1이면 지정된 테이블을 VarDecimal 스토리지 형식에 사용할 수 있습니다. FALSE, OFF 또는 0이면 지정된 테이블을 VarDecimal 스토리지 형식에 사용할 수 없습니다. Vardecimal 저장소 형식은 [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)를 사용 하 여 데이터베이스에서 vardecimal 저장소 형식을 사용 하도록 설정한 경우에만 사용할 수 있습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]이상에서 **vardecimal** 저장소 형식은 더 이상 사용 되지 않습니다. 대신 ROW 압축을 사용하세요. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요. 0이 기본값입니다.|  
  
 [ @OptionValue =] '*value*'  
 *Option_name* 사용 (TRUE, ON 또는 1) 또는 해제 (FALSE, OFF 또는 0) 인지 여부입니다. *값* 은 **varchar (12)** 이며 기본값은 없습니다. *값* 은 대/소문자를 구분 하지 않습니다.  
  
 유효한 text in row 옵션 값은 0, ON, OFF 또는 24에서 7000까지의 정수입니다. *값* 을 ON으로 설정 하면 기본적으로 256 바이트로 제한 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 오류 번호(실패)  
  
## <a name="remarks"></a>설명  
 sp_tableoption은 사용자 정의 테이블의 옵션 값을 설정할 때만 사용합니다. 테이블 속성을 표시 하려면 OBJECTPROPERTY 또는 query sys.debug를 사용 합니다.  
  
 sp_tableoption의 text in row 옵션은 텍스트 열을 포함하는 테이블에서만 설정 또는 해제될 수 있습니다. 테이블에 텍스트 열이 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 발생합니다.  
  
 Text in row 옵션을 설정 하면 @OptionValue 사용자가이 매개 변수를 사용 하 여 BLOB에 대 한 행에 저장 되는 최대 크기를 지정할 수 있습니다. 기본값은 256바이트이며 24에서 7000바이트까지의 범위에서 값을 지정할 수 있습니다.  
  
 **text**, **ntext**또는 **image** 문자열은 다음 조건이 적용 되는 경우 데이터 행에 저장 됩니다.  
  
-   text in row가 설정된 경우  
  
-   문자열의 길이가에 지정 된 제한 보다 짧은 경우@OptionValue  
  
-   데이터 행에 사용할 수 있는 충분한 공간이 있을 경우  
  
 BLOB 문자열이 데이터 행에 저장 된 경우 **text**, **ntext**또는 **image** 문자열을 읽고 쓰는 것은 문자와 이진 문자열을 읽거나 쓰는 것 만큼 빠를 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 BLOB 문자열을 읽거나 쓰기 위해 별도의 페이지에 액세스할 필요가 없습니다.  
  
 **Text**, **ntext**또는 **image** 문자열이 행에서 지정 된 제한 또는 사용 가능한 공간 보다 큰 경우에는 포인터가 행에 대신 저장 됩니다. 하지만 이 경우에도 행에 BLOB 문자열을 저장하기 위한 조건이 적용됩니다. 포인터를 저장할 때도 데이터 행에 충분한 공간이 필요합니다.  
  
 테이블 행에 저장된 BLOB 문자열 및 포인터는 가변 길이 문자열과 비슷하게 취급됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 문자열 또는 포인터를 저장하는 데 필요한 바이트 수만 사용됩니다.  
  
 기존 BLOB 문자열은 text in row가 처음 설정될 때 즉시 변환되지 않고 업데이트될 때만 변환됩니다. 마찬가지로 text in row 옵션 제한을 늘리면 데이터 행에 이미 있는 **text**, **ntext**또는 **image** 문자열이 업데이트 될 때까지 새 제한을 따르도록 변환 되지 않습니다.  
  
> [!NOTE]  
>  text in row 옵션을 해제하거나 옵션의 제한 값을 줄이려면 모든 BLOB을 변환해야 하므로 변환해야 하는 BLOB 문자열 수에 따라 프로세스가 오래 걸릴 수도 있습니다. 변환을 처리하는 동안 테이블은 잠깁니다.  
  
 테이블 변수를 반환하는 함수를 포함한 테이블 변수의 경우 text in row 옵션이 기본 인라인 제한 값 256으로 자동 설정됩니다. 이 옵션은 변경되지 않습니다.  
  
 text in row 옵션은 TEXTPTR, WRITETEXT, UPDATETEXT 및 READTEXT 함수를 지원합니다. SUBSTRING() 함수를 사용하여 BLOB을 부분적으로 읽을 수 있지만 행 내부 텍스트 포인터에는 다른 텍스트 포인터와는 다른 기간 및 숫자 제한이 있습니다.  
  
 테이블의 VarDecimal 스토리지 형식을 일반 Decimal 스토리지 형식으로 변경하려면 데이터베이스는 단순 복구 모드이어야 합니다. 복구 모드를 변경하면 백업 목적의 로그 체인이 끊어지므로 테이블에서 VarDecimal 스토리지 형식을 제거한 후 전체 데이터베이스 백업을 만들어야 합니다.  
  
 기존 LOB 데이터 형식 열 (text, ntext 또는 image)을 중소 규모의 큰 값 유형 (varchar (max), nvarchar (max) 또는 varbinary (max))으로 변환 하는 경우 대부분의 문은 사용자 환경에서 큰 값 유형 열을 참조 하지 않으므로 최적의 성능을 얻기 위해 **large_value_types_out_of_row** 를 **1** 로 변경 하는 것이 좋습니다. **Large_value_types_out_of_row** 옵션 값이 변경 되 면 기존 varchar (max), nvarchar (max), varbinary (max) 및 xml 값이 즉시 변환 되지 않습니다. 문자열의 스토리지는 이후에 업데이트될 때 변경됩니다. 테이블에 삽입되는 새 값은 적용된 테이블 옵션에 따라 저장됩니다. 즉각적인 결과를 위해 데이터의 복사본을 만든 다음, **large_value_types_out_of_row** 설정을 변경 하 고 각 작은-보통 크기의 작은 값 유형 열을 자동으로 업데이트 하 여 문자열의 저장소가 적용 되는 테이블 옵션으로 변경 되도록 합니다. 테이블을 압축하려면 업데이트 또는 다시 채우기 후 테이블에 대한 인덱스를 다시 빌드하세요. 
    
  
## <a name="permissions"></a>사용 권한  
 sp_tableoption을 실행하려면 테이블에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-storing-xml-data-out-of-the-row"></a>A. xml 데이터를 행 외부에 저장  
 다음 예에서는 테이블의 **xml** 데이터를 행 외부에 저장 하도록 지정 합니다 `HumanResources.JobCandidate` .  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'HumanResources.JobCandidate', 'large value types out of row', 1;  
```  
  
### <a name="b-enabling-vardecimal-storage-format-on-a-table"></a>B. 테이블에 VarDecimal 스토리지 형식 사용  
 다음 예에서는 테이블을 수정 `Production.WorkOrderRouting` 하 여 `decimal` 데이터 형식을 저장소 형식으로 저장 합니다 `vardecimal` .  

```sql  
USE master;  
GO  
-- The database must be enabled for vardecimal storage format  
-- before a table can be enabled for vardecimal storage format  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'Production.WorkOrderRouting',   
   'vardecimal storage format', 'ON';  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys. Transact-sql &#40;&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
