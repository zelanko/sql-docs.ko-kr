---
title: 데이터 형식 사용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a649e00e5b77a7b3276e82e34c04657cd8307284
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121583"
---
# <a name="working-with-data-types"></a>데이터 형식 사용
  데이터는 정의된 길이가 있는 문자열, 특정 정확성이 있는 숫자 또는 해당 규칙 집합이 있는 다른 개체인 사용자 정의 데이터 형식과 같은 다양한 유형과 크기로 제공됩니다. <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체는 데이터의 형식을 분류로 올바르게 처리할 수 있도록 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체는 데이터를 허용하는 개체와 연결되어 있습니다. 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하 여 정의 해야 하는 데이터를 반영 하는 관리 개체 (SMO) 개체는 <xref:Microsoft.SqlServer.Management.Smo.DataType> 속성을 개체:  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 데이터를 허용하는 개체의 `DataType` 속성은 여러 가지 방법으로 설정할 수 있습니다.  
  
-   기본 생성자를 사용 하 고 지정 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체 속성을 명시적으로  
  
-   오버 로드 된 생성자를 사용 하 고 지정 된 <xref:Microsoft.SqlServer.Management.Smo.DataType> 매개 변수로 속성.  
  
-   지정 된 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체 생성자에서 인라인.  
  
-   <xref:Microsoft.SqlServer.Management.Smo.DataType> 클래스의 정적 멤버 중 하나(예: `Int`)를 사용합니다. 이렇게 하면 실제로 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체의 인스턴스가 반환됩니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.DataType> 개체에는 데이터 형식을 정의하는 몇 가지 속성이 있습니다. 예를 들어 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 속성을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지정합니다. 상수 값을 나타내는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에 나와 있는 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 열거. 이것은 `varchar`, `nchar`, `currency`, `integer`, `float` 및 `datetime`과 같은 데이터 형식을 참조합니다.  
  
 데이터 형식이 설정된 경우 데이터의 특정 속성을 설정해야 합니다. 예를 들어 `nchar` 유형인 경우 `Length` 속성에서 문자열 데이터의 길이를 설정해야 합니다. 전체 자릿수와 소수 자릿수를 지정해야 하는 숫자 값의 경우도 마찬가지입니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 및 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 데이터 형식은 사용자가 정의한 데이터 형식의 정의가 포함된 개체를 참조합니다. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>은 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 열거형의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 기반으로 합니다. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET 데이터 형식입니다. 일반적으로 이것은 조직에서 정의된 비즈니스 규칙 때문에 데이터베이스에서 자주 다시 사용되는 특정 유형의 데이터를 나타냅니다. 예를 들어 금액과 통화 액면가를 저장하는 데이터 형식은 여러 통화를 다루는 회사에서 유용합니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 열거형에는 모든 목록을 포함의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-데이터 형식을 지원 합니다.  
  
## <a name="examples"></a>예  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>Visual Basic의 생성자 사양으로 DataType 개체 생성  
 기반으로 하는 서로 다른 데이터 형식의 인스턴스를 만드는 생성자를 사용 하는 방법을 보여 주는 코드 예제 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 및 XML 유형에서 개체를 식별하려면 모두 이름 값이 필요합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes1](SMO How to#SMO_VBDataTypes1)]  -->  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>Visual C#의 생성자 사양으로 DataType 개체 생성  
 기반으로 하는 서로 다른 데이터 형식의 인스턴스를 만드는 생성자를 사용 하는 방법을 보여 주는 코드 예제 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 및 XML 유형에서 개체를 식별하려면 모두 이름 값이 필요합니다.  
  
```  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguements specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>Visual Basic의 기본 생성자를 사용하여 DataType 개체 생성  
 기반으로 하는 서로 다른 데이터 형식의 인스턴스를 만들고 기본 생성자를 사용 하는 방법을 보여 주는 코드 예제 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다. 그런 다음 속성을 사용하여 데이터 형식을 지정합니다.  
  
 **참고** 는 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, 모든 XML 형식 개체를 식별 하는 이름 값이 필요 하 고.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes2](SMO How to#SMO_VBDataTypes2)]  -->  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>Visual C#의 기본 생성자를 사용하여 DataType 개체 생성  
 기반으로 하는 서로 다른 데이터 형식의 인스턴스를 만들고 기본 생성자를 사용 하는 방법을 보여 주는 코드 예제 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다. 그런 다음 속성을 사용하여 데이터 형식을 지정합니다.  
  
 **참고** 는 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, 모든 XML 형식 개체를 식별 하는 이름 값이 필요 하 고.  
  
```  
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
  
  
