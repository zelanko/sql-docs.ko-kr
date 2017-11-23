---
title: "데이터 형식 작업 | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 68e89b1615013947bd4f249b6ddfd67084db1d68
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="working-with-data-types"></a>데이터 형식 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]데이터에 다양 한 유형과 정의 된 길이, 특정 정확성이 있는 숫자 또는 고유한 규칙 집합이 있는 다른 개체인 사용자 정의 데이터 형식이 포함 된 문자열을 같은 크기를 가져옵니다. <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체에서 올바르게 처리 될 수 있도록 데이터 형식을 분류 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체는 데이터를 허용하는 개체와 연결되어 있습니다. 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하 여 정의 해야 하는 데이터를 허용 하는 관리 개체 (SMO) 개체는 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체 속성:  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 데이터를 허용하는 개체의 **DataType** 속성은 여러 가지 방법으로 설정할 수 있습니다.  
  
-   기본 생성자를 사용 하 고 지정 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체 속성을 명시적으로  
  
-   오버 로드 된 생성자를 사용 하 고 지정 된 <xref:Microsoft.SqlServer.Management.Smo.DataType> 속성을 매개 변수로 합니다.  
  
-   지정 된 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체 생성자에 인라인 합니다.  
  
-   정적 멤버 중 하나를 사용 하 여는 <xref:Microsoft.SqlServer.Management.Smo.DataType> 클래스, 예를 들어 **Int**합니다. 이렇게 하면 실제로 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체의 인스턴스가 반환됩니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체에는 데이터 형식을 정의하는 몇 가지 속성이 있습니다. 예를 들어 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 속성을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지정합니다. 상수 값을 나타내며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에 나열 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 열거형입니다. 이것은 **varchar**, **nchar**, **currency**, **integer**, **float**및 **datetime**과 같은 데이터 형식을 참조합니다.  
  
 데이터 형식이 설정된 경우 데이터의 특정 속성을 설정해야 합니다. 예를 들어 **nchar** 유형인 경우 **Length** 속성에서 문자열 데이터의 길이를 설정해야 합니다. 전체 자릿수와 소수 자릿수를 지정해야 하는 숫자 값의 경우도 마찬가지입니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 및 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 데이터 형식은 사용자가 정의한 데이터 형식의 정의가 포함된 개체를 참조합니다. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>은 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 열거형의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 기반으로 합니다. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 기반 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET 데이터 형식입니다. 일반적으로 이것은 조직에서 정의된 비즈니스 규칙 때문에 데이터베이스에서 자주 다시 사용되는 특정 유형의 데이터를 나타냅니다. 예를 들어 금액과 통화 액면가를 저장하는 데이터 형식은 여러 통화를 다루는 회사에서 유용합니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 열거형에는 모든 목록이 포함 되어는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-지원 되는 데이터 형식입니다.  
  
## <a name="examples"></a>예  
제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 참조 [만들기 Visual C &#35; Visual Studio.NET에서에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>Visual Basic의 생성자 사양으로 DataType 개체 생성  
 이 코드 예제를 기반으로 하는 다른 데이터 형식의 인스턴스를 만드는 생성자를 사용 하는 방법을 보여 줍니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 및 XML 유형에서 개체를 식별하려면 모두 이름 값이 필요합니다.  
  
```VBNET
'Declare a DataType object variable and define the data type in the constructor.
Dim dt As DataType
'For the decimal data type the following two arguements specify precision, and scale.
dt = New DataType(SqlDataType.Decimal, 10, 2)
``` 
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>Visual C#의 생성자 사양으로 DataType 개체 생성  
 이 코드 예제를 기반으로 하는 다른 데이터 형식의 인스턴스를 만드는 생성자를 사용 하는 방법을 보여 줍니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 및 XML 유형에서 개체를 식별하려면 모두 이름 값이 필요합니다.  
  
```csharp  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguements specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>Visual Basic의 기본 생성자를 사용하여 DataType 개체 생성  
 이 코드 예제를 기반으로 하는 다른 데이터 형식의 인스턴스를 만들 기본 생성자를 사용 하는 방법을 보여 줍니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다. 그런 다음 속성을 사용하여 데이터 형식을 지정합니다.  
  
 **참고** 는 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, 및 모든 XML 형식 개체를 식별 하는 이름 값이 필요 합니다.  
  
```VBNET
'Declare and create a DataType object variable.
Dim dt As DataType
dt = New DataType
'Define the data type by setting the SqlDataType property.
dt.SqlDataType = SqlDataType.VarChar
'The VarChar data type requires a value for the MaximumLength property.
dt.MaximumLength = 100
```
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>Visual C#의 기본 생성자를 사용하여 DataType 개체 생성  
 이 코드 예제를 기반으로 하는 다른 데이터 형식의 인스턴스를 만들 기본 생성자를 사용 하는 방법을 보여 줍니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다. 그런 다음 속성을 사용하여 데이터 형식을 지정합니다.  
  
 **참고** 는 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, 및 모든 XML 형식 개체를 식별 하는 이름 값이 필요 합니다.  
  
```csharp  
{   
//Declare and create a DataType object variable.   
DataType dt;   
dt = new DataType();   
//Define the data type by setting the SqlDataType property.   
dt.SqlDataType = SqlDataType.VarChar;   
//The VarChar data type requires a value for the MaximumLength property.   
dt.MaximumLength = 100;   
}  
```  
  
  
