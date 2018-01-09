---
title: "사용자 정의 형식 코딩 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f1abec952d7ad6ca57b38ff1bda37134312da4b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="creating-user-defined-types---coding"></a>사용자 정의 형식-코딩 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]사용자 정의 형식 (UDT) 정의 코딩 하는 경우에 있는지 여부를 구현 하는 UDT를 클래스 또는 구조체와 선택한 형식 및 직렬화 옵션에 따라 다양 한 기능을 구현 해야 합니다.  
  
 구현은이 섹션의 예는 **지점** 으로 UDT는 **구조체** (또는 **구조** Visual basic에서). **지점** UDT은 X 및 Y 좌표도 구현 된 속성 프로시저입니다.  
  
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
  
 **Microsoft.SqlServer.Server** UDT의 다양 한 특성에 필요한 개체를 포함 하는 네임 스페이스 및 **System.Data.SqlTypes** 를나타내는클래스를포함하는네임스페이스[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]네이티브 데이터 형식을 어셈블리에 사용할 수 있습니다. 물론 어셈블리가 올바르게 작동하는 데 필요한 추가 네임스페이스가 있을 수도 있습니다. **지점** UDT 또한 사용 하 여는 **System.Text** 문자열 작업에 대 한 네임 스페이스입니다.  
  
> [!NOTE]  
>  Visual c + + 데이터베이스 개체를 사용 하 여 컴파일된 Udt 등 **/clr: pure** 실행에 대 한 지원 되지 않습니다.  
  
## <a name="specifying-attributes"></a>특성 지정  
 특성은 직렬화를 사용하여 UDT의 저장소 표현을 생성하고 UDT를 값으로 클라이언트에 전송하는 방법을 결정합니다.  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** 가 필요 합니다. **Serializable** 특성은 선택 사항입니다. 지정할 수 있습니다는 **Microsoft.SqlServer.Server.SqlFacetAttribute** UDT의 반환 형식에 대 한 정보를 제공 합니다. 자세한 내용은 참조 [CLR 루틴에 대 한 사용자 지정 특성](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)합니다.  
  
### <a name="point-udt-attributes"></a>Point UDT 특성  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** 의 저장소 형식을 설정 하는 **지점** UDT를 **네이티브**합니다. **IsByteOrdered** 로 설정 된 **true**, 비교의 결과가 동일한 지 SQL Server에서 동일한 비교가 관리 코드에서 수행 했 마치 보장 합니다. UDT를 구현 하는 **System.Data.SqlTypes.INullable** null을 인식 하도록 하는 인터페이스입니다.  
  
 다음 코드 조각에 대 한 특성을 보여 줍니다.는 **지점** UDT입니다.  
  
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
 어셈블리의 특성을 올바르게 지정하는 것 외에도 UDT는 Null 허용 여부를 지원해야 합니다. 에 로드 된 Udt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] null 인식 하지만 udt에서 null 값을 인식할 수 순서로 UDT를 구현 해야 합니다는 **System.Data.SqlTypes.INullable** 인터페이스입니다.  
  
 라는 속성이 만들어야 **IsNull**, CLR 코드 내에서 null 값이 있는지 확인 하는 데 필요한 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 UDT의 Null 인스턴스를 찾으면 일반적인 Null 처리 메서드를 사용하여 UDT가 유지됩니다. 서버는 필요하지 않은 경우 UDT 직렬화 또는 역직렬화하는 데 시간을 낭비하지 않으며 Null UDT를 저장하는 공간을 낭비하지 않습니다. 이 Null 검사는 CLR에서 UDT를 가져올 때마다 수행되므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 구문을 사용한 Null UDT 검사가 항상 작동해야 합니다. **IsNull** 속성은 또한 인스턴스가 null 인지 여부를 테스트 서버에서 사용 됩니다. 서버에서 UDT가 Null임을 확인하면 기본 Null 처리를 사용할 수 있습니다.  
  
 **get ()** 방식의 **IsNull** 특별 하 게 처리 어떤 방식으로든에서 않습니다. 경우는 **지점** 변수  **@p**  은 **Null**, 다음  **@p.IsNull**  은 기본적으로 "NULL"을 평가 하지 않습니다: "1". ¿¡´는 **SqlMethod(OnNullCall)** 특성에는 **IsNull get ()** 메서드 기본값은 false입니다. 개체는 **Null**개체가 역직렬화 되지 되, 메서드는, 및 "NULL"의 기본값이 반환 됩니다 속성이 요청 될 때입니다.  
  
### <a name="example"></a>예제  
 다음 예에서 `is_Null` 변수는 전용이며 UDT 인스턴스에 대해 Null 상태를 포함합니다. 코드에서 `is_Null`에 적합한 값을 유지해야 합니다. UDT 이라는 정적 속성이 있어야 **Null** UDT의 null 값 인스턴스를 반환 하는 합니다. 이렇게 하면 인스턴스가 데이터베이스에서 실제로 Null인 경우 UDT에서 Null 값을 반환할 수 있습니다.  
  
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
  
### <a name="is-null-vs-isnull"></a>IS NULL 및 IsNull  
 여기서 스키마 점을 (id int, 위치 지점)를 포함 하는 테이블 **지점** CLR UDT 및 다음 쿼리는:  
  
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
  
 두 쿼리 모두 아닌 점의 Id를 반환**Null** 위치입니다. 쿼리 1에서는 일반적인 Null 처리가 사용되며 UDT의 역직렬화가 필요하지 않습니다. 쿼리 2, 반면에 대 한 역직렬화 아닌 각**Null** 개체와 호출을 CLR의 값을 가져옵니다는 **IsNull** 속성입니다. 명확 하 게 사용 하 여 **IS NULL** 성능이 향상 됩니다 하 고 있으면 안을 읽을 이유가 **IsNull** 에서 UDT의 속성 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드입니다.  
  
 이란 사용은 **IsNull** 속성? 첫째, 값이 있는지 확인 하려면 필요한 **Null** CLR 코드 내에서. 서버 인스턴스가 있는지 여부를 테스트 방법이 필요 합니다. 둘째, **Null**이므로이 속성은 서버에서 사용 합니다. 것을 확인 한 후 **Null**, 취급 하는 데 하면 기본 null 처리를 사용할 수 있습니다.  
  
## <a name="implementing-the-parse-method"></a>Parse 메서드 구현  
 **구문 분석** 및 **ToString** 와 UDT의 문자열 표현을 상호 변환에 대 한 메서드를 사용 합니다. **구문 분석** 메서드를 사용 하는 문자열을 UDT로 변환할 수 있습니다. 으로 선언 되어야 합니다 **정적** (또는 **Shared** Visual basic에서), 형식의 매개 변수를 사용 하 고 **System.Data.SqlTypes.SqlString**합니다.  
  
 다음 코드 구현은 **구문 분석** 에 대 한 메서드는 **지점** X 및 Y 좌표를 구분 하는 UDT입니다. **구문 분석** 메서드는 형식의 단일 인수 **System.Data.SqlTypes.SqlString**, X 및 Y 값을 쉼표로 구분 된 문자열로 제공 된 것으로 가정 하 고 있습니다. 설정의 **Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall** 특성을 **false** 방지는 **구문 분석** 에서 null 인스턴스에서 호출 되는 메서드 점입니다.  
  
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
 **ToString** 메서드 변환은 **지점** UDT를 문자열 값입니다. 문자열 "NULL"의 Null 인스턴스에 대해 반환 되는 경우에 **지점** 유형입니다. **ToString** 메서드 역순으로 **구문 분석** 메서드를 사용 하 여 한 **System.Text.StringBuilder** 쉼표로 구분 하 여 반환할 **System.String**X 및 Y 좌표 값으로 이루어진 합니다. 때문에 **InvokeIfReceiverIsNull** 기본값은 false의 null 인스턴스 검사가 **지점** 필요 하지 않습니다.  
  
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
 **지점** UDT 유형의 공용 읽기 / 쓰기 속성으로 구현 된 X 및 Y 좌표를 노출 **System.Int32**합니다.  
  
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
 UDT 데이터를 사용할 때 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 자동으로 이진 값을 UDT 값으로 변환합니다. 이 변환 프로세스에는 값이 유형의 직렬화 형식에 적합하고 값을 올바르게 역직렬화할 수 있는지 확인하는 작업이 포함됩니다. 이렇게 하면 값 다시 이진 형식으로 변환할 수 있습니다. 또한 바이트 정렬 UDT의 경우 결과 이진 값이 원래 이진 값과 일치하여 잘못된 값이 데이터베이스에 저장되지 않도록 합니다. 경우에 따라 이 검사 수준이 부적절할 수도 있습니다. UDT 값이 예상 도메인이나 범위에 있어야 하는 경우 추가 유효성 검사가 필요할 수도 있습니다. 예를 들어 날짜를 구현하는 UDT의 경우 일 값이 유효한 값의 특정 범위 내에 있는 양수여야 할 수도 있습니다.  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName** 의 속성은 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** 이름을 제공할 수 있습니다. 서버 시 실행 하는 유효성 검사 메서드의 데이터가 UDT에 할당 되거나 UDT로 변환 합니다. **ValidationMethodName** bcp 유틸리티, BULK INSERT, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, 분산된 쿼리 및 테이블 형식 데이터 TDS (stream) 원격 프로시저 호출 (RPC) 작업을 실행 하는 동안에 호출 됩니다. 에 대 한 기본값 **ValidationMethodName** 유효성 검사 메서드가 없음을 나타내는 null입니다.  
  
### <a name="example"></a>예제  
 다음 코드 조각에 대 한 선언을 보여 줍니다.는 **지점** 지정 하는 클래스는 **ValidationMethodName** 의 **ValidatePoint**합니다.  
  
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
  
 유효성 검사 메서드가 모든 범위를 가질 수 및 반환 해야 **true** 값이 유효 하 고 **false** 그렇지 않은 경우. 메서드에서 반환 되 면 **false** 해당 값으로 처리는 예외를 throw 또는 유효 하지 않은 고 오류가 발생 합니다.  
  
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
  
 속성 setter에서 유효성 검사 메서드를 명시적으로 호출 해야 및 **구문 분석** 메서드 유효성 검사 메서드를 모든 상황에서 실행 하려는 경우. 이것은 요구 사항은 아니며 경우에 따라 바람직하지 않을 수도 있습니다.  
  
### <a name="parse-validation-example"></a>유효성 검사 구문 분석 예  
 되도록는 **ValidatePoint** 메서드가 호출 되는 **지점** 클래스를 호출 해야에서 **구문 분석** 메서드에서 X 및 Y를 설정 하는 속성 프로시저 좌표 값입니다. 다음 코드 조각에서는 호출 하는 방법을 보여 줍니다.는 **ValidatePoint** 에서 유효성 검사 메서드는 **구문 분석** 함수입니다.  
  
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
 다음 코드 조각에서는 호출 하는 방법을 보여 줍니다.는 **ValidatePoint** X 및 Y 좌표를 설정 하는 속성 프로시저에서 유효성 검사 메서드.  
  
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
 UDT 메서드를 코딩하는 경우 사용된 알고리즘이 시간에 따라 변경될 수 있는지 여부를 고려합니다. 변경되는 경우 UDT에서 사용하는 메서드에 대해 별도의 클래스를 만들어야 할 수도 있습니다. 알고리즘이 변경되면 새 코드를 사용하여 클래스를 다시 컴파일하고 UDT에 영향을 주지 않고 어셈블리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드할 수 있습니다. 대체로 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 문을 사용하여 UDT를 다시 로드할 수 있지만 이 경우 기존 데이터에서 문제가 발생할 수 있습니다. 예를 들어는 **통화** 에 포함 된 UDT는 **AdventureWorks** 샘플 데이터베이스에서는 한 **ConvertCurrency** 구현 되는 통화 값으로 변환 함수 별도 클래스. 변환 알고리즘이 미래에 예기치 않은 방식으로 변경되거나 새 기능이 필요할 수도 있습니다. 구분 하는 **ConvertCurrency** 에서 함수는 **통화** UDT 구현 나중에 변경 내용에 대 한 계획할 때 유연성을 제공 합니다.  
  
### <a name="example"></a>예제  
 **지점** 거리를 계산 하기 위한 세 가지 간단한 메서드를 포함 하는 클래스: **거리**, **DistanceFrom** 및 **DistanceFromXY**합니다. 각 반환는 **double** 까지의 거리를 계산 **가리킨** 를 0으로의 거리를 지정 된 지점에서 **가리킨**, 거리에서 X 및 Y 좌표를 지정 하 고 **지점**합니다. **거리** 및 **DistanceFrom** 호출할 때마다 **DistanceFromXY**, 각 방법에 대해 서로 다른 인수를 사용 하는 방법을 보여 줍니다.  
  
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
 **Microsoft.SqlServer.Server.SqlMethodAttribute** 클래스 null 호출 동작에 결정성을 지정 하기 위해 및 메서드에서 변경자 (mutator) 인지를 지정 하는 메서드 정의 표시 하는 데 사용할 수 있는 사용자 지정 특성을 제공 합니다. 이러한 속성에 대해서는 기본값이 사용되며, 사용자 지정 특성은 기본값이 아닌 값이 필요한 경우에만 사용됩니다.  
  
> [!NOTE]  
>  **SqlMethodAttribute** 클래스에서 상속 된 **SqlFunctionAttribute** 하므로 클래스 **SqlMethodAttribute** 상속의 **FillRowMethodName** 및 **TableDefinition** 에서 필드 **SqlFunctionAttribute**합니다. 즉, 적합하지 않은 테이블 반환 메서드를 쓸 수 있음을 의미합니다. 메서드가 컴파일되고 어셈블리가 배포 되지만 오류에 대 한는 **IEnumerable** 다음 메시지와 런타임 시 형식 발생 반환: "메서드, 속성 또는 필드 '\<이름 >'에서 클래스의\<클래스 >' 어셈블리에서 '\<어셈블리 >' 반환 형식이 잘못 되었습니다. "  
  
 다음 표에서 개의 관련 된 일부 설명 **Microsoft.SqlServer.Server.SqlMethodAttribute** UDT 메서드에 사용할 수 있으며 해당 기본값을 나열 하는 속성입니다.  
  
 DataAccess  
 함수가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 저장된 사용자 데이터에 대한 액세스를 수행하는지 여부를 나타냅니다. 기본값은 **DataAccessKind**. **None**합니다.  
  
 IsDeterministic  
 동일한 입력 값과 동일한 데이터베이스 상태가 지정된 경우 함수에서 항상 동일한 값을 출력하는지 여부를 나타냅니다. 기본값은 **false**합니다.  
  
 IsMutator  
 메서드로 인해 UDT 인스턴스의 상태가 변경되는지 여부를 나타냅니다. 기본값은 **false**합니다.  
  
 IsPrecise  
 함수가 부동 소수점 연산과 같은 부정확한 계산을 수행하는지 여부를 나타냅니다. 기본값은 **false**합니다.  
  
 OnNullCall  
 Null 참조 입력 인수를 지정할 때 메서드가 호출되는지 여부를 나타냅니다. 기본값은 **true**합니다.  
  
### <a name="example"></a>예제  
 **Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator** 속성을 사용 하면 UDT 인스턴스의 상태 변경을 허용 하는 메서드를 표시할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서는 UPDATE 문의 SET 절에 두 개의 UDT 속성을 설정할 수 없습니다. 하지만 메서드를 두 멤버를 변경하는 변경자(mutator)로 표시할 수 있습니다.  
  
> [!NOTE]  
>  변경자(mutator) 메서드는 쿼리에 사용할 수 없으며, 대입문이나 데이터 수정 문에서만 호출할 수 있습니다. 변경자 (mutator)을 반환 하지 않는 것으로 표시 하는 메서드 **void** (없거나는 **Sub** Visual basic에서), 오류가 발생 하 여 CREATE TYPE이 실패 합니다.  
  
 다음 문은 있다고 가정는 **삼각형** 있는 UDT는 **회전** 메서드. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] update 문을 호출 하 여 **회전** 메서드:  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 **회전** 로 데코레이팅된 메서드는 **SqlMethod** 설정을 특성 **IsMutator** 를 **true** 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 표시할 수 변경자 (mutator) 메서드로 메서드입니다. 코드에서는 또한 설정 **OnNullCall** 를 **false**, 메서드가 null 참조를 반환 한다고 서버에 나타냅니다 (**Nothing** Visual Basic의) 입력의 경우 매개 변수는 null 참조입니다.  
  
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
 사용자 정의 형식으로 UDT를 구현 하는 경우 구현 해야 **읽기** 및 **쓰기** 는 처리할 Microsoft.SqlServer.Server.IBinarySerialize 인터페이스를 직렬화 하는 작업을 구현 하는 메서드 및 UDT 데이터를 역직렬화합니다. 도 지정 해야는 **MaxByteSize** 의 속성은 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**합니다.  
  
### <a name="the-currency-udt"></a>Currency UDT  
 **통화** UDT는 함께 설치할 수 있는 CLR 예제에 포함 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]부터 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다.  
  
 **통화** UDT는 특정 culture의 화폐 시스템에서 금액 처리를 지원 합니다. 두 개의 필드를 정의 해야 합니다:는 **문자열** 에 대 한 **CultureInfo**, 통화를 발행 한 주체를 지정 하는 (en-예) 및 **10 진수** 에 대 한  **CurrencyValue**, 금액입니다.  
  
 비교를 위해 서버에서 사용 되지 않지만 **통화** UDT를 구현 하는 **System.IComparable** 단일 메서드를 노출 하는 인터페이스  **System.IComparable.CompareTo**합니다. 이 인터페이스는 culture 내에서 통화 값을 정확하게 비교하거나 정렬해야 하는 경우에 클라이언트 쪽에서 사용됩니다.  
  
 CLR에서 실행되는 코드는 통화 값과 별도로 culture를 비교합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드의 경우 다음 동작에 의해 비교가 결정됩니다.  
  
1.  설정의 **IsByteOrdered** 특성을 true로 알려 주는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비교에 대 한 디스크에 저장된 된 이진 표현을 사용 하 합니다.  
  
2.  사용 하 여는 **쓰기** 에 대 한 메서드는 **통화** UDT를 유지 하는 방법을 결정 하는 UDT 디스크에 따라서 UDT 값 비교 및 정렬 방식을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 합니다.  
  
3.  저장 된 **통화** UDT 다음 이진 형식을 사용 하 여:  
  
    1.  오른쪽에 Null 문자를 채워 바이트 0-19에 대한 UTF-16 인코딩 문자열로 culture를 저장합니다.  
  
    2.  바이트 20 이상을 사용하여 통화의 10진수 값을 포함합니다.  
  
 패딩의 목적은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드에서 한 UDT와 다른 UDT를 비교할 때 culture 바이트는 culture 바이트와 비교하고 통화 바이트 값은 통화 바이트 값과 비교하도록 culture를 통화 값과 완전히 분리하는 것입니다.  
  
 에 대 한 전체 코드에 대 한 예제는 **통화** UDT 예제 CLR을 설치 하기 위한 지침에 따라 [SQL Server 데이터베이스 엔진 예제](http://msftengprodsamples.codeplex.com/)합니다.  
  
### <a name="currency-attributes"></a>통화 특성  
 **통화** UDT는 다음 특성으로 정의 됩니다.  
  
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
 선택 하는 경우 **UserDefined** 직렬화 형식을 구현 해야는 **IBinarySerialize** 인터페이스를 직접 만들 **읽기** 및 **쓰기**  메서드. 다음 절차는 **통화** UDT 사용은 **System.IO.BinaryReader** 및 **System.IO.BinaryWriter** UDT를 읽고 있습니다.  
  
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
  
 에 대 한 전체 코드에 대 한 예제는 **통화** UDT 참조 [SQL Server 데이터베이스 엔진 예제](http://msftengprodsamples.codeplex.com/)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 정의 형식 만들기](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
