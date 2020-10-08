---
title: SSVARIANT 구조체(OLE DB 드라이버)
description: OLE DB Driver for SQL Server의 SSVARIANT 구조
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6cef1fb9b92df92cba00ea9e9aa8c9591e887a6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727237"
---
# <a name="ssvariant-structure"></a>SSVARIANT 구조
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  msoledbsql.h에 정의된 **SSVARIANT** 구조는 OLE DB Driver for SQL Server의 DBTYPE_SQLVARIANT 값에 해당합니다.  
  
 **SSVARIANT**는 판별 공용 구조체입니다. vt 멤버의 값에 따라 소비자는 읽을 멤버를 결정할 수 있습니다. vt 값은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에 해당하므로 **SSVARIANT** 구조는 모든 SQL Server 형식을 보유할 수 있습니다. 표준 OLE DB 형식의 데이터 구조에 대한 자세한 내용은 [형식 표시기](/previous-versions/windows/desktop/ms711251(v=vs.85))를 참조하세요.  
  
## <a name="remarks"></a>설명  
 DataTypeCompat==80인 경우, 여러 **SSVARIANT** 하위 유형이 문자열이 됩니다. 예를 들면 다음 vt 값이 **SSVARIANT**에 VT_SS_WVARSTRING으로 나타납니다.  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 DateTypeCompat == 0인 경우, 이러한 유형은 네이티브 형식으로 나타납니다.  
  
 SSPROP_INIT_DATATYPECOMPATIBILITY에 대한 내용은 [OLE DB Driver for SQL Server에서 연결 문자열 키워드 사용](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)을 참조하세요.  
  
 msoledbsql.h 파일에는 **SSVARIANT** 구조에서 멤버 유형 역참조를 단순화하는 변형 액세스 매크로가 있습니다. 예로는 다음과 같이 사용 가능한 V_SS_DATETIMEOFFSET가 있습니다.  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 **SSVARIANT** 구조의 각 멤버에 대한 액세스 매크로의 전체 집합은 msoledbsql.h 파일을 참조하세요.  
  
 다음 표에서는 **SSVARIANT** 구조의 멤버를 설명합니다.  
  
|멤버|OLE DB 유형 표시기|OLE DB C 데이터 형식|vt 값|주석|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||**SSVARIANT** 구조에 포함된 값 유형을 지정합니다.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|**tinyint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|**smallint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|**int**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|**bigint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|**real**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|**float**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|**money** 및 **smallmoney**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|**bit**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|**uniqueidentifier**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|**numeric**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|**date**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|**smalldatetime**, **datetime** 및 **datetime2**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|**time**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *tTime2Val*(**DBTIME2**)<br /><br /> *bScale*(**BYTE**) *tTime2Val* 값의 소수 자릿수를 지정합니다.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|**datetime2**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *tsDataTimeVal*(DBTIMESTAMP)<br /><br /> *bScale*(**BYTE**) *tsDataTimeVal* 값의 소수 자릿수를 지정합니다.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|**datetimeoffset**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *tsoDateTimeOffsetVal*(**DBTIMESTAMPOFFSET**)<br /><br /> *bScale*(**BYTE**) *tsoDateTimeOffsetVal* 값의 소수 자릿수를 지정합니다.|  
|NCharVal|해당하는 OLE DB 유형 표시기 없음|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|**nchar** 및 **nvarchar**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *sActualLength*(**SHORT**) *pwchNCharVal*이 가리키는 문자열의 실제 길이를 지정합니다. 이 값은 0으로 끝나지 않습니다.<br /><br /> *sMaxLength*(**SHORT**) *pwchNCharVal*이 가리키는 문자열의 최대 길이를 지정합니다.<br /><br /> *pwchNCharVal*(**WCHAR** \*) 문자열에 대한 포인터입니다.<br /><br /> *rgbReserved*(**BYTE[5]** ) 데이터 정렬 정보를 지정합니다.<br /><br /> 사용되지 않은 멤버: *dwReserved* 및 *pwchReserved*.|  
|CharVal|해당하는 OLE DB 유형 표시기 없음|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|**char** 및 **varchar**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *sActualLength*(**SHORT**) *pchCharVal*이 가리키는 문자열의 실제 길이를 지정합니다. 이 값은 0으로 끝나지 않습니다.<br /><br /> *sMaxLength*(**SHORT**) *pchCharVal*이 가리키는 문자열의 최대 길이를 지정합니다.<br /><br /> *pchCharVal*(**CHAR** \*) 문자열에 대한 포인터입니다.<br /><br /> *rgbReserved*(**BYTE[5]** ) 데이터 정렬 정보를 지정합니다.<br /><br /> 사용되지 않은 멤버:<br /><br /> *dwReserved* 및 *pwchReserved*.|  
|BinaryVal|해당하는 OLE DB 유형 표시기 없음|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|**binary** 및 **varbinary**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *sActualLength*(**SHORT**) *prgbBinaryVal*이 가리키는 문자열의 실제 길이를 지정합니다.<br /><br /> *sMaxLength*(**SHORT**) *prgbBinaryVal*이 가리키는 문자열의 최대 길이를 지정합니다.<br /><br /> *prgbBinaryVal*(**BYTE** \*) 이진 데이터에 대한 포인터입니다.<br /><br /> 사용되지 않는 멤버: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
## <a name="known-issues"></a>알려진 문제
### <a name="possible-narrow-string-data-corruption"></a>좁은 문자열 데이터 손상 가능성
OLE DB 드라이버 버전 18.4보다 이전에는 다음 조건이 모두 true일 경우 `sql_variant` 열에 삽입하면 서버에서 데이터가 손상될 수 있습니다.
- 클라이언트 컴퓨터 코드 페이지가 데이터베이스 데이터 정렬 코드 페이지와 일치하지 않습니다.
- 삽입할 클라이언트 버퍼가 코드 페이지에 인코딩된 비 ASCII 좁은 문자열 문자를 포함합니다.
- 다음 조건 중 하나가 true입니다.
  - `sql_variant` 열에 해당하는 매개 변수를 설명하는 `DBPARAMBINDINFO` 구조의 `pwszDataSourceType` 필드가 `L"DBTYPE_SQLVARIANT"`, `L"DBTYPE_VARIANT"`또는 `L"sql_variant"`로 설정되었습니다. 자세한 내용은 다음을 참조하세요. [ICommandWithParameters::SetParameterInfo](/previous-versions/windows/desktop/ms725393(v=vs.85)).

    *or*
  - 삽입에 사용되는 매개 변수가 있는 SQL 쿼리가 준비되었습니다.

구체적으로 말하면 OLE DB 드라이버는 데이터 삽입 전에 데이터를 데이터베이스 데이터 정렬 코드 페이지로 변환하지 않았습니다. 그러나 드라이버가 데이터베이스 데이터 정렬 코드 페이지에서 데이터가 인코딩되었다고 서버에 잘못 표시한 것입니다. 이 동작으로 인해 데이터와 `sql_variant` 열에 저장된 해당 코드 페이지가 일치하지 않습니다.

마찬가지로, 동일한 값을 검색할 때 OLE DB 드라이버는 문자열을 클라이언트 코드 페이지로 변환하지 않았습니다. 그러나 삽입된 데이터는 이미 클라이언트 코드 페이지에 있기 때문에(위 단락 참조) 클라이언트 애플리케이션이 데이터를 올바르게 해석할 수 있습니다. 그렇더라도 다른 드라이버를 사용하는 애플리케이션은 이러한 값을 손상된 형식으로 검색할 수 있습니다. 다른 드라이버가 데이터베이스 데이터 정렬 코드 페이지의 문자열을 해석하고 클라이언트 코드 페이지로 변환하려고 시도했기 때문에 손상이 발생합니다.

18.4 버전부터 OLE DB 드라이버는 좁은 문자열을 삽입 전에 데이터베이스 데이터 정렬 코드 페이지로 변환합니다. 마찬가지로 드라이버는 데이터를 검색할 때 다시 클라이언트 코드 페이지로 변환합니다. 따라서 위에 언급된 버그를 사용하는 클라이언트 애플리케이션은 이전 버전의 OLE DB 드라이버를 사용하여 삽입된 데이터를 검색할 때 문제가 발생할 수 있습니다. 아래 [복구 절차](#recovery-procedure)는 이러한 문제를 해결하기 위한 지침을 제공합니다.

### <a name="recovery-procedure"></a>복구 절차
> [!IMPORTANT]  
> 아래 복구 단계를 수행하기 전에 기존 데이터를 백업해야 합니다.

OLE DB 드라이버 버전 18.4로 전환한 후 애플리케이션이 `sql_variant` 열에서 데이터를 검색하는 데 문제가 발생하는 경우 데이터가 저장되는 데이터베이스와 동일한 데이터 정렬을 갖도록 손상된 데이터를 수정해야 합니다. 다음 스크립트를 사용하여 `sql_variant` 열에서 단일 값을 복구할 수 있습니다. 이 스크립트는 템플릿이며 사용자가 시나리오에 맞게 조정해야 합니다.

> [!IMPORTANT]  
> 데이터의 원래 코드 페이지가 저장되지 않으므로 데이터를 처음 인코딩한 방법을 서버에 알려주어 야 합니다. 이렇게 하려면 처음에 데이터를 삽입한 클라이언트의 코드 페이지와 동일한 코드 페이지를 갖는 데이터베이스의 컨텍스트 내에서 스크립트를 실행합니다. 예를 들어 손상된 데이터가 코드 페이지 `932`로 구성된 클라이언트로부터 삽입된 경우 다음 스크립트를 일본어 데이터 정렬(예: `Japanese_XJIS_100_CS_AI`)을 사용하는 데이터베이스의 컨텍스트 내에서 실행해야 합니다.

```sql
/*
    Description:
        Template that can be used to recover the corrupted value inserted into the sql_variant column.

    Scenario:
        The database is named [YourDatabase] and it contains a table named [YourTable], which contains the corrupted value.
        Schema is named [dbo].
        The corrupted value is stored in a column of type sql_variant named [YourColumn].
        The corrupted value is sql_variant of BaseType char. For details on sql_variant properties, see:
            https://docs.microsoft.com/sql/t-sql/functions/sql-variant-property-transact-sql
*/

-- Base type in sql_variant can hold a maximum of 8000 bytes
-- For details see: 
--  https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql#remarks
DECLARE @bin VARBINARY(8000)

-- In the following lines we convert the sql_variant base type to binary.
-- <FilterExpression>
--      Is a placeholder and must be replaced with an expression that filters a single corrupted value to be recovered.
--      Therefore, the expression must result in a single value being returned only.
SET @bin = (SELECT CAST([YourColumn] AS VARBINARY(8000)) FROM [YourDatabase].[dbo].[YourTable] WHERE <FilterExpression>)

-- In the following lines we store the binary value in char(59) (a fixed-size character data type).
-- IMPORTANT NOTE: 
--      This example assumes the corrupted sql_variant's base type is char(59).
--      You MUST adjust the type (that is, char/varchar) and size to match your scenario exactly.
DECLARE @char CHAR(59)
SET @char = CAST((@bin) AS CHAR(59))
DECLARE @sqlvariant sql_variant

-- The following lines recover the corrupted value by translating the value to the collation of the database.
-- <DBCollation>
--      Must be replaced with the collation (for example, Latin1_General_100_CI_AS_SC_UTF8) of the database holding the data.
SET @sqlvariant = @char collate <DBCollation>

-- Finally, we update the corrupted value with the recovered value.
-- "<FilterExpression>"
--      Is a placeholder and must be replaced with an expression that filters a single corrupted value to be recovered.
--      Therefore, the expression must result in a single value being returned only.
UPDATE [YourDatabase].[dbo].[YourTable] SET [YourColumn] = @sqlvariant WHERE <FilterExpression>
```

## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
