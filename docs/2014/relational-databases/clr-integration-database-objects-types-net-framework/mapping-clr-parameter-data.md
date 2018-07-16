---
title: CLR 매개 변수 데이터 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
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
caps.latest.revision: 69
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 34d30e57908e8cd44eefa43d6f2d030ae0d102f7
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37354525"
---
# <a name="mapping-clr-parameter-data"></a>CLR 매개 변수 데이터 매핑
  다음 표에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 CLR (공용 언어 런타임)에 있는 동등한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 `System.Data.SqlTypes` 네임 스페이스와 해당 기본 CLR에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
||||  
|-|-|-|  
|**SQL Server 데이터 형식**|System.Data.SqlTypes 또는 Microsoft.SqlServer.Types의 형식|**CLR 데이터 형식 (.NET Framework)**|  
|`bigint`|`SqlInt64`|**Int64, Nullable\<Int64>**|  
|`binary`|`SqlBytes, SqlBinary`|`Byte[]`|  
|`bit`|`SqlBoolean`|**Boolean, Nullable\<Boolean>**|  
|`char`|InclusionThresholdSetting|InclusionThresholdSetting|  
|`cursor`|InclusionThresholdSetting|InclusionThresholdSetting|  
|`date`|`SqlDateTime`|**DateTime, Nullable\<DateTime>**|  
|`datetime`|`SqlDateTime`|**DateTime, Nullable\<DateTime>**|  
|`datetime2`|InclusionThresholdSetting|**DateTime, Nullable\<DateTime>**|  
|`DATETIMEOFFSET`|`None`|**DateTimeOffset, Nullable\<DateTimeOffset>**|  
|`decimal`|`SqlDecimal`|**Decimal, Nullable\<10 진수 >**|  
|`float`|`SqlDouble`|**Double, Nullable\<Double>**|  
|`geography`|`SqlGeography`<br /><br /> `SqlGeography` SQL Server와 함께 설치 되 고에서 다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](http://go.microsoft.com/fwlink/?LinkId=131220)합니다.|InclusionThresholdSetting|  
|`geometry`|`SqlGeometry`<br /><br /> `SqlGeometry` SQL Server와 함께 설치 되 고에서 다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](http://go.microsoft.com/fwlink/?LinkId=131220)합니다.|InclusionThresholdSetting|  
|`hierarchyid`|`SqlHierarchyId`<br /><br /> `SqlHierarchyId` SQL Server와 함께 설치 되 고에서 다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](http://go.microsoft.com/fwlink/?LinkId=131220)합니다.|InclusionThresholdSetting|  
|`image`|InclusionThresholdSetting|InclusionThresholdSetting|  
|`int`|`SqlInt32`|**Int32, Nullable\<Int32>**|  
|`money`|`SqlMoney`|**Decimal, Nullable\<10 진수 >**|  
|`nchar`|`SqlChars, SqlString`|`String, Char[]`|  
|`ntext`|InclusionThresholdSetting|InclusionThresholdSetting|  
|`numeric`|`SqlDecimal`|**Decimal, Nullable\<10 진수 >**|  
|`nvarchar`|`SqlChars, SqlString`<br /><br /> `SQLChars`는 데이터 전송 및 액세스에 더 적합하고 `SQLString`은 문자열 작업에 더 적합합니다.|`String, Char[]`|  
|`nvarchar(1), nchar(1)`|`SqlChars, SqlString`|**Char, String, Char[], Nullable\<char>**|  
|`real`|`SqlSingle`(`SqlSingle` 범위, 단, `real`보다 큼)|**Single, Nullable\<Single>**|  
|`rowversion`|InclusionThresholdSetting|`Byte[]`|  
|`smallint`|`SqlInt16`|**Int16, Nullable\<Int16>**|  
|`smallmoney`|`SqlMoney`|**Decimal, Nullable\<10 진수 >**|  
|`sql_variant`|InclusionThresholdSetting|`Object`|  
|`table`|InclusionThresholdSetting|InclusionThresholdSetting|  
|`text`|InclusionThresholdSetting|InclusionThresholdSetting|  
|`time`|InclusionThresholdSetting|**TimeSpan, Nullable\<TimeSpan>**|  
|`timestamp`|InclusionThresholdSetting|InclusionThresholdSetting|  
|`tinyint`|`SqlByte`|**Byte, Nullable\<Byte>**|  
|`uniqueidentifier`|`SqlGuid`|**Guid, Nullable\<Guid>**|  
|`User-defined type(UDT)`|InclusionThresholdSetting|동일한 어셈블리 또는 종속 어셈블리의 사용자 정의 형식에 바인딩된 동일한 클래스입니다.|  
|**varbinary**|`SqlBytes, SqlBinary`|`Byte[]`|  
|`varbinary(1), binary(1)`|`SqlBytes, SqlBinary`|**byte, Byte[], Nullable\<byte>**|  
|`varchar`|InclusionThresholdSetting|InclusionThresholdSetting|  
|`xml`|`SqlXml`|InclusionThresholdSetting|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Out 매개 변수로 자동 데이터 형식 변환  
 CLR 메서드는 `out` 한정자(Microsoft Visual C#) 또는 `<Out()> ByRef`(Microsoft Visual Basic)로 입력 매개 변수를 표시하여 호출 코드나 프로그램에 정보를 반환할 수 있습니다. 입력 매개 변수가 `System.Data.SqlTypes` 네임스페이스의 CLR 데이터 형식이고 호출 프로그램이 이에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 입력 매개 변수로 지정할 경우 CLR 메서드가 데이터 형식을 반환하면 자동으로 형식 변환이 수행됩니다.  
  
 예를 들어 다음 CLR 저장 프로시저에는 `SqlInt32`(C#) 또는 `out`(Visual Basic)로 표시된 `<Out()> ByRef` CLR 데이터 형식의 입력 매개 변수가 있습니다.  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ … }  
```  
  
```vb  
<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
…  
End Sub  
```  
  
 어셈블리가 데이터베이스에서 만들어진 후에는 저장 프로시저가 `int`의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 OUTPUT 매개 변수로 지정하는 다음 Transact-SQL을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 만들어집니다.  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 CLR 저장 프로시저 호출되면 `SqlInt32` 데이터 형식이 자동으로 `int` 데이터 형식으로 변환되고 호출 프로그램에 반환됩니다.  
  
 그러나 Out 매개 변수를 통해 모든 CLR 데이터 형식을 이에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환할 수는 없습니다. 다음 표에서는 이러한 예외를 보여 줍니다.  
  
|||  
|-|-|  
|**CLR 데이터 형식 (SQL Server)**|**SQL Server 데이터 형식**|  
|`Decimal`|SMALLMONEY|  
|`SqlMoney`|SMALLMONEY|  
|`Decimal`|money|  
|`DateTime`|smalldatetime|  
|`SQLDateTime`|smalldatetime|  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|`SqlGeography`, `SqlGeometry` 및 `SqlHierarchyId` 형식이 매핑 테이블에 추가되었습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [.NET Framework의 SQL Server 데이터 형식](sql-server-data-types-in-the-net-framework.md)  
  
  
