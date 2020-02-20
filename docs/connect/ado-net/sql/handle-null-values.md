---
title: NULL 값 처리
description: SQL Server 및 .NET에서 GUID 및 uniqueidentifier 값을 사용하는 방법을 보여 줍니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 861ed4395e6cf8f5e8df3a5cc41a0f6da597e5ad
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247747"
---
# <a name="handling-null-values"></a>NULL 값 처리

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

관계형 데이터베이스에서 null 값은 열 값을 알 수 없거나 값이 누락된 경우에 사용됩니다. Null은 빈 문자열(문자 또는 날짜/시간 데이터 형식의 경우)도 아니고 0 값(숫자 데이터 형식의 경우)도 아닙니다. ANSI SQL-92 사양에서는 모든 null이 일관되게 처리되도록 null이 모든 데이터 형식에 대해 동일해야 함을 명시합니다. <xref:System.Data.SqlTypes> 네임스페이스는 <xref:System.Data.SqlTypes.INullable> 인터페이스를 구현하여 null 의미 체계를 제공합니다. <xref:System.Data.SqlTypes>의 각 데이터 형식에는 해당 데이터 형식의 인스턴스에 할당할 수 있는 고유한 `IsNull` 속성과 `Null` 값이 있습니다.  
  
> [!NOTE]
>  .NET Framework 버전 2.0 및 .NET Core 버전 1.0에는 nullable 형식에 대한 지원이 도입되었습니다. 이를 통해 프로그래머는 값 형식을 확장하여 기본 형식의 모든 값을 나타낼 수 있습니다. 이러한 CLR nullable 형식은 <xref:System.Nullable> 구조체의 인스턴스를 나타냅니다. 이 기능은 값 형식이 boxed 및 unboxed인 경우에 특히 유용하며 개체 유형과의 호환성을 향상시킵니다. ANSI SQL null은 `null` 참조(또는 Visual Basic의 `Nothing`)와 동일한 방식으로 동작하지 않으므로 CLR nullable 형식은 데이터베이스 null을 저장하는 데 적합하지 않습니다. 데이터베이스 ANSI SQL null 값에 대한 작업을 수행하려면 <xref:System.Nullable> 대신 <xref:System.Data.SqlTypes> null을 사용합니다. C#에서 CLR nullable 형식으로 작업하는 방법에 대한 자세한 내용은 [Nullable 형식](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/)을 참조하고, C#의 경우 [Nullable 형식 사용](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/)을 참조하세요.  
  
## <a name="nulls-and-three-valued-logic"></a>Null 및 3치 논리  
열 정의에 null 값을 허용하면 애플리케이션에 값이 3치 논리가 도입됩니다. 비교는 다음 세 가지 조건 중 하나로 평가될 수 있습니다.  
  
- True  
  
- False  
  
- 알 수 없음  
  
Null은 unknown으로 간주되기 때문에 서로 비교되는 두 null 값은 동일한 것으로 간주되지 않습니다. 산술 연산자를 사용하는 식에서 피연산자 중 하나라도 null이면 결과도 null입니다.  
  
## <a name="nulls-and-sqlboolean"></a>Null 및 SqlBoolean  
<xref:System.Data.SqlTypes> 간 비교는 <xref:System.Data.SqlTypes.SqlBoolean>을 반환합니다. 각 `SqlType`에 대한 `IsNull` 함수는 <xref:System.Data.SqlTypes.SqlBoolean>을 반환하며 null 값을 확인하는 데 사용할 수 있습니다. 다음 진리표에서는 null 값이 있는 경우 AND, OR 및 NOT 연산자가 작동하는 방식을 보여 줍니다. (T=true, F=false, U=unknown 또는 null)  
  
![진리표](../media/truthtable-bpuedev11.gif "TruthTable_bpuedev11")  
  
### <a name="understanding-the-ansi_nulls-option"></a>ANSI_NULLS 옵션 이해  
<xref:System.Data.SqlTypes>는 SQL Server에서 ANSI_NULLS 옵션이 on으로 설정된 경우와 동일한 의미 체계를 제공합니다. 모든 산술 연산자(+, -, *, /, %), 비트 단위 연산자(~, &, &#124;) 및 대부분의 함수는 피연산자 또는 인수 중 하나가 null이면 null을 반환합니다. 단, `IsNull` 속성의 경우는 제외됩니다.  
  
ANSI SQL-92 표준에서는 WHERE 절에서 *columnName* = NULL을 지원하지 않습니다. SQL Server에서 ANSI_NULLS 옵션은 데이터베이스의 기본 null 허용 여부와 null 값에 대한 비교 평가를 모두 제어합니다. ANSI_NULLS이 설정된 경우(기본값) null 값을 테스트할 때 식에서 IS NULL 연산자를 사용해야 합니다. 예를 들어 ANSI_NULLS가 on이면 다음 비교 결과는 항상 unknown이 됩니다.  
  
```console
colname > NULL  
```  
  
Null 값을 포함하는 변수와 비교하면 unknown도 생성됩니다.  
  
```console
colname > @MyVariable  
```  
  
IS NULL 또는 IS NOT NULL 조건자를 사용하여 null 값을 테스트하세요. 그렇게 하면 WHERE 절이 복잡해질 수 있습니다. 예를 들어 AdventureWorks Customer 테이블의 TerritoryID 열은 null 값을 허용합니다. SELECT 문이 다른 값 이외에 Null 값을 테스트하는 경우 IS NULL 조건자가 포함되어야 합니다.  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
SQL Server에서 ANSI_NULLS를 off로 설정한 경우 같음 연산자를 사용하여 null과 비교하는 식을 만들 수 있습니다. 그러나 다른 연결이 해당 연결에 null 옵션을 설정하는 것을 방지할 수 없습니다. 연결에 대한 ANSI_NULLS 설정에 관계없이 null 값을 테스트하기 위해 IS NULL을 사용하는 것은 항상 작동합니다.  
  
<xref:System.Data.SqlTypes>에서 null 값을 처리하기 위해 항상 ANSI SQL-92 표준을 따르는 `DataSet`에서는 ANSI_NULLS를 off로 설정할 수 없습니다.  
  
## <a name="assigning-null-values"></a>Null 값 할당  
Null 값은 특수하며, 저장 및 할당 의미 체계가 다양한 형식 시스템 및 스토리지 시스템에서 서로 다릅니다. `Dataset`는 다양한 형식 및 스토리지 시스템에서 사용하도록 설계되었습니다.  
  
이 섹션에서는 다양한 형식 시스템에서 <xref:System.Data.DataRow>의 <xref:System.Data.DataColumn>에 null 값을 할당하기 위한 null 의미 체계에 대해 설명합니다.  
  
`DBNull.Value`  
이 할당은 모든 형식의 `DataColumn`에 유효합니다. 형식이 `INullable`를 구현하는 경우 `DBNull.Value`는 적절한 강력한 형식의 Null 값으로 강제 변환됩니다.  
  
`SqlType.Null`  
모든 <xref:System.Data.SqlTypes> 데이터 형식에서 `INullable`을 구현합니다. 암시적 캐스트 연산자를 사용하여 강력한 형식의 null 값을 열의 데이터 형식으로 변환할 수 있는 경우 할당이 통과합니다. 그렇지 않으면 잘못된 캐스트 예외가 throw됩니다.  
  
`null`  
'Null'이 지정된 `DataColumn` 데이터 형식에 올바른 값이면 `INullable` 형식(`SqlType.Null`)과 연결된 적절한 `DbNull.Value` 또는 `Null`으로 강제 변환됩니다.  
  
`derivedUdt.Null`  
UDT 열의 경우 null은 항상 `DataColumn`과 연결된 형식에 따라 저장됩니다. `DataColumn`과 연결된 UDT가 `INullable`를 구현하지 않지만 하위 클래스는 구현하는 경우를 생각해 보겠습니다. 이 경우 파생 클래스와 연결된 강력한 형식의 null 값이 할당되면 해당 값은 형식화되지 않은 `DbNull.Value`로 저장됩니다. Null 저장소는 항상 DataColumn의 데이터 형식과 일치하기 때문입니다.  
  
> [!NOTE]
>  `Nullable<T>` 또는 <xref:System.Nullable> 구조체는 현재 `DataSet`에서 지원되지 않습니다.  
  
### <a name="multiple-column-row-assignment"></a>여러 열(행) 할당  
`DataTable.Add`, `DataTable.LoadDataRow`또는 행에 매핑되는 <xref:System.Data.DataRow.ItemArray%2A>를 수락하는 다른 API는 'null'을 DataColumn의 기본값에 매핑합니다. 배열의 개체에 `DbNull.Value` 또는 강력한 형식의 상응하는 값이 포함된 경우 위에 설명한 것과 동일한 규칙이 적용됩니다.  
  
또한 `DataRow.["columnName"]` null 할당 인스턴스에 다음 규칙이 적용됩니다.  
  
- 강력한 형식의 null 값이 적절한 강력한 형식의 null 열을 제외한 모든 열에서 기본 *default* 값은 `DbNull.Value`입니다.  
  
- "xsi:nil"에서처럼 XML 파일로 직렬화하는 동안에는 null 값이 작성되지 않습니다.  
  
- 기본값을 포함하여 null이 아닌 모든 값은 항상 XML로 직렬화하는 동안 작성됩니다. 이는 null 값(xsi: nil)이 명시적이고 기본값이 암시적인(XML에 없는 경우 유효성 검사 파서가 연결된 XSD 스키마에서 가져올 수 있음) XSD/XML 의미 체계와는 다릅니다. `DataTable`에서는 그 반대입니다. Null 값은 암시적이고 기본값은 명시적입니다.  
  
- XML 입력에서 읽은 행에 대해 누락된 모든 열 값에는 NULL이 할당됩니다. <xref:System.Data.DataTable.NewRow%2A> 또는 유사한 메서드를 사용하여 만든 행에는 DataColumn의 기본값이 할당됩니다.  
  
- <xref:System.Data.DataRow.IsNull%2A> 메서드는 `DbNull.Value` 및 `INullable.Null`에 대해 `true`를 반환합니다.  
  
## <a name="assigning-null-values"></a>Null 값 할당  
<xref:System.Data.SqlTypes> 인스턴스의 기본값은 null입니다.  
  
<xref:System.Data.SqlTypes>의 null은 형식에 따라 달라지며 `DbNull`과 같은 단일 값으로 나타낼 수 없습니다. `IsNull` 속성을 사용하여 null을 확인합니다.  
  
다음 코드 예제와 같이 <xref:System.Data.DataColumn>에 null 값을 할당할 수 있습니다. 예외를 트리거하지 않고 `SqlTypes` 변수에 null 값을 직접 할당할 수 있습니다.  
  
### <a name="example"></a>예제  
다음 코드 예제에서는 <xref:System.Data.SqlTypes.SqlInt32> 및 <xref:System.Data.SqlTypes.SqlString>으로 정의된 두 개의 열이 있는 <xref:System.Data.DataTable>을 만듭니다. 이 코드는 알려진 값의 행과 null 값의 행을 하나씩 추가하고 <xref:System.Data.DataTable>을 반복하여 변수에 값을 할당하고 콘솔 창에 출력을 표시합니다.  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
이 예제에서 표시되는 결과는 다음과 같습니다.  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>SqlTypes 및 CLR 형식으로 null 값 비교  
Null 값을 비교할 때 `Equals` 메서드가 CLR 형식에서 작동하는 방식과 비교하여 <xref:System.Data.SqlTypes>에서 null 값을 평가하는 방법 간의 차이점을 이해하는 것이 중요합니다. 모든 <xref:System.Data.SqlTypes>`Equals` 메서드는 null 값을 평가하는 데 데이터베이스 의미 체계를 사용합니다. 두 값 중 하나 또는 둘 다 null이면 비교가 null을 생성합니다. 반면에 두 <xref:System.Data.SqlTypes>에서 CLR `Equals` 메서드를 사용하면 둘 다 null인 경우 true가 생성됩니다. 이는 CLR `String.Equals` 메서드와 같은 인스턴스 메서드를 사용하는 경우와 정적/공유 메서드 `SqlString.Equals`를 사용하는 경우의 차이점을 반영합니다.  
  
다음 예제에서는 각각에 null 값 쌍이 전달된 후 빈 문자열 쌍이 전달될 때 `SqlString.Equals` 메서드와 `String.Equals` 메서드 간의 결과 차이를 보여 줍니다.  
  
[!code-csharp[DataWorks SqlString_Equals#1](~/../sqlclient/doc/samples/SqlString_Equals.cs#1)]
  
이 코드는 다음 출력을 생성합니다.  
  
```console
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 데이터 형식 및 ADO.NET](sql-server-data-types.md)
