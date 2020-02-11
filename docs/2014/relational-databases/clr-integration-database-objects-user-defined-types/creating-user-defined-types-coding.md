---
title: 사용자 정의 형식 코딩 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7427de92691a2d5c0a92aac55ac16f47dd2ef6b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75232236"
---
# <a name="coding-user-defined-types"></a>사용자 정의 형식 코딩
  UDT(사용자 정의 형식) 정의를 코딩하는 경우 UDT를 클래스 또는 구조로 구현할지 여부와 선택한 형식 및 직렬화 옵션에 따라 다양한 기능을 구현해야 합니다.  
  
 이 섹션의 예에서는 `Point` UDT를 `struct`(Visual Basic의 경우 `Structure`)로 구현하는 방법을 보여 줍니다. 
  `Point` UDT는 속성 프로시저로 구현된 X 및 Y 좌표로 구성됩니다.  
  
 UDT를 정의하는 경우 다음 네임스페이스가 필요합니다.  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 
  `Microsoft.SqlServer.Server` 네임스페이스에는 UDT의 다양한 특성에 필요한 개체가 포함되어 있고, `System.Data.SqlTypes` 네임스페이스에는 어셈블리에서 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 데이터 형식을 나타내는 클래스가 포함되어 있습니다. 물론 어셈블리가 올바르게 작동하는 데 필요한 추가 네임스페이스가 있을 수도 있습니다. 또한 `Point` UDT는 문자열 작업에 `System.Text` 네임스페이스를 사용합니다.  
  
> [!NOTE]  
>  
  `/clr:pure`를 사용하여 컴파일된 UDT 등의 Visual C++ 개체는 실행할 수 없습니다.  
  
## <a name="specifying-attributes"></a>특성 지정  
 특성은 직렬화를 사용하여 UDT의 스토리지 표현을 생성하고 UDT를 값으로 클라이언트에 전송하는 방법을 결정합니다.  
  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 은 필수 사항입니다. 
  `Serializable` 특성은 선택 사항입니다. 
  `Microsoft.SqlServer.Server.SqlFacetAttribute`를 지정하여 UDT의 반환 형식에 대한 정보를 제공할 수도 있습니다. 자세한 내용은 [CLR 루틴용 사용자 지정 특성](../clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)을 참조하세요.  
  
### <a name="point-udt-attributes"></a>Point UDT 특성  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`는 `Point` UDT의 스토리지 형식을 `Native`로 설정합니다. 
  `IsByteOrdered`는 `true`로 설정되며, 이 경우 비교 결과는 SQL Server에서 동일한 비교가 관리 코드에서 수행된 결과와 같습니다. UDT는 UDT에서 Null을 인식하도록 하는 `System.Data.SqlTypes.INullable` 인터페이스를 구현합니다.  
  
 다음 코드 조각에서는 `Point` UDT의 특성을 보여 줍니다.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>Null 허용 여부 구현  
 어셈블리의 특성을 올바르게 지정하는 것 외에도 UDT는 Null 허용 여부를 지원해야 합니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드된 UDT는 Null을 인식하지만 UDT에서 Null 값을 인식하려면 `System.Data.SqlTypes.INullable` 인터페이스를 구현해야 합니다.  
  
 CLR 코드 내에서 값이 Null인지 여부를 결정하는 데 필요한 `IsNull` 속성을 만들어야 합니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 UDT의 Null 인스턴스를 찾으면 일반적인 Null 처리 메서드를 사용하여 UDT가 유지됩니다. 서버는 필요하지 않은 경우 UDT 직렬화 또는 역직렬화하는 데 시간을 낭비하지 않으며 Null UDT를 저장하는 공간을 낭비하지 않습니다. 이 Null 검사는 CLR에서 UDT를 가져올 때마다 수행되므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 구문을 사용한 Null UDT 검사가 항상 작동해야 합니다. 또한 서버는 `IsNull` 속성을 사용하여 인스턴스가 Null인지 여부를 테스트합니다. 서버에서 UDT가 Null임을 확인하면 기본 Null 처리를 사용할 수 있습니다.  
  
 
  `get()`의 `IsNull` 메서드는 어떤 방식으로든 특별하게 처리되지 않습니다. 
  `Point` 변수 `@p`가 `Null`이면 기본적으로 `@p.IsNull`은 "1"이 아니라 "NULL"이 됩니다. 이는 `SqlMethod(OnNullCall)` 메서드의 `IsNull get()` 특성이 기본적으로 false로 설정되어 있기 때문입니다. 개체가 `Null`이므로 속성이 요청될 때 개체가 역직렬화되지 않고 메서드가 호출되지 않으며 기본값 "NULL"이 반환됩니다.  
  
### <a name="example"></a>예제  
 다음 예에서 `is_Null` 변수는 프라이빗이며 UDT 인스턴스에 대해 Null 상태를 포함합니다. 코드에서 `is_Null`에 적합한 값을 유지해야 합니다. 또한 UDT의 Null 값 인스턴스를 반환하는 `Null`이라는 정적 속성이 UDT에 있어야 합니다. 이렇게 하면 인스턴스가 데이터베이스에서 실제로 Null인 경우 UDT에서 Null 값을 반환할 수 있습니다.  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>IS NULL 및 IsNull 비교  
 Points(id int, location Point) 스키마 및 다음 쿼리가 포함된 테이블을 살펴 보십시오. 여기서 `Point`는 CLR UDT입니다.  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 두 쿼리에서 모두 위치가 `Null`이 아닌 점의 ID를 반환합니다. 쿼리 1에서는 일반적인 Null 처리가 사용되며 UDT의 역직렬화가 필요하지 않습니다. 반면, 쿼리 2에서는 `Null`이 아닌 각 개체와 호출을 CLR로 역직렬화하여 `IsNull` 속성 값을 얻어야 합니다. 
  `IS NULL`을 사용하면 성능이 향상되는 것이 확실하며 `IsNull` 코드에서 UDT의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 속성을 읽을 이유가 없어야 합니다.  
  
 그러면 `IsNull` 속성은 어떤 용도로 사용됩니까? 첫째, CLR 코드 내에서 값이 `Null`인지 여부를 결정하는 데 필요합니다. 둘째, 서버에서 인스턴스가 `Null`인지 여부를 테스트할 수 있어야 하므로 이 속성은 서버에서 사용됩니다. 서버에서 `Null`임을 확인하면 기본 Null 처리를 사용하여 처리할 수 있습니다.  
  
## <a name="implementing-the-parse-method"></a>Parse 메서드 구현  
 
  `Parse` 및 `ToString` 메서드를 사용하면 UDT의 문자열 표현으로 변환하거나 그 반대로 변환할 수 있습니다. 
  `Parse` 메서드는 문자열을 UDT로 변환할 수 있게 하며, 
  `static`(Visual Basic의 경우 `Shared`)으로 선언되고 `System.Data.SqlTypes.SqlString` 유형의 매개 변수를 사용해야 합니다.  
  
 다음 코드 예제에서는 `Parse` UDT에 대해 X 및 Y 좌표를 구분하는 `Point` 메서드를 구현합니다. 
  `Parse` 메서드는 `System.Data.SqlTypes.SqlString` 유형의 인수 하나를 사용하며, X 및 Y 값이 쉼표로 구분된 문자열로 제공된다고 가정합니다. 
  `Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall` 특성을 `false`로 설정하면 Point의 Null 인스턴스에서 `Parse` 메서드를 호출할 수 없습니다.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>ToString 메서드 구현  
 
  `ToString` 메서드는 `Point` UDT를 문자열 값으로 변환합니다. 이 경우 `Point` 유형의 Null 인스턴스에 대해 "NULL" 문자열이 반환됩니다. 
  `ToString` 메서드는 `Parse` 메서드와 반대로 `System.Text.StringBuilder`를 사용하여 X 및 Y 좌표 값으로 구성된, 쉼표로 구분된 `System.String`을 반환합니다. **InvokeIfReceiverIsNull** 기본값은 false 이므로의 `Point` null 인스턴스에 대 한 검사는 필요 하지 않습니다.  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>UDT 속성 노출  
 
  `Point` UDT는 `System.Int32` 유형의 공용 읽기/쓰기 속성으로 구현된 X 및 Y 좌표를 노출합니다.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>UDT 값 유효성 검사  
 UDT 데이터를 사용할 때 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 자동으로 이진 값을 UDT 값으로 변환합니다. 이 변환 프로세스에는 값이 유형의 직렬화 형식에 적합하고 값을 올바르게 역직렬화할 수 있는지 확인하는 작업이 포함됩니다. 이렇게 하면 값을 다시 이진 형식으로 변환할 수 있습니다. 또한 바이트 정렬 UDT의 경우 결과 이진 값이 원래 이진 값과 일치하여 잘못된 값이 데이터베이스에 저장되지 않도록 합니다. 경우에 따라 이 검사 수준이 부적절할 수도 있습니다. UDT 값이 예상 도메인이나 범위에 있어야 하는 경우 추가 유효성 검사가 필요할 수도 있습니다. 예를 들어 날짜를 구현하는 UDT의 경우 일 값이 유효한 값의 특정 범위 내에 있는 양수여야 할 수도 있습니다.  
  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName`의  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 속성을 사용하면 데이터가 UDT에 할당되거나 UDT로 변환될 때 서버에서 실행하는 유효성 검사 메서드의 이름을 제공할 수 있습니다. 
  `ValidationMethodName`은 bcp 유틸리티, BULK INSERT, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, 분산 쿼리 및 TDS(Tabular Data Stream) RPC(원격 프로시저 호출) 작업을 실행하는 동안에도 호출됩니다. 
  `ValidationMethodName`의 기본값은 유효성 검사 메서드가 없음을 나타내는 Null입니다.  
  
### <a name="example"></a>예제  
 다음 코드 조각에서는 `Point`의 `ValidationMethodName`을 지정하는 `ValidatePoint` 클래스 선언을 보여 줍니다.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 유효성 검사 메서드가 지정된 경우 해당 메서드에 다음 코드 조각과 유사한 서명이 있어야 합니다.  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 유효성 검사 메서드는 모든 범위를 가질 수 있으며 값이 유효한 경우 `true`, 그렇지 않으면 `false`을 반환해야 합니다. 메서드에서 `false`를 반환하고 예외를 throw하면 값이 잘못된 것으로 처리되고 오류가 발생합니다.  
  
 아래 코드 예제에서는 값이 0보다 큰 X 및 Y 좌표만 허용합니다.  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>유효성 검사 메서드 제한 사항  
 서버는 개별 속성을 설정하여 데이터가 삽입되거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 문을 사용하여 데이터가 삽입될 때가 아니라 서버에서 변환을 수행할 때 유효성 검사 메서드를 호출합니다.  
  
 모든 상황에서 유효성 검사 메서드를 실행 하려면 속성 setter 및 `Parse` 메서드에서 유효성 검사 메서드를 명시적으로 호출 해야 합니다. 이것은 요구 사항은 아니며 경우에 따라 바람직하지 않을 수도 있습니다.  
  
### <a name="parse-validation-example"></a>유효성 검사 구문 분석 예  
 클래스가 클래스에서 호출 되도록 하려면 `Parse` 메서드 및 X 및 Y 좌표 값을 설정 하는 속성 프로시저에서 호출 해야 합니다. `ValidatePoint` `Point` 다음 코드 조각에서는 `ValidatePoint` `Parse` 함수에서 유효성 검사 메서드를 호출 하는 방법을 보여 줍니다.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>속성 유효성 검사 예  
 다음 코드 조각에서는 X 및 Y 좌표를 `ValidatePoint` 설정 하는 속성 프로시저에서 유효성 검사 메서드를 호출 하는 방법을 보여 줍니다.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>UDT 메서드 코딩  
 UDT 메서드를 코딩하는 경우 사용된 알고리즘이 시간에 따라 변경될 수 있는지 여부를 고려합니다. 변경되는 경우 UDT에서 사용하는 메서드에 대해 별도의 클래스를 만들어야 할 수도 있습니다. 알고리즘이 변경되면 새 코드를 사용하여 클래스를 다시 컴파일하고 UDT에 영향을 주지 않고 어셈블리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드할 수 있습니다. 대체로 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 문을 사용하여 UDT를 다시 로드할 수 있지만 이 경우 기존 데이터에서 문제가 발생할 수 있습니다. 예를 들어 `Currency` **AdventureWorks** 예제 데이터베이스에 포함 된 UDT는 **convertcurrency** 함수를 사용 하 여 별도의 클래스에 구현 된 통화 값을 변환 합니다. 변환 알고리즘이 미래에 예기치 않은 방식으로 변경되거나 새 기능이 필요할 수도 있습니다. **Convertcurrency** 함수를 `Currency` UDT 구현에서 분리 하면 나중에 변경 하는 것을 계획할 때 유연성을 높일 수 있습니다.  
  
### <a name="example"></a>예제  
 클래스 `Point` 에는 거리를 계산 하기 위한 세 가지 간단한 메서드인 **distance**, **distancefrom** 및 **DistanceFromXY**가 포함 되어 있습니다. 각 메서드는 `double`에서 0까지의 거리, 지정된 점에서 `Point`까지의 거리 및 지정된 X 및 Y 좌표에서 `Point`까지의 거리를 계산하는 `Point`을 반환합니다. 각 호출에 대 한 **Distance** 및 **** **distancefrom** 는 각 메서드에 서로 다른 인수를 사용 하는 방법을 보여 줍니다.  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>SqlMethod 특성 사용  
 
  `Microsoft.SqlServer.Server.SqlMethodAttribute` 클래스는 Null 호출 동작에 결정성을 지정하고 메서드가 변경자(mutator)인지 여부를 지정하기 위해 메서드 정의를 표시하는 데 사용할 수 있는 사용자 지정 특성을 제공합니다. 이러한 속성에 대해서는 기본값이 사용되며, 사용자 지정 특성은 기본값이 아닌 값이 필요한 경우에만 사용됩니다.  
  
> [!NOTE]  
>  
  `SqlMethodAttribute` 클래스는 `SqlFunctionAttribute` 클래스에서 상속되므로 `SqlMethodAttribute`는 `FillRowMethodName`의 `TableDefinition` 및 `SqlFunctionAttribute` 필드에서 상속됩니다. 즉, 적합하지 않은 테이블 반환 메서드를 쓸 수 있음을 의미합니다. 메서드가 컴파일되고 어셈블리가 `IEnumerable` 배포 되지만 런타임에 반환 형식에 대 한 오류가 발생 하는 이유는 어셈블리 ' assembly '\<\<\<의 클래스 ' 클래스> '에 있는 "메서드, 속성 또는 필드 ' 이름> '이 (가)> '의 반환 형식이 잘못 되었습니다." 라는 메시지와 함께 런타임에 발생 합니다.  
  
 다음 표에서는 UDT 메서드에 사용할 수 있는 몇 개의 관련된 `Microsoft.SqlServer.Server.SqlMethodAttribute` 속성에 대해 설명하고 해당 기본값을 표시합니다.  
  
 DataAccess  
 함수가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 저장된 사용자 데이터에 대한 액세스를 수행하는지 여부를 나타냅니다. 기본값은 `DataAccessKind`.`None`입니다.  
  
 IsDeterministic  
 동일한 입력 값과 동일한 데이터베이스 상태가 지정된 경우 함수에서 항상 동일한 값을 출력하는지 여부를 나타냅니다. 기본값은 `false`입니다.  
  
 IsMutator  
 메서드로 인해 UDT 인스턴스의 상태가 변경되는지 여부를 나타냅니다. 기본값은 `false`입니다.  
  
 IsPrecise  
 함수가 부동 소수점 연산과 같은 부정확한 계산을 수행하는지 여부를 나타냅니다. 기본값은 `false`입니다.  
  
 OnNullCall  
 Null 참조 입력 인수를 지정할 때 메서드가 호출되는지 여부를 나타냅니다. 기본값은 `true`입니다.  
  
### <a name="example"></a>예제  
 
  `Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator` 속성을 사용하면 UDT 인스턴스의 상태 변경을 허용하는 메서드를 표시할 수 있습니다. 
  [!INCLUDE[tsql](../../includes/tsql-md.md)]에서는 UPDATE 문의 SET 절에 두 개의 UDT 속성을 설정할 수 없습니다. 하지만 메서드를 두 멤버를 변경하는 변경자(mutator)로 표시할 수 있습니다.  
  
> [!NOTE]  
>  변경자(mutator) 메서드는 쿼리에 사용할 수 없으며, 대입문이나 데이터 수정 문에서만 호출할 수 있습니다. 변경자(mutator)로 표시된 메서드에서 `void`를 반환하지 않는 경우(Visual Basic의 경우 `Sub`가 아님) CREATE TYPE이 오류로 인해 실패합니다.  
  
 다음 문에서는 `Triangles` 메서드가 포함된 `Rotate` UDT가 있다고 가정합니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE 문에서는 `Rotate` 메서드를 호출합니다.  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 
  `Rotate` 메서드는 `SqlMethod`를 `IsMutator`로 설정하는 `true` 특성으로 데코레이팅되어 있으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 해당 메서드를 변경자(mutator) 메서드로 표시할 수 있습니다. 또한 이 코드에서는 `OnNullCall`을 `false`로 설정하여, Null 참조인 입력 매개 변수가 있을 경우 메서드에서 Null 참조(Visual Basic의 경우 `Nothing`)를 반환한다고 서버에 알립니다.  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>사용자 정의 형식으로 UDT 구현  
 사용자 정의 형식으로 UDT를 구현하는 경우 UDT 데이터 직렬화 및 역직렬화를 처리할 Microsoft.SqlServer.Server.IBinarySerialize 인터페이스를 구현하는 `Read` 및 `Write` 메서드를 구현해야 합니다. 또한 `MaxByteSize`의 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 속성을 지정해야 합니다.  
  
### <a name="the-currency-udt"></a>Currency UDT  
 
  `Currency` UDT는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]부터 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]와 함께 설치할 수 있는 CLR 예제에 포함되어 있습니다.  
  
 
  `Currency` UDT는 특정 culture의 화폐 시스템에서 금액 처리를 지원합니다. 두 개의 필드를 정의해야 합니다. `string`에 대한 `CultureInfo`은 통화를 발행한 주체(예: en-us)를 지정하고 `decimal`에 대한 `CurrencyValue`은 금액을 지정합니다.  
  
 비교를 위해 서버에서 사용되지는 않지만 `Currency` UDT는 단일 메서드 `System.IComparable`를 노출하는 `System.IComparable.CompareTo` 인터페이스를 구현합니다. 이 인터페이스는 culture 내에서 통화 값을 정확하게 비교하거나 정렬해야 하는 경우에 클라이언트 쪽에서 사용됩니다.  
  
 CLR에서 실행되는 코드는 통화 값과 별도로 culture를 비교합니다. 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드의 경우 다음 동작에 의해 비교가 결정됩니다.  
  
1.  
  `IsByteOrdered` 특성을 true로 설정하여 디스크에 저장된 이진 표현을 비교에 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 지정합니다.  
  
2.  
  `Write` UDT에 대해 `Currency` 메서드를 사용하여 UDT가 디스크에 유지되는 방법 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업을 위해 UDT 값이 비교 및 정렬되는 방법을 결정합니다.  
  
3.  다음 이진 형식을 사용하여 `Currency` UDT를 저장합니다.  
  
    1.  오른쪽에 Null 문자를 채워 바이트 0-19에 대한 UTF-16 인코딩 문자열로 culture를 저장합니다.  
  
    2.  바이트 20 이상을 사용하여 통화의 10진수 값을 포함합니다.  
  
 패딩의 목적은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드에서 한 UDT와 다른 UDT를 비교할 때 culture 바이트는 culture 바이트와 비교하고 통화 바이트 값은 통화 바이트 값과 비교하도록 culture를 통화 값과 완전히 분리하는 것입니다.  
  
 `Currency` UDT에 대 한 전체 코드 목록을 보려면 [SQL Server 데이터베이스 엔진 샘플](https://msftengprodsamples.codeplex.com/)에서 CLR 예제를 설치 하는 지침을 따르세요.  
  
### <a name="currency-attributes"></a>통화 특성  
 
  `Currency` UDT는 다음 특성을 사용하여 정의됩니다.  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>IBinarySerialize를 사용하여 읽기 및 쓰기 메서드 만들기  
 
  `UserDefined` 직렬화 형식을 선택하는 경우 `IBinarySerialize` 인터페이스를 구현하고 고유한 `Read` 및 `Write` 메서드도 만들어야 합니다. 
  `Currency` UDT의 다음 프로시저에서는 `System.IO.BinaryReader` 및 `System.IO.BinaryWriter`를 사용하여 UDT를 읽고 씁니다.  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 `Currency` UDT에 대 한 전체 코드 목록은 [SQL Server 데이터베이스 엔진 샘플](https://msftengprodsamples.codeplex.com/)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 정의 형식 만들기](creating-user-defined-types.md)  
  
