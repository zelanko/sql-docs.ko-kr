---
title: 날짜 및 시간 데이터
description: SQL Server 2008에서 도입된 새 날짜 및 시간 데이터 형식을 사용하는 방법을 설명합니다.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 43a7f03a4e8a9a3c67a3263f792f2f921eef7a78
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928852"
---
# <a name="date-and-time-data"></a>날짜 및 시간 데이터

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 2008에는 날짜 및 시간 정보를 처리하기 위한 새로운 데이터 형식이 도입되었습니다. 새 데이터 형식에는 날짜 및 시간에 대한 별도의 형식, 그리고 더 큰 범위, 전체 자릿수 및 표준 시간대 인식이 포함된 확장된 데이터 형식이 포함됩니다. Microsoft SqlClient Data Provider for SQL Server(<xref:Microsoft.Data.SqlClient>)는 SQL Server 2008 데이터베이스 엔진의 새로운 기능을 모두 완벽하게 지원합니다. SqlClient에서 이러한 새로운 기능을 사용하려면 .NET Framework 3.5 SP1(이상) 또는 .NET Core 1.0(이상) 버전을 설치해야 합니다.  
  
SQL Server 2008보다 이전의 SQL Server 버전에는 날짜 및 시간 값을 사용하기 위한 두 가지 데이터 형식 `datetime` 및 `smalldatetime`이 있습니다. 두 데이터 형식 모두 날짜 값과 시간 값을 모두 포함하므로 날짜나 시간 값만 가지고 작업하기는 어려웠습니다. 또한 이러한 날짜 형식은 1753년 영국에 양력이 도입된 이후의 날짜만 지원합니다. 또 다른 제한 사항은 이러한 이전 데이터 형식이 표준 시간대를 인식하지 못해 여러 표준 시간대에서 발생하는 데이터로 작업하기가 어렵다는 것입니다.  
  
SQL Server 온라인 설명서에서 SQL Server 데이터 형식에 대한 전체 설명을 찾을 수 있습니다. 날짜 및 시간 데이터에 대한 초급 수준 설명은 [날짜 및 시간 데이터 사용](https://go.microsoft.com/fwlink/?LinkID=98361)을 참조하세요.
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>SQL Server 2008에 날짜/시간 데이터 형식이 도입됨  
 다음 표에서는 새로운 날짜 및 시간 데이터 형식에 대해 설명합니다.  
  
|SQL Server 데이터 형식|Description|  
|--------------------------|-----------------|  
|`date`|`date` 데이터 형식은 하루 단위이며 범위는 01년 1월 1일부터 9999년 12월 31일까지입니다. 기본값은 1900년 1월 1일입니다. 스토리지 크기는 3바이트입니다.|  
|`time`|`time` 데이터 형식은 24시간제를 기준으로 시간 값만 저장합니다. `time` 데이터 형식의 범위는 00:00:00.0000000~23:59:59.9999999이며 정확도는 100나노초입니다. 기본값은 00:00:00.0000000(자정)입니다. `time` 데이터 형식은 소수 자릿수 초 전체 자릿수에 대한 사용자 정의를 지원하며 저장 크기는 지정된 전체 자릿수에 따라 3~6바이트를 사용합니다.|  
|`datetime2`|`datetime2` 데이터 형식은 `date` 및 `time` 데이터 형식의 범위와 전체 자릿수를 단일 데이터 형식으로 결합합니다.<br /><br /> 기본값과 문자열 리터럴 형식은 `date` 및 `time` 데이터 형식에 정의된 값과 동일합니다.|  
|`datetimeoffset`|`datetimeoffset` 데이터 형식은 `datetime2`의 모든 기능을 포함하며 추가로 표준 시간대 오프셋 기능을 지원합니다. 표준 시간대 오프셋은 [+&#124;-] HH:MM으로 표현됩니다. HH는 00에서 14 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 시간(시간)을 나타냅니다. MM은 00에서 59 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 추가 시간(분)을 나타냅니다. 이 시간 형식은 100나노초까지 지원합니다. 필수 + 또는 - 부호는 현지 시간을 얻기 위해 표준 시간대 오프셋을 UTC(협정 세계시 또는 그리니치 표준시)에서 추가하거나 뺄 것인지를 나타냅니다.|  
  
> [!NOTE]
>  `Type System Version` 키워드 사용에 관한 자세한 내용은 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>을 참조하세요.  
  
## <a name="date-format-and-date-order"></a>날짜 형식 및 날짜 순서  
SQL Server가 날짜 및 시간 값을 구문 분석하는 방법은 형식 시스템 버전 및 서버 버전뿐만 아니라 서버의 기본 언어 및 형식 설정에 따라서도 달라집니다. 다른 언어 및 날짜 형식 설정을 사용하는 연결에 의해 쿼리가 실행되는 경우 한 언어의 날짜 형식에 대해 작동하는 날짜 문자열이 인식되지 않을 수 있습니다.  
  
Transact-SQL SET LANGUAGE 문은 날짜 부분의 순서를 결정하는 DATEFORMAT를 묵시적으로 설정합니다. 연결에서 SET DATEFORMAT Transact-SQL 문을 사용하여 MDY, DMY, YMD, YDM, MYD 또는 DYM 순서의 날짜 부분을 정렬하여 날짜 값을 명확히 구분할 수 있습니다.  
  
연결에 대해 DATEFORMAT을 지정하지 않으면 SQL Server는 연결과 연결된 기본 언어를 사용합니다. 예를 들어 날짜 문자열 '01/02/03'은 언어 설정이 미국 영어인 서버에서는 MDY(2003년 1월 2일)로 해석되고 언어 설정이 영국 영어인 서버에서는 DMY(2003년 2월 1일)로 해석됩니다. 연도는 세기 값을 할당하는 구분 날짜를 정의하는 SQL Server의 구분 연도 규칙을 사용하여 결정됩니다. 자세한 내용은 SQL Server 온라인 설명서의 [two digit year cutoff](https://go.microsoft.com/fwlink/?LinkId=120473) 옵션을 참조하세요.  
  
> [!NOTE]
>  문자열 형식에서 `date`, `time`, `datetime2` 또는 `datetimeoffset`로 변환할 때는 YDM 날짜 형식이 지원되지 않습니다.  
  
SQL Server에서 날짜 및 시간 데이터를 해석하는 방법은 SQL Server 2008 온라인 설명서의 [날짜 및 시간 데이터 사용](https://go.microsoft.com/fwlink/?LinkID=98361)을 참조하세요.  
  
## <a name="datetime-data-types-and-parameters"></a>날짜/시간 데이터 형식 및 매개 변수  
새 날짜 및 시간 데이터 형식을 지원하기 위해 <xref:System.Data.SqlDbType>에 다음 열거형이 추가되었습니다.  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

앞의 <xref:Microsoft.Data.SqlClient.SqlParameter> 열거형 중 하나를 사용하여 <xref:System.Data.SqlDbType>의 데이터 형식을 지정할 수 있습니다. 

> [!NOTE]
> `DbType`의 `SqlParameter` 속성을 `SqlDbType.Date`로 설정할 수 없습니다.

또한, <xref:Microsoft.Data.SqlClient.SqlParameter> 개체의 <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> 속성을 특정 `SqlParameter` 열거형 값으로 설정하면 일반적인 방식으로 <xref:System.Data.DbType>의 형식을 지정할 수 있습니다. <xref:System.Data.DbType> 및 `datetime2` 데이터 형식을 지원하기 위해 다음 열거형 값이 `datetimeoffset`에 추가되었습니다.  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
이들 새 열거형은 `Date`, `Time` 및 `DateTime` 열거형을 보완합니다.  
  
매개 변수 개체의 Microsoft SqlClient Data Provider 형식은 매개 변수 개체 값의 .NET 형식에서 또는 매개 변수 개체의 `DbType`에서 유추됩니다. 새 날짜 및 시간 데이터 형식을 지원하기 위해 도입된 새로운 <xref:System.Data.SqlTypes> 데이터 형식은 없습니다. 다음 표에서는 SQL Server 2008 날짜 및 시간 데이터 형식과 CLR 데이터 형식 간의 매핑에 대해 설명합니다.  
  
|SQL Server 데이터 형식|.NET 형식|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|date|System.DateTime|Date|Date|  
|time|System.TimeSpan|Time|Time|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|Datetime|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>SqlParameter 속성  
 다음 표에서는 날짜 및 시간 데이터 형식과 관련된 `SqlParameter` 속성을 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|값이 null을 허용하는지 여부를 가져오거나 설정합니다. Null 매개 변수 값을 서버에 보낼 때 <xref:System.DBNull>(Visual Basic에서는 `null`) 대신 `Nothing`을 지정해야 합니다. 데이터베이스 null에 대한 자세한 내용은 [null 값 처리](handle-null-values.md)를 참조하세요.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|값을 나타내는 데 사용되는 최대 자릿수를 가져오거나 설정합니다. 날짜 및 시간 데이터 형식에 대해서는 이 설정이 무시됩니다.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|`Time`, `DateTime2`, 및 `DateTimeOffset`의 날짜 부분 값이 확인되는 소수 자릿수를 가져오거나 설정합니다. 기본값은 0이며,이 값은 실제 소수 자릿수가 값에서 유추되고 서버로 전송됨을 의미합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|날짜 및 시간 데이터 형식에 대해서는 무시됩니다.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|매개 변수 값을 가져오거나 설정합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|매개 변수 값을 가져오거나 설정합니다.|  
  
> [!NOTE]
>  0보다 작거나 24시간보다 크거나 같은 시간 값은 <xref:System.ArgumentException>을 throw합니다.  
  
### <a name="creating-parameters"></a>매개 변수 만들기  
<xref:Microsoft.Data.SqlClient.SqlParameter> 개체는 해당 생성자를 사용하여 만들거나 <xref:Microsoft.Data.SqlClient.SqlCommand>.<xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> 컬렉션에 추가하여 만들 수 있습니다(`Add`의 <xref:Microsoft.Data.SqlClient.SqlParameterCollection> 메서드를 호출). `Add` 메서드는 생성자 인수 또는 기존 매개 변수 개체를 입력으로 사용합니다.  
  
이 항목의 다음 섹션에서는 날짜 및 시간 매개 변수를 지정하는 방법에 대한 예제를 제공합니다.
  
### <a name="date-example"></a>날짜 예제  
다음 코드 조각에서는 `date` 매개 변수를 지정하는 방법을 보여 줍니다.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>시간 예제  
다음 코드 조각에서는 `time` 매개 변수를 지정하는 방법을 보여 줍니다.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Datetime2 예제  
다음 코드 조각에서는 날짜 및 시간 부분을 모두 사용하여 `datetime2` 매개 변수를 지정하는 방법을 보여 줍니다.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>DateTimeOffSet 예제  
다음 코드 조각에서는 날짜, 시간 및 표준 시간대 오프셋이 0인 `DateTimeOffSet` 매개 변수를 지정하는 방법을 보여 줍니다.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
다음 코드 조각과 같이 `AddWithValue`의 <xref:Microsoft.Data.SqlClient.SqlCommand> 메서드를 사용하여 매개 변수를 제공할 수도 있습니다. 그러나 `AddWithValue` 메서드에서는 매개 변수에 <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> 또는 <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A>를 지정할 수 없습니다.  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
`@date` 매개 변수는 서버의 `date`, `datetime` 또는 `datetime2` 데이터 형식에 매핑될 수 있습니다. 새 `datetime` 데이터 형식으로 작업하는 경우 매개 변수의 <xref:System.Data.SqlDbType> 속성을 명시적으로 인스턴스의 데이터 형식으로 설정해야 합니다. <xref:System.Data.SqlDbType.Variant>를 사용하거나 매개 변수 값을 암시적으로 제공하면 `datetime` 및 `smalldatetime` 데이터 형식에 이전 버전 호환성 문제가 발생할 수 있습니다.  
  
다음 표에서는 CLR 형식에서 유추되는 `SqlDbTypes`를 보여 줍니다.  
  
|CLR 유형|유추된 SqlDbType|  
|--------------|------------------------|  
|DateTime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>날짜 및 시간 데이터 검색  
다음 표에서는 SQL Server 2008 날짜 및 시간 값을 검색하는 데 사용되는 메서드에 대해 설명합니다.  
  
|SqlClient 메서드|Description|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|지정된 열 값을 <xref:System.DateTime> 구조체로 검색합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|지정된 열 값을 <xref:System.DateTimeOffset> 구조체로 검색합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|필드에 대해 기본 공급자별 형식인 형식을 반환합니다. 새 날짜 및 시간 형식에 대해 `GetFieldType`과 동일한 형식을 반환합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|지정한 열의 값을 검색합니다. 새 날짜 및 시간 형식에 대해 `GetValue`와 동일한 형식을 반환합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|지정된 배열의 값을 검색합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|열 값을 <xref:System.Data.SqlTypes.SqlString>으로 검색합니다. 데이터를 <xref:System.InvalidCastException>으로 표현할 수 없는 경우 `SqlString`이 발생합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|열 데이터를 기본 `SqlDbType`으로 검색합니다. 새 날짜 및 시간 형식에 대해 `GetValue`와 동일한 형식을 반환합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|지정된 배열의 값을 검색합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|Type System Version이 SQL Server 2005로 설정되어 있는 경우 열 값을 문자열로 검색합니다. 데이터를 문자열로 표현할 수 없는 경우 <xref:System.InvalidCastException>이 발생합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|지정된 열 값을 <xref:System.TimeSpan> 구조체로 검색합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|지정된 열 값을 기본 CLR 형식으로 검색합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|배열에서 열 값을 검색합니다.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|결과 집합의 메타데이터를 설명하는 <xref:System.Data.DataTable>을 반환합니다.|  
  
> [!NOTE]
>  SQL Server에서 in-process로 실행되는 코드에는 새로운 날짜 및 시간 `SqlDbTypes`이 지원되지 않습니다. 이러한 형식 중 하나가 서버에 전달되면 예외가 발생합니다.  
  
## <a name="specifying-date-and-time-values-as-literals"></a>날짜 및 시간 값을 리터럴로 지정  
날짜 및 시간 데이터 형식은 다양한 리터럴 문자열 형식을 사용하여 지정할 수 있으며, 그러면 SQL Server가 런타임에 해당 형식을 평가하여 내부 날짜/시간 구조체로 변환합니다. SQL Server는 작은따옴표(')로 묶인 날짜 및 시간 데이터를 인식합니다. 다음은 일부 형식의 예입니다.  
  
- `'October 15, 2006'`과 같은 영문자 날짜 형식.  
  
- `'10/15/2006'`과 같은 숫자 날짜 형식.  
  
- `'20061015'`와 같은 구분되지 않은 문자열 형식(ISO 표준 날짜 형식을 사용하는 경우 2006년 10월 15일로 해석됨).  
  
> [!NOTE]
>  SQL Server 온라인 설명서에서 날짜 및 시간 데이터 형식의 모든 리터럴 문자열 형식 및 기타 기능에 대한 전체 설명을 찾을 수 있습니다.  
  
0보다 작거나 24시간보다 크거나 같은 시간 값은 <xref:System.ArgumentException>을 throw합니다.  
  
## <a name="resources-in-sql-server-2008-books-online"></a>SQL Server 2008 온라인 설명서 내 리소스  
SQL Server 2008에서 날짜 및 시간 값을 사용하는 방법에 대한 자세한 내용은 SQL Server 2008 온라인 설명서에서 다음 리소스를 참조하세요.  
  
|항목|Description|  
|-----------|-----------------|  
|[날짜 및 시간 데이터 형식 및 함수(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98360)|모든 Transact-SQL 날짜 및 시간 데이터 형식 및 함수에 대한 개요를 제공합니다.|  
|[날짜 및 시간 데이터 사용](https://go.microsoft.com/fwlink/?LinkId=98361)|날짜 및 시간 데이터 형식 및 함수에 관한 정보와 사용 예제를 제공합니다.|  
|[데이터 형식(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98362)|SQL Server 2008의 시스템 데이터 형식에 대해 설명합니다.|  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 데이터 형식 및 ADO.NET](sql-server-data-types.md)
