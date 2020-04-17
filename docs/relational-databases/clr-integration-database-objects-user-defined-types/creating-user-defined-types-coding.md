---
title: 사용자 정의 유형 코딩 | 마이크로 소프트 문서
description: 이 예제에서는 SQL Server 데이터베이스에서 사용할 UDT를 구현하는 방법을 보여 주며 있습니다. UDT를 구조로 구현합니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
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
ms.openlocfilehash: a9d51cc0c33c8b656df176baa606a88a542ca4bc
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486962"
---
# <a name="creating-user-defined-types---coding"></a>사용자 정의 형식 만들기 - 코딩
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  UDT(사용자 정의 형식) 정의를 코딩하는 경우 UDT를 클래스 또는 구조로 구현할지 여부와 선택한 형식 및 직렬화 옵션에 따라 다양한 기능을 구현해야 합니다.  
  
 이 섹션의 예제에서는 **점 UDT를** **구조체(또는** **Structure** 시각적 기본구조)로 구현하는 것을 보여 줍니다. **점** UDT는 속성 프로시저로 구현된 X 및 Y 좌표로 구성됩니다.  
  
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
  
 **Microsoft.SqlServer.Server** 네임스페이스에는 UDT의 다양한 특성에 필요한 개체가 포함되어 있으며 **System.Data.SqlTypes** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네임스페이스에는 어셈블리에서 사용할 수 있는 네이티브 데이터 형식을 나타내는 클래스가 포함되어 있습니다. 물론 어셈블리가 올바르게 작동하는 데 필요한 추가 네임스페이스가 있을 수도 있습니다. **또한 점** UDT는 문자열 작업에 **System.Text** 네임스페이스를 사용합니다.  
  
> [!NOTE]  
>  **/clr:pure로** 컴파일된 UDT와 같은 Visual C++ 데이터베이스 개체는 실행에 지원되지 않습니다.  
  
## <a name="specifying-attributes"></a>특성 지정  
 특성은 직렬화를 사용하여 UDT의 스토리지 표현을 생성하고 UDT를 값으로 클라이언트에 전송하는 방법을 결정합니다.  
  
 **Microsoft.SqlServer.Server.SqlUser정의 TypeAttribute가** 필요합니다. **Serializable** 특성은 선택 사항입니다. UDT의 반환 유형에 대한 정보를 제공하기 위해 **Microsoft.SqlServer.Server.SqlFacetAttribute를** 지정할 수도 있습니다. 자세한 내용은 [CLR 루틴용 사용자 지정 특성](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)을 참조하세요.  
  
### <a name="point-udt-attributes"></a>Point UDT 특성  
 **Microsoft.SqlServer.Server.SqlUser정의 TypeAttribute는** **지점** UDT에 대한 저장소 형식을 **기본**으로 설정합니다. **IsByteOrdered** **true로**설정되어 관리 코드에서 동일한 비교가 수행된 것처럼 SQL Server에서 비교 결과가 동일하도록 합니다. UDT는 UDT null을 인식하도록 **System.Data.SqlType.INullable** 인터페이스를 구현합니다.  
  
 다음 코드 조각은 **Point** UDT에 대한 특성을 보여 주며,  
  
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
 어셈블리의 특성을 올바르게 지정하는 것 외에도 UDT는 Null 허용 여부를 지원해야 합니다. 로드된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UDT는 null 인식이지만 UDT가 null 값을 인식하려면 UDT가 **System.Data.SqlTypes.INullable** 인터페이스를 구현해야 합니다.  
  
 CLR 코드 내에서 값이 null인지 여부를 확인하는 데 필요한 **IsNull이라는**속성을 만들어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 UDT의 Null 인스턴스를 찾으면 일반적인 Null 처리 메서드를 사용하여 UDT가 유지됩니다. 서버는 필요하지 않은 경우 UDT 직렬화 또는 역직렬화하는 데 시간을 낭비하지 않으며 Null UDT를 저장하는 공간을 낭비하지 않습니다. 이 Null 검사는 CLR에서 UDT를 가져올 때마다 수행되므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 구문을 사용한 Null UDT 검사가 항상 작동해야 합니다. **IsNull** 속성은 인스턴스가 null인지 여부를 테스트하기 위해 서버에서도 사용됩니다. 서버에서 UDT가 Null임을 확인하면 기본 Null 처리를 사용할 수 있습니다.  
  
 **IsNull의** **get()** 메서드는 어떤 식으로든 특별한 경우가 아닙니다. **포인트** 변수 ** \@p가** **Null인** ** \@경우 p.IsNull은** 기본적으로 "1"이 아닌 "NULL"로 평가합니다. 이는 **IsNull get()** 메서드의 **SqlMethod(OnNullCall)** 특성이 기본값으로 false이기 때문입니다. 개체가 **Null이기**때문에 속성이 요청되면 개체가 역직렬화되지 않고 메서드가 호출되지 않으며 "NULL"의 기본값이 반환됩니다.  
  
### <a name="example"></a>예제  
 다음 예에서 `is_Null` 변수는 프라이빗이며 UDT 인스턴스에 대해 Null 상태를 포함합니다. 코드에서 `is_Null`에 적합한 값을 유지해야 합니다. UDT에는 UDT의 null 값 인스턴스를 반환하는 **Null이라는** 정적 속성도 있어야 합니다. 이렇게 하면 인스턴스가 데이터베이스에서 실제로 Null인 경우 UDT에서 Null 값을 반환할 수 있습니다.  
  
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
 **포인트가** CLR UDT인 스키마 포인트(id int, location Point)와 다음 쿼리가 포함된 테이블을 고려합니다.  
  
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
  
 두 쿼리 모두 Null이 아닌**위치가** 있는 점의 아이디를 반환합니다. 쿼리 1에서는 일반적인 Null 처리가 사용되며 UDT의 역직렬화가 필요하지 않습니다. 쿼리 2는 각**비Null** 개체를 역직렬화하고 CLR을 호출하여 **IsNull** 속성의 값을 얻어야 합니다. IS **NULL을** 사용하면 성능이 향상되며 코드에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] UDT의 **IsNull** 속성을 읽을 이유가 없어야 합니다.  
  
 그래서, **IsNull** 속성의 사용은 무엇입니까? 먼저 CLR 코드 내에서 값이 **Null인지** 여부를 결정해야 합니다. 둘째, 서버는 인스턴스가 **Null인지**여부를 테스트하는 방법이 필요하므로 이 속성은 서버에서 사용됩니다. **Null이라고**결정한 후 네이티브 null 처리를 사용하여 처리할 수 있습니다.  
  
## <a name="implementing-the-parse-method"></a>Parse 메서드 구현  
 **구문 분석** 및 **ToString** 메서드는 UDT의 문자열 표현을 및 변환할 수 있도록 합니다. **구문 분석** 메서드를 사용하면 문자열을 UDT로 변환할 수 있습니다. **정적(또는** 시각적 기본에서 **공유됨)으로** 선언되어야 하며 **System.Data.SqlTypes.SqlString**형식의 매개 변수를 가져가야 합니다.  
  
 다음 코드는 X 좌표와 Y 좌표를 구분하는 **Point** UDT에 대한 **구문 분석** 메서드를 구현합니다. **구문 분석** 메서드는 **System.Data.SqlTypes.SqlString**형식의 단일 인수를 가지며 X 및 Y 값이 쉼표 구분 문자열로 제공된다고 가정합니다. **Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall** 특성을 **false로** 설정하면 **구문 분석** 메서드가 포인트의 null 인스턴스에서 호출되는 것을 방지할 수 있습니다.  
  
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
 **ToString** 메서드는 **포인트** UDT를 문자열 값으로 변환합니다. 이 경우 **Point** 형식의 Null 인스턴스에 대해 문자열 "NULL"이 반환됩니다. **ToString** 메서드는 **System.Text.StringBuilder를** 사용하여 X 및 Y 좌표 값으로 구성된 쉼표 구분 **된 System.String을** 반환하여 **구문 분석** 메서드를 반대로 합니다. **InvokeIfReceiverIsNull** 기본값은 false이므로 **포인트의** null 인스턴스에 대한 검사는 필요하지 않습니다.  
  
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
 **포인트** UDT는 **System.Int32**형식의 공용 읽기 쓰기 속성으로 구현되는 X 및 Y 좌표를 노출합니다.  
  
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
  
 **Microsoft.SqlServer.Server.SqlUser정의TypeAttribute.ValidateMethodName** 속성인 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** 속성을 사용하면 데이터가 UDT에 할당되거나 UDT로 변환될 때 서버가 실행되는 유효성 검사 방법의 이름을 제공할 수 있습니다. **유효성 검사MethodName은** bcp 유틸리티, 벌크 삽입, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC 검사 테이블, 분산 쿼리 및 TDS(테이블 형식 데이터 스트림) 원격 프로시저 호출(RPC) 작업을 실행하는 동안에도 호출됩니다. 유효성 검사 **메서드의** 기본값은 null이며 유효성 검사 메서드가 없음을 나타냅니다.  
  
### <a name="example"></a>예제  
 다음 코드 조각은 유효성 검사 메서드 **Name의 유효성 검사 메서드를** 지정 하는 **Point** 클래스에 대 한 선언을 보여 **주면 유효성 검사입니다.**  
  
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
  
 유효성 검사 메서드는 모든 범위를 가질 수 있으며 값이 유효한 경우 **true를** 반환해야 하며 그렇지 않으면 **false가** 됩니다. 메서드가 **false를** 반환하거나 예외를 throw하면 값이 유효하지 않은 것으로 처리되고 오류가 발생합니다.  
  
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
  
 유효성 검사 메서드를 모든 상황에서 실행하려면 속성 setter 및 **Parse** 메서드에서 유효성 검사 메서드를 명시적으로 호출해야 합니다. 이것은 요구 사항은 아니며 경우에 따라 바람직하지 않을 수도 있습니다.  
  
### <a name="parse-validation-example"></a>유효성 검사 구문 분석 예  
 Point **클래스에서** **ValidatePoint** 메서드가 호출되도록 하려면 **구문 분석** 메서드와 X 및 Y 좌표 값을 설정하는 속성 프로시저에서 호출해야 합니다. 다음 코드 조각에서는 **구문 분석** 함수에서 **ValidatePoint** 유효성 검사 메서드를 호출하는 방법을 보여 주어집니다.  
  
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
 다음 코드 조각에서는 X 및 Y 좌표를 설정하는 속성 프로시저에서 **ValidatePoint** 유효성 검사 메서드를 호출하는 방법을 보여 주어집니다.  
  
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
 UDT 메서드를 코딩하는 경우 사용된 알고리즘이 시간에 따라 변경될 수 있는지 여부를 고려합니다. 변경되는 경우 UDT에서 사용하는 메서드에 대해 별도의 클래스를 만들어야 할 수도 있습니다. 알고리즘이 변경되면 새 코드를 사용하여 클래스를 다시 컴파일하고 UDT에 영향을 주지 않고 어셈블리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드할 수 있습니다. 대체로 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 문을 사용하여 UDT를 다시 로드할 수 있지만 이 경우 기존 데이터에서 문제가 발생할 수 있습니다. 예를 들어 **AdventureWorks** 샘플 데이터베이스에 포함된 **통화** UDT는 **ConvertCurrency** 함수를 사용하여 별도의 클래스에서 구현되는 통화 값을 변환합니다. 변환 알고리즘이 미래에 예기치 않은 방식으로 변경되거나 새 기능이 필요할 수도 있습니다. **변환Currency** 함수를 **통화** UDT 구현에서 분리하면 향후 변경 계획을 수립할 때 유연성이 향상됩니다.  
  
### <a name="example"></a>예제  
 **포인트** 클래스에는 **거리,** **거리** 및 **거리로부터의**세 가지 간단한 방법이 포함되어 있습니다. 각각은 **점에서** 0까지의 거리, 지정된 점에서 **점까지의**거리 및 지정된 X 및 Y 좌표에서 **점까지의**거리를 **계산하는 double을** 반환합니다. **거리** 및 **거리각 호출에서** **DistanceFromXY,** 각 방법에 대해 다른 인수를 사용하는 방법을 보여줍니다.  
  
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
 **Microsoft.SqlServer.Server.SqlMethodAttribute** 클래스는 결정성을 지정하고 null 호출 동작을 지정하고 메서드가 뮤태터인지 여부를 지정하기 위해 메서드 정의를 표시하는 데 사용할 수 있는 사용자 지정 특성을 제공합니다. 이러한 속성에 대해서는 기본값이 사용되며, 사용자 지정 특성은 기본값이 아닌 값이 필요한 경우에만 사용됩니다.  
  
> [!NOTE]  
>  **SqlMethodAttribute** 클래스는 **SqlFunctionAttribute** 클래스에서 상속되므로 **SqlMethodAttribute는** **SqlFunctionAttribute에서** **FillRowMethod 및** **테이블 정의** 필드를 상속합니다. 즉, 적합하지 않은 테이블 반환 메서드를 쓸 수 있음을 의미합니다. **IEnumerable** 메서드가 컴파일되고 어셈블리가 배포되지만 "메서드, 속성 또는 필드 '이름\<>' 클래스의 '클래스\<>'에서 어셈블리 '어셈블리\<>'에서 잘못된 반환 형식이 있습니다."  
  
 다음 표에서는 UDT 메서드에서 사용할 수 있는 관련 **Microsoft.SqlServer.Server.SqlMethod 속성** 중 일부를 설명하고 기본 값을 나열합니다.  
  
 DataAccess  
 함수가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 저장된 사용자 데이터에 대한 액세스를 수행하는지 여부를 나타냅니다. 기본값은 **DataAccessKind**. **없음**.  
  
 IsDeterministic  
 동일한 입력 값과 동일한 데이터베이스 상태가 지정된 경우 함수에서 항상 동일한 값을 출력하는지 여부를 나타냅니다. 기본값은 **false입니다.**  
  
 IsMutator  
 메서드로 인해 UDT 인스턴스의 상태가 변경되는지 여부를 나타냅니다. 기본값은 **false입니다.**  
  
 IsPrecise  
 함수가 부동 소수점 연산과 같은 부정확한 계산을 수행하는지 여부를 나타냅니다. 기본값은 **false입니다.**  
  
 OnNullCall  
 Null 참조 입력 인수를 지정할 때 메서드가 호출되는지 여부를 나타냅니다. 기본값은 **true입니다.**  
  
### <a name="example"></a>예제  
 **Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator** 속성을 사용하면 UDT 인스턴스의 상태를 변경할 수 있는 메서드를 표시할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서는 UPDATE 문의 SET 절에 두 개의 UDT 속성을 설정할 수 없습니다. 하지만 메서드를 두 멤버를 변경하는 변경자(mutator)로 표시할 수 있습니다.  
  
> [!NOTE]  
>  변경자(mutator) 메서드는 쿼리에 사용할 수 없으며, 대입문이나 데이터 수정 문에서만 호출할 수 있습니다. 뮤터로 표시된 메서드가 **void를** 반환하지 않거나 Visual Basic의 **하위가** 아닌 경우 CREATE TYPE에 오류가 발생합니다.  
  
 다음 문은 **Rotate** 메서드가 있는 삼각형 UDT가 있다고 **가정합니다.** 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 업데이트 문은 **Rotate** 메서드를 호출합니다.  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 **Rotate** 메서드는 메서드를 뮤터 메서드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 표시할 수 **있도록** **True로 SqlMethod** 특성 설정 **IsMutator로** 장식 됩니다. 또한 이 코드는 **OnNullCall을** **false로**설정하여 메서드가 null 참조(Visual Basic에서**없음)를** 반환한다는 것을 서버에 나타냅니다.  
  
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
 사용자 정의 형식으로 UDT를 구현할 때는 UDT 데이터를 직렬화및 역직렬화처리하기 위해 Microsoft.SqlServer.Server.IBinarySerialize 인터페이스를 구현하는 **읽기** 및 **쓰기** 메서드를 구현해야 합니다. 또한 **Microsoft.SqlServer.Server.SqlUser정의 TypeAttribute**의 **MaxByteSize** 속성을 지정해야 합니다.  
  
### <a name="the-currency-udt"></a>Currency UDT  
 **로** 시작 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 으로 설치할 수 있는 CLR 샘플에는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]통화 UDT가 포함되어 있습니다.  
  
 **통화** UDT는 특정 문화의 통화 시스템에서 금액처리를 지원합니다. 통화(예: en-us)를 발행한 사람을 지정하는 **CultureInfo의** **문자열과** **통화값(moneyValue)의** **소수점** , 금액의 두 필드를 정의해야 합니다.  
  
 비교를 수행하기 위해 서버에서 사용되지 는 않지만 **통화** UDT는 단일 메서드인 **System.IComparable.CompareTo를**노출하는 **System.IComparable** 인터페이스를 구현합니다. 이 인터페이스는 culture 내에서 통화 값을 정확하게 비교하거나 정렬해야 하는 경우에 클라이언트 쪽에서 사용됩니다.  
  
 CLR에서 실행되는 코드는 통화 값과 별도로 culture를 비교합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드의 경우 다음 동작에 의해 비교가 결정됩니다.  
  
1.  **IsByteOrdered** 특성을 true로 설정하여 비교를 위해 디스크에서 지속된 이진 표현을 사용하도록 지시합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
2.  **통화** UDT에 대한 **쓰기** 메서드를 사용하여 UDT가 디스크에서 유지되는 방법과 UDT 값을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 비교하고 작업에 정렬하는 방법을 결정합니다.  
  
3.  다음 이진 형식을 사용하여 **통화** UDT를 저장합니다.  

    1.  오른쪽에 Null 문자를 채워 바이트 0-19에 대한 UTF-16 인코딩 문자열로 culture를 저장합니다.  
  
    2.  바이트 20 이상을 사용하여 통화의 10진수 값을 포함합니다.  
  
 패딩의 목적은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드에서 한 UDT와 다른 UDT를 비교할 때 culture 바이트는 culture 바이트와 비교하고 통화 바이트 값은 통화 바이트 값과 비교하도록 culture를 통화 값과 완전히 분리하는 것입니다.  
  
 **통화** UDT에 대한 전체 코드 목록의 경우 SQL Server 데이터베이스 엔진 샘플에서 CLR 샘플을 설치하는 지침을 [따르십시오.](https://msftengprodsamples.codeplex.com/)  
  
### <a name="currency-attributes"></a>통화 특성  
 **통화** UDT는 다음 특성으로 정의됩니다.  
  
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
 **UserDefined** 직렬화 형식을 선택할 때 **IBinary Serialize** 인터페이스를 구현하고 사용자 고유의 **읽기** 및 **쓰기** 메서드를 만들어야 합니다. **통화** UDT의 다음 절차는 **System.IO.BinaryReader** 및 **System.IO.BinaryWriter를** 사용하여 UDT에서 읽고 씁니다.  
  
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
  
 **통화** UDT에 대한 전체 코드 목록은 [SQL Server 데이터베이스 엔진 샘플을](https://msftengprodsamples.codeplex.com/)참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 정의 형식 만들기](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
