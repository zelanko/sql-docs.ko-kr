---
title: CLR 매개 변수 데이터 매핑 | Microsoft Docs
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
ms.openlocfilehash: 530db4d31d3db4773713816f1b68404990997512
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081308"
---
# <a name="mapping-clr-parameter-data"></a>CLR 매개 변수 데이터 매핑
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  다음 표에서는 데이터 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식, **SqlTypes** 네임 스페이스의에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR (공용 언어 런타임)의 해당 데이터 형식 및 .NET Framework의 해당 네이티브 clr에 해당 하는 데이터 형식을 보여 줍니다.  
  
||||  
|-|-|-|  
|**SQL Server 데이터 형식**|System.Data.SqlTypes 또는 Microsoft.SqlServer.Types의 형식|**CLR 데이터 형식(.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, Nullable\<int64>**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte []**|  
|**bit**|**SqlBoolean**|**부울, Nullable\<부울>**|  
|**char**|None|None|  
|**위치**|None|None|  
|**date**|**SqlDateTime**|**DateTime, Nullable\<datetime>**|  
|**datetime**|**SqlDateTime**|**DateTime, Nullable\<datetime>**|  
|**datetime2**|None|**DateTime, Nullable\<datetime>**|  
|**DATETIMEOFFSET**|**없음을**|**DateTimeOffset, Nullable\<DateTimeOffset>**|  
|**진수가**|**SqlDecimal**|**Decimal, Nullable\<decimal>**|  
|**float**|**SqlDouble**|**Double, Nullable\<double>**|  
|**geography**|**SqlGeography**<br /><br /> **Sqlgeography** 는 SQL Server와 함께 설치 되 고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=52676)에서 다운로드할 수 있는 Microsoft. s s t. d l l. l d. .dll에 정의 되어 있습니다.|None|  
|**geometry**|**SqlGeometry**<br /><br /> **Sqlgeometry** 는 SQL Server와 함께 설치 되 고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=52676)에서 다운로드할 수 있는 Microsoft. s t a. t a r .dll에 정의 되어 있습니다.|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **Sqlhierarchyid** 는 SQL Server와 함께 설치 되 고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=52676)에서 다운로드할 수 있는 Microsoft. s s t. t a r l i d. .dll에 정의 되어 있습니다.|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32, Nullable\<int32>**|  
|**money**|**SqlMoney**|**Decimal, Nullable\<decimal>**|  
|**nchar**|**SqlChars, SqlString**|**String, Char[]**|  
|**ntext**|None|None|  
|**번호**|**SqlDecimal**|**Decimal, Nullable\<decimal>**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **Sqlchars** 는 데이터 전송 및 액세스와 더 잘 일치 하 고 **SQLString** 는 문자열 작업을 수행 하는 데 더 적합 합니다.|**String, Char[]**|  
|**nvarchar (1), nchar (1)**|**SqlChars, SqlString**|**Char, String, Char [], Nullable\<문자>**|  
|**실제로**|**Sqlsingle** ( **sqlsingle**의 범위 이지만 **실제**보다 큼)|**단일 Nullable\<단일>**|  
|**rowversion**|None|**Byte []**|  
|**smallint**|**SqlInt16**|**Int16, Nullable\<int16>**|  
|**smallmoney**|**SqlMoney**|**Decimal, Nullable\<decimal>**|  
|**sql_variant**|None|**Object**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**TimeSpan, Nullable\<timespan>**|  
|**없으면**|None|None|  
|**tinyint**|**SqlByte**|**바이트, Nullable\<바이트>**|  
|**uniqueidentifier**|**SqlGuid**|**Guid, Nullable\<guid>**|  
|**UDT (사용자 정의 형식)**|None|동일한 어셈블리 또는 종속 어셈블리의 사용자 정의 형식에 바인딩된 동일한 클래스입니다.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte []**|  
|**varbinary (1), binary (1)**|**SqlBytes, SqlBinary**|**byte, Byte [], Nullable\<바이트>**|  
|**varchar**|None|None|  
|**xml**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Out 매개 변수로 자동 데이터 형식 변환  
 Clr 메서드는 입력 매개 변수가 시스템의 clr 데이터 형식이 면 **out** 한정자 (microsoft Visual c #) 또는 ** \<out () > ByRef** (microsoft Visual Basic)를 사용 하 여 입력 매개 변수를 표시 하 여 호출 코드 또는 프로그램에 정보를 반환할 수 있습니다 **. SqlTypes** 네임 스페이스 및 호출 프로그램은 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 입력 매개 변수로 지정 합니다. CLR 메서드에서 데이터 형식을 반환 하면 형식 변환이 자동으로 수행 됩니다.  
  
 예를 들어 다음 clr 저장 프로시저에는 **out** (c #) 또는 ** \<out () > ByRef** (Visual Basic)로 표시 된 **SqlInt32** CLR 데이터 형식의 입력 매개 변수가 있습니다.  
  
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
  
 데이터베이스에서 어셈블리를 작성 하 고 만든 후에는 다음 Transact-sql을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 저장 프로시저를 만들고이를 출력 매개 변수로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int** 의 데이터 형식을 지정 합니다.  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 CLR 저장 프로시저가 호출 되 면 **SqlInt32** 데이터 형식이 자동으로 **int** 데이터 형식으로 변환 되 고 호출 프로그램으로 반환 됩니다.  
  
 그러나 Out 매개 변수를 통해 모든 CLR 데이터 형식을 이에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환할 수는 없습니다. 다음 표에서는 이러한 예외를 보여 줍니다.  
  
|||  
|-|-|  
|**CLR 데이터 형식(SQL Server)**|**SQL Server 데이터 형식**|  
|**Decimal**|smallmoney|  
|**SqlMoney**|smallmoney|  
|**Decimal**|money|  
|**날짜**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|**Sqlgeography**, **Sqlgeography**및 **sqlgeography** 유형을 매핑 테이블에 추가 했습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
