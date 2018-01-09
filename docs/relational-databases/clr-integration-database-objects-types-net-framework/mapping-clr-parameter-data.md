---
title: "CLR 매개 변수 데이터 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "71"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3592a4c547b3586df4be45b2e1734e330dd16664
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="mapping-clr-parameter-data"></a>CLR 매개 변수 데이터 매핑
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]다음 표에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대 한 공용 언어 런타임 (CLR)에서 동등 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 **System.Data.SqlTypes** 네임 스페이스 및 해당 네이티브 CLR 형식에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET framework입니다.  
  
||||  
|-|-|-|  
|**SQL Server 데이터 형식**|System.Data.SqlTypes 또는 Microsoft.SqlServer.Types의 형식|**CLR 데이터 형식 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, null 허용\<Int64 >**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte]**|  
|**bit**|**SqlBoolean**|**부울, null은 허용\<부울 >**|  
|**char**|InclusionThresholdSetting|InclusionThresholdSetting|  
|**cursor**|InclusionThresholdSetting|InclusionThresholdSetting|  
|**date**|**SqlDateTime**|**DateTime, null 허용\<날짜/시간 >**|  
|**datetime**|**SqlDateTime**|**DateTime, null 허용\<날짜/시간 >**|  
|**datetime2**|InclusionThresholdSetting|**DateTime, null 허용\<날짜/시간 >**|  
|**DATETIMEOFFSET**|**없음**|**DateTimeOffset의 경우 null을 허용\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**10 진수, null은 허용\<10 진수 >**|  
|**float**|**SqlDouble**|**Double, null은 허용\<Double >**|  
|**geography**|**SqlGeography**<br /><br /> **SqlGeography** SQL Server와 함께 설치 되어 있고에서 다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=52676)합니다.|InclusionThresholdSetting|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry** SQL Server와 함께 설치 되어 있고에서 다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=52676)합니다.|InclusionThresholdSetting|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** SQL Server와 함께 설치 되어 있고에서 다운로드할 수 있는 Microsoft.SqlServer.Types.dll에 정의 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [기능 팩](https://www.microsoft.com/download/details.aspx?id=52676)합니다.|InclusionThresholdSetting|  
|**image**|InclusionThresholdSetting|InclusionThresholdSetting|  
|**int**|**SqlInt32**|**Int32, null 허용\<i n t 32 >**|  
|**money**|**SqlMoney**|**10 진수, null은 허용\<10 진수 >**|  
|**nchar**|**SqlChars, SqlString**|**String, Char**|  
|**ntext**|InclusionThresholdSetting|InclusionThresholdSetting|  
|**numeric**|**SqlDecimal**|**10 진수, null은 허용\<10 진수 >**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** 데이터 전송 및 액세스에 대 한 더 일치 되 고 **SQLString** 더 적합 한 문자열 작업 수행에 대 한 합니다.|**String, Char**|  
|**nvarchar(1), nchar(1)**|**SqlChars, SqlString**|**Char, String, Char, Nullable\<char >**|  
|**real**|**그러나 SqlSingle** (범위 **SqlSingle**, 보다 크면 **실제**)|**단일, null은 허용\<단일 >**|  
|**rowversion**|InclusionThresholdSetting|**Byte]**|  
|**smallint**|**SqlInt16**|**Int16, null 허용\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**10 진수, null은 허용\<10 진수 >**|  
|**sql_variant**|InclusionThresholdSetting|**개체**|  
|**table**|InclusionThresholdSetting|InclusionThresholdSetting|  
|**text**|InclusionThresholdSetting|InclusionThresholdSetting|  
|**time**|InclusionThresholdSetting|**Null 허용 TimeSpan\<TimeSpan >**|  
|**timestamp**|InclusionThresholdSetting|InclusionThresholdSetting|  
|**tinyint**|**SqlByte**|**Byte, null 허용\<바이트 >**|  
|**uniqueidentifier**|**SqlGuid**|**Guid, null 허용\<Guid >**|  
|**사용자 정의 type(UDT)**|InclusionThresholdSetting|동일한 어셈블리 또는 종속 어셈블리의 사용자 정의 형식에 바인딩된 동일한 클래스입니다.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**바이트, Byte, Nullable\<바이트 >**|  
|**varchar**|InclusionThresholdSetting|InclusionThresholdSetting|  
|**xml**|**SqlXml**|InclusionThresholdSetting|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Out 매개 변수로 자동 데이터 형식 변환  
 CLR 메서드는 입력된 매개 변수를 표시 하 여 호출 코드나 프로그램 정보를 반환할 수는 **아웃** 한정자 (Microsoft Visual C#) 또는  **\<out () > ByRef** (Microsoft Visual Basic) 입력된 매개 변수는 CLR 데이터 형식에는 **System.Data.SqlTypes** 네임 스페이스에 속하고 호출 프로그램에 해당 하는 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식 변환이 자동으로 발생 입력된 매개 변수 데이터 형식 CLR 메서드가 데이터 형식을 반환 합니다.  
  
 예를 들어 다음 CLR 저장 프로시저에 대 한 입력된 매개 변수 **SqlInt32** CLR 데이터 형식으로 표시 된 **아웃** (C#) 또는  **\<out () > ByRef** 드 ( Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ … }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
…  
End Sub  
```  
  
 저장된 프로시저가 생성 된 어셈블리를 작성 하는 데이터베이스에서 만든 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정 하는 다음 Transact SQL로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 데이터 형식이 **int** 출력 매개 변수로:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 CLR 저장 프로시저를 호출 하는 **SqlInt32** 데이터 형식을 자동으로 변환 됩니다는 **int** 데이터 형식이 고 호출 프로그램에 반환 합니다.  
  
 그러나 Out 매개 변수를 통해 모든 CLR 데이터 형식을 이에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환할 수는 없습니다. 다음 표에서는 이러한 예외를 보여 줍니다.  
  
|||  
|-|-|  
|**CLR 데이터 형식 (SQL Server)**|**SQL Server 데이터 형식**|  
|**10 진수**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**10 진수**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|추가 **SqlGeography**, **SqlGeometry**, 및 **SqlHierarchyId** 매핑 테이블에는 형식입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
