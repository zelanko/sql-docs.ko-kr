---
title: CLR 매개 변수 데이터 매핑 | 마이크로 소프트 문서
description: 이 문서에서는 Microsoft SQL Server 데이터 형식, SQL Server용 CLR의 등가물 및 .NET 프레임워크의 네이티브 CLR 등가물을 나열합니다.
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
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
ms.openlocfilehash: 360a94229b107e9f24bb2a769157c75cdeb3c143
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488471"
---
# <a name="mapping-clr-parameter-data"></a>CLR 매개 변수 데이터 매핑
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  다음 표에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **System.Data.SqlTypes** 네임스페이스에 대한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공통 언어 런타임(CLR)의 데이터 형식 및 .NET Framework의 기본 CLR 등가물 등이 나열됩니다.  
  
||||  
|-|-|-|  
|**SQL Server 데이터 형식**|System.Data.SqlTypes 또는 Microsoft.SqlServer.Types의 형식|**CLR 데이터 형식(.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, Nullable\<Int64>**|  
|**binary**|**SqlBytes, SqlBinary**|**바이트[]**|  
|**bit**|**SqlBoolean**|**Boolean, Nullable\<Boolean>**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDate시간**|**DateTime, Nullable\<DateTime>**|  
|**datetime**|**SqlDate시간**|**DateTime, Nullable\<DateTime>**|  
|**datetime2**|None|**DateTime, Nullable\<DateTime>**|  
|**Datetimeoffset**|**없음**|**DateTimeOffset, Nullable\<DateTimeOffset>**|  
|**decimal**|**Sqldecimal**|**소수점, null가능한\<소수점>**|  
|**float**|**SqlDouble**|**Double, Nullable\<Double>**|  
|**지리**|**SqlGeography**<br /><br /> **SqlGeography는** SQL Server와 함께 설치되고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩에서](https://www.microsoft.com/download/details.aspx?id=52676)다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의되어 있습니다.|None|  
|**형상**|**SqlGeometry**<br /><br /> **SqlGeometry는** SQL Server와 함께 설치되고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩에서](https://www.microsoft.com/download/details.aspx?id=52676)다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의되어 있습니다.|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId는** SQL Server와 함께 설치되고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩에서](https://www.microsoft.com/download/details.aspx?id=52676)다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의되어 있습니다.|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32, Nullable\<Int32>**|  
|**money**|**SQL머니**|**소수점, null가능한\<소수점>**|  
|**nchar**|**SqlChars, SqlString**|**문자열, Char[]**|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**소수점, null가능한\<소수점>**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars는** 데이터 전송 및 액세스에 더 적합하며 **SQLString은** 문자열 작업을 수행하는 데 더 적합합니다.|**문자열, Char[]**|  
|**nvarchar(1), nchar(1)**|**SqlChars, SqlString**|**Char, String, Char[], Nullable\<char>**|  
|**real**|**SqlSingle** **(SqlSingle의**범위는 **실제보다**큽니다.|**Single, Nullable\<Single>**|  
|**rowversion**|None|**바이트[]**|  
|**smallint**|**SqlInt16**|**Int16, Nullable\<Int16>**|  
|**smallmoney**|**SQL머니**|**소수점, null가능한\<소수점>**|  
|**sql_variant**|None|**Object**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**TimeSpan, Nullable\<TimeSpan>**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**Byte, Nullable\<Byte>**|  
|**uniqueidentifier**|**SqlGuid**|**Guid, Nullable\<Guid>**|  
|**사용자 정의 유형(UDT)**|None|동일한 어셈블리 또는 종속 어셈블리의 사용자 정의 형식에 바인딩된 동일한 클래스입니다.|  
|**varbinary**|**SqlBytes, SqlBinary**|**바이트[]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**byte, Byte[], Nullable\<byte>**|  
|**varchar**|None|None|  
|**xml**|**Sqlxml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Out 매개 변수로 자동 데이터 형식 변환  
 CLR 메서드는 입력 매개 변수가 **System.Data.SqlTypes** 네임스페이스의 CLR 데이터 형식인 경우 입력 매개 변수를 **out** 수정자(Microsoft Visual C#) 또는 ** \<Out(Out)>** 입력 매개 변수로 표시하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호출 코드 또는 프로그램에 정보를 반환할 수 있으며 호출 프로그램은 CLR 메서드가 데이터 형식을 반환할 때 해당 데이터 형식을 입력 매개 변수로 지정합니다.  
  
 예를 들어 다음 CLR 저장 프로시저에는 Out(C#) 또는 **out** ** \<Out()> ByRef(Visual** Basic)로 표시된 **SqlInt32** CLR 데이터 형식의 입력 매개 변수가 있습니다.  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 어셈블리를 데이터베이스에서 빌드하고 만든 후 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로시저는 다음 Transact-SQL을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만들어지며, 이 프로시저는 **int의** 데이터 형식을 OUTPUT 매개 변수로 지정합니다.  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 CLR 저장 프로시저를 호출하면 **SqlInt32** 데이터 형식이 자동으로 **int** 데이터 유형으로 변환되고 호출 프로그램으로 반환됩니다.  
  
 그러나 Out 매개 변수를 통해 모든 CLR 데이터 형식을 이에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환할 수는 없습니다. 다음 표에서는 이러한 예외를 보여 줍니다.  
  
|||  
|-|-|  
|**CLR 데이터 형식(SQL Server)**|**SQL Server 데이터 형식**|  
|**Decimal**|smallmoney|  
|**SQL머니**|smallmoney|  
|**Decimal**|money|  
|**DateTime**|smalldatetime|  
|**SQLDate시간**|smalldatetime|  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|매핑 테이블에 **SqlGeography,** **SqlGeometry**및 **SqlHierarchyId** 형식이 추가되었습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
