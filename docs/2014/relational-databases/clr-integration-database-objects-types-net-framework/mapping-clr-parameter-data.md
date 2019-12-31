---
title: CLR 매개 변수 데이터 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 17eeefbe125722c666f9f56394028da8c66a66b3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232277"
---
# <a name="mapping-clr-parameter-data"></a>CLR 매개 변수 데이터 매핑
  다음 표에서는 데이터 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `System.Data.SqlTypes` 네임 스페이스의에 대 한 CLR (공용 언어 런타임)의 해당 형식 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework의 해당 네이티브 clr에 해당 하는 데이터 형식을 보여 줍니다.  
  
||||  
|-|-|-|  
|**SQL Server 데이터 형식**|System.Data.SqlTypes 또는 Microsoft.SqlServer.Types의 형식|**CLR 데이터 형식(.NET Framework)**|  
|`bigint`|`SqlInt64`|**Int64, Nullable\<int64>**|  
|`binary`|`SqlBytes, SqlBinary`|`Byte[]`|  
|`bit`|`SqlBoolean`|**부울, Nullable\<부울>**|  
|`char`|없음|없음|  
|`cursor`|없음|없음|  
|`date`|`SqlDateTime`|**DateTime, Nullable\<datetime>**|  
|`datetime`|`SqlDateTime`|**DateTime, Nullable\<datetime>**|  
|`datetime2`|없음|**DateTime, Nullable\<datetime>**|  
|`DATETIMEOFFSET`|`None`|**DateTimeOffset, Nullable\<DateTimeOffset>**|  
|`decimal`|`SqlDecimal`|**Decimal, Nullable\<decimal>**|  
|`float`|`SqlDouble`|**Double, Nullable\<double>**|  
|`geography`|`SqlGeography`<br /><br /> `SqlGeography`는 SQL Server와 함께 설치 되 고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=53164)에서 다운로드할 수 있는 Microsoft. i m l. d l l .dll에 정의 되어 있습니다.|없음|  
|`geometry`|`SqlGeometry`<br /><br /> `SqlGeometry`는 SQL Server와 함께 설치 되 고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=53164)에서 다운로드할 수 있는 Microsoft. i m l. d l l .dll에 정의 되어 있습니다.|없음|  
|`hierarchyid`|`SqlHierarchyId`<br /><br /> `SqlHierarchyId`는 SQL Server와 함께 설치 되 고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=53164)에서 다운로드할 수 있는 Microsoft. i m l. d l l .dll에 정의 되어 있습니다.|없음|  
|`image`|없음|없음|  
|`int`|`SqlInt32`|**Int32, Nullable\<int32>**|  
|`money`|`SqlMoney`|**Decimal, Nullable\<decimal>**|  
|`nchar`|`SqlChars, SqlString`|`String, Char[]`|  
|`ntext`|없음|없음|  
|`numeric`|`SqlDecimal`|**Decimal, Nullable\<decimal>**|  
|`nvarchar`|`SqlChars, SqlString`<br /><br /> 
  `SQLChars`는 데이터 전송 및 액세스에 더 적합하고 `SQLString`은 문자열 작업에 더 적합합니다.|`String, Char[]`|  
|`nvarchar(1), nchar(1)`|`SqlChars, SqlString`|**Char, String, Char [], Nullable\<문자>**|  
|`real`|
  `SqlSingle`(`SqlSingle` 범위, 단, `real`보다 큼)|**단일 Nullable\<단일>**|  
|`rowversion`|없음|`Byte[]`|  
|`smallint`|`SqlInt16`|**Int16, Nullable\<int16>**|  
|`smallmoney`|`SqlMoney`|**Decimal, Nullable\<decimal>**|  
|`sql_variant`|없음|`Object`|  
|`table`|없음|없음|  
|`text`|없음|없음|  
|`time`|없음|**TimeSpan, Nullable\<timespan>**|  
|`timestamp`|없음|없음|  
|`tinyint`|`SqlByte`|**바이트, Nullable\<바이트>**|  
|`uniqueidentifier`|`SqlGuid`|**Guid, Nullable\<guid>**|  
|`User-defined type(UDT)`|없음|동일한 어셈블리 또는 종속 어셈블리의 사용자 정의 형식에 바인딩된 동일한 클래스입니다.|  
|**varbinary**|`SqlBytes, SqlBinary`|`Byte[]`|  
|`varbinary(1), binary(1)`|`SqlBytes, SqlBinary`|**byte, Byte [], Nullable\<바이트>**|  
|`varchar`|없음|없음|  
|`xml`|`SqlXml`|없음|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Out 매개 변수로 자동 데이터 형식 변환  
 CLR 메서드는 `out` 한정자(Microsoft Visual C#) 또는 `<Out()> ByRef`(Microsoft Visual Basic)로 입력 매개 변수를 표시하여 호출 코드나 프로그램에 정보를 반환할 수 있습니다. 입력 매개 변수가 `System.Data.SqlTypes` 네임스페이스의 CLR 데이터 형식이고 호출 프로그램이 이에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 입력 매개 변수로 지정할 경우 CLR 메서드가 데이터 형식을 반환하면 자동으로 형식 변환이 수행됩니다.  
  
 예를 들어 다음 CLR 저장 프로시저에는 `SqlInt32`(C#) 또는 `out`(Visual Basic)로 표시된 `<Out()> ByRef` CLR 데이터 형식의 입력 매개 변수가 있습니다.  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 어셈블리가 데이터베이스에서 만들어진 후에는 저장 프로시저가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 OUTPUT 매개 변수로 지정하는 다음 Transact-SQL을 사용하여 `int`에서 만들어집니다.  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 CLR 저장 프로시저 호출되면 `SqlInt32` 데이터 형식이 자동으로 `int` 데이터 형식으로 변환되고 호출 프로그램에 반환됩니다.  
  
 그러나 Out 매개 변수를 통해 모든 CLR 데이터 형식을 이에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환할 수는 없습니다. 다음 표에서는 이러한 예외를 보여 줍니다.  
  
|||  
|-|-|  
|**CLR 데이터 형식(SQL Server)**|**SQL Server 데이터 형식**|  
|`Decimal`|smallmoney|  
|`SqlMoney`|smallmoney|  
|`Decimal`|money|  
|`DateTime`|smalldatetime|  
|`SQLDateTime`|smalldatetime|  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|
  `SqlGeography`, `SqlGeometry` 및 `SqlHierarchyId` 형식이 매핑 테이블에 추가되었습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 데이터 형식 SQL Server](sql-server-data-types-in-the-net-framework.md)  
  
  
