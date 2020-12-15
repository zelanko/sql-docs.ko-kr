---
title: DataAdapter 매개 변수
description: 데이터 원본에서 데이터를 반환하고 데이터 원본에 대한 변경 내용을 관리하는 DbDataAdapter의 속성에 대해 알아봅니다.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: d72660a55fa047864148c90ae4087782302adc22
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772286"
---
# <a name="dataadapter-parameters"></a>DataAdapter 매개 변수

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:System.Data.Common.DbDataAdapter>에는 데이터 소스에서 데이터를 검색하고 업데이트하는 데 사용되는 다음과 같은 네 가지 속성이 있습니다. <xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> 속성은 데이터 소스에서 데이터를 반환하며 <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A> , <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 및 <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> 속성은 데이터 소스에서 변경 내용을 관리하는 데 사용됩니다.

> [!NOTE]
> `SelectCommand` 속성은 `Fill`의 `DataAdapter` 메서드를 호출하기 전에 설정해야 합니다. `InsertCommand`, `UpdateCommand` 또는 `DeleteCommand` 속성은 `Update`의 `DataAdapter` 메서드가 호출되기 전에 설정해야 하며, <xref:System.Data.DataTable>의 데이터에 적용된 변경 내용에 따라 설정 값이 달라집니다. 예를 들어, 행이 추가되었으면 `InsertCommand`를 호출하기 전에 `Update`를 설정해야 합니다. `Update`가 삽입, 업데이트 또는 삭제된 행을 처리하는 동안 `DataAdapter`는 해당 `Command` 속성을 사용하여 동작을 처리합니다. 수정된 행에 대한 현재 정보는 `Command` 컬렉션을 통해 `Parameters` 개체에 전달됩니다.

데이터 원본에서 행을 업데이트할 때 업데이트할 테이블의 행을 식별하는 고유 식별자를 사용하는 UPDATE 문을 호출합니다. 고유 식별자란 대개 기본 키 필드의 값을 말합니다. UPDATE 문은 다음의 Transact-SQL 문과 같이 고유 식별자와 업데이트된 열 및 값을 모두 포함하는 매개 변수를 사용합니다.

```sql
UPDATE Customers SET CompanyName = @CompanyName
  WHERE CustomerID = @CustomerID  
```  

> [!NOTE]
> 매개 변수 자리 표시자의 구문은 데이터 소스에 따라 다릅니다. 이 예제에서는 SQL Server 데이터 소스용 자리 표시자를 보여 줍니다.

이 예제에서는 `CustomerID`가 `@CustomerID` 매개 변수의 값과 동일한 행에 대해 `CompanyName` 필드가 `@CompanyName` 매개 변수의 값으로 업데이트됩니다. 이 매개 변수는 <xref:Microsoft.Data.SqlClient.SqlParameter> 개체의 <xref:Microsoft.Data.SqlClient.SqlParameter.SourceColumn%2A> 속성을 사용하여 수정된 행의 정보를 검색합니다. 다음은 앞에 나온 샘플 UPDATE 문에 대한 매개 변수입니다. 이 코드에서는 `adapter` 변수가 올바른 <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 개체를 나타낸다고 가정합니다.

[!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter#2](~/../sqlclient/doc/samples/SqlDataAdapter_SqlDataAdapter.cs#2)]

`Add` 컬렉션의 `Parameters` 메서드는 매개 변수 이름, 데이터 형식, 크기(해당 형식에 적용되는 경우) 및 <xref:System.Data.Common.DbParameter.SourceColumn%2A>의 `DataTable` 이름을 사용합니다. <xref:System.Data.Common.DbParameter.SourceVersion%2A> 매개 변수의 `@CustomerID`은 `Original`로 설정됩니다. 그러면 식별하는 열 값이 수정된 <xref:System.Data.DataRow>에서 변경된 경우 데이터 소스의 기존 행이 업데이트됩니다. 이 경우 `Original` 행 값은 데이터 소스의 현재 값과 일치하고 `Current` 행 값에는 업데이트된 값이 포함됩니다. `SourceVersion` 매개 변수의 `@CompanyName`은 설정되어 있지 않으므로 기본값인 `Current` 행 값을 사용합니다.

> [!NOTE]
> `DataAdapter`의 `Fill` 작업과 `DataReader`의 `Get` 메서드 모두에 대해 .NET 형식은 Microsoft SqlClient Data Provider for SQL Server에서 반환된 형식에서 유추됩니다. Microsoft SQL Server 데이터 형식에 대해 유추된 .NET 형식 및 접근자 메서드는 [ADO.NET의 데이터 형식 매핑](data-type-mappings-ado-net.md)에 설명되어 있습니다.

## <a name="parametersourcecolumn-parametersourceversion"></a>Parameter.SourceColumn, Parameter.SourceVersion

`SourceColumn` 및 `SourceVersion`은 `Parameter` 생성자에 인수로 전달되거나 기존 `Parameter`의 속성으로 설정될 수 있습니다. `SourceColumn`은 <xref:System.Data.DataColumn> 값이 검색될 <xref:System.Data.DataRow>의 `Parameter` 이름입니다. `SourceVersion`에서는 `DataRow`가 값을 검색하기 위해 사용하는 `DataAdapter` 버전을 지정합니다.

다음 표에서는 <xref:System.Data.DataRowVersion>에 사용할 수 있는 `SourceVersion` 열거형 값을 보여 줍니다.

|DataRowVersion 열거형|Description|  
|--------------------------------|-----------------|  
|`Current`|열의 현재 값을 사용하는 매개 변수입니다. 이것이 기본값입니다.|  
|`Default`|열의 `DefaultValue`를 사용하는 매개 변수입니다.|  
|`Original`|열의 원래 값을 사용하는 매개 변수입니다.|  
|`Proposed`|제안된 값을 사용하는 매개 변수입니다.|  

다음 단원의 `SqlClient` 코드 예제에서는 <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 열이 두 매개 변수 `CustomerID`(`SourceColumn`) 및 `@CustomerID` (`SET CustomerID = @CustomerID`)에 대한 `@OldCustomerID`으로 사용되는 `WHERE CustomerID = @OldCustomerID`의 매개 변수를 정의합니다. `@CustomerID` 매개 변수는 **CustomerID** 열을 `DataRow`의 현재 값으로 업데이트하는 데 사용됩니다. 결과적으로 `SourceVersion`이 `Current`인 `CustomerID` `SourceColumn`이 사용됩니다. `@OldCustomerID` 매개 변수는 데이터 원본에서 현재 행을 식별하는 데 사용됩니다. 행의 `Original` 버전에 일치하는 열 값이 있으므로 `SourceColumn`이 `CustomerID`인 동일한 `SourceVersion`(`Original`)이 사용됩니다.

## <a name="work-with-sqlclient-parameters"></a>SqlClient 매개 변수 작업

다음 예제에서는 데이터베이스에서 추가적인 스키마 정보를 검색하기 위해 <xref:Microsoft.Data.SqlClient.SqlDataAdapter>를 만들고 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A>을 <xref:System.Data.MissingSchemaAction.AddWithKey>로 설정하는 방법을 보여 줍니다. <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> 및 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> 속성이 설정되고 해당 <xref:Microsoft.Data.SqlClient.SqlParameter> 개체가 <xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> 컬렉션에 추가됩니다. 메서드에서 `SqlDataAdapter` 개체를 반환합니다.

[!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter#1](~/../sqlclient/doc/samples/SqlDataAdapter_SqlDataAdapter.cs#1)]

## <a name="see-also"></a>참고 항목

- [DataAdapters 및 DataReaders](dataadapters-datareaders.md)
- [명령 및 매개 변수](commands-parameters.md)
- [DataAdapter로 데이터 원본 업데이트](update-data-sources-with-dataadapters.md)
- [ADO.NET에서 데이터 형식 매핑](data-type-mappings-ado-net.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
