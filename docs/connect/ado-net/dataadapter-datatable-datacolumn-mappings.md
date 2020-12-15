---
title: DataAdapter, DataTable 및 DataColumn 매핑
description: DataAdapter에 대해 DataTableMapping 및 ColumnMapping을 설정하는 방법을 설명합니다.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e8b2f84fbbf888fc67cdb8f945d7f0c887c14eaa
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772322"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>DataAdapter, DataTable 및 DataColumn 매핑

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient.SqlDataAdapter>는 <xref:System.Data.Common.DataAdapter.TableMappings%2A> 속성에 0개 이상의 <xref:System.Data.Common.DataTableMapping> 개체 컬렉션을 포함합니다. **DataTableMapping** 은 데이터 원본에 대한 쿼리에서 반환된 데이터와 <xref:System.Data.DataTable> 사이에 마스터 매핑을 제공합니다. **DataTableMapping** 이름은 **DataTable** 이름 대신 **DataAdapter** 의 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 메서드에 전달될 수 있습니다. 다음 예제에서는 **Authors** 테이블에 대해 **AuthorsMapping** 이라는 **DataTableMapping** 을 만듭니다.

```csharp
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");
```

**DataTableMapping** 을 통해 데이터베이스의 열 이름과 다른 **DataTable** 의 열 이름을 사용할 수 있습니다. **DataAdapter** 는 테이블이 업데이트될 때 매핑을 통해 열을 일치시킵니다.

> [!NOTE]
> **DataAdapter** 의 **Fill** 또는 **Update** 메서드를 호출할 때 **TableName** 또는 **DataTableMapping** 이름을 지정하지 않으면 **DataAdapter** 가 “Table”이라는 **DataTableMapping** 을 찾습니다. 해당 **DataTableMapping** 이 없으면 **DataTable** 의 **TableName** 은 “Table”입니다. “Table”이라는 이름의 **DataTableMapping** 을 만들어 기본 **DataTableMapping** 을 지정할 수 있습니다.

다음 코드 예제에서는 <xref:System.Data.Common> 네임스페이스에서 **DataTableMapping** 을 만들고, 이름을 “Table”로 하여 지정된 **DataAdapter** 의 기본 매핑으로 설정합니다. 그런 다음, 쿼리 결과의 첫 번째 테이블(**Northwind** 데이터베이스의 **Customers** 테이블)에 있는 열을 <xref:System.Data.DataSet>의 **Northwind Customers** 테이블에 있는, 사용자에게 더 친숙한 이름 세트로 매핑합니다. 매핑되지 않는 열의 경우 데이터 소스의 열 이름이 사용됩니다.

[!code-csharp[SqlDataAdapter_TableMappings#1](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#1)]

나중에 동일한 **DataAdapter** 에서 다른 매핑을 사용하는 다른 테이블의 로드를 지원하도록 할 수도 있습니다. 이를 수행하려면 **DataTableMapping** 개체를 추가합니다.

**Fill** 메서드에 **DataSet** 의 인스턴스와 **DataTableMapping** 이름이 전달될 때 해당 이름의 매핑이 있으면 그 매핑이 사용되고, 없으면 해당 이름의 **DataTable** 이 사용됩니다.

다음 예제에서는 **Customers** 라는 이름의 **DataTableMapping** 과 **BizTalkSchema** 라는 이름의 **DataTable** 을 만듭니다. 그런 다음, SELECT 문에서 반환하는 행을 **BizTalkSchema** **DataTable** 에 매핑합니다.

[!code-csharp[SqlDataAdapter_TableMappings#2](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#2)]

> [!NOTE]
> 열 매핑에 원본 열 이름을 제공하지 않으면 기본 이름이 자동으로 생성됩니다. 열 매핑에 원본 열을 제공하지 않으면 **SourceColumn1** 로 시작하는 증분 기본 이름인 **SourceColumn** *N* 이 열 매핑에 제공됩니다.

> [!NOTE]
> 테이블 매핑에 원본 테이블 이름을 제공하지 않으면 기본 이름이 자동으로 생성됩니다. 테이블 매핑에 원본 테이블 이름을 제공하지 않으면 **SourceTable1** 로 시작하는 증분 기본 이름인 **SourceTable** *N* 이 테이블 매핑에 제공됩니다.

> [!NOTE]
> 사용자가 제공하는 이름이 **ColumnMappingCollection** 에 있는 기존의 기본 열 매핑 이름이나 **DataTableMappingCollection** 에 있는 테이블 매핑 이름과 충돌할 수 있으므로, 열 매핑에 **SourceColumn** *N* 을 제공하거나 테이블 매핑에 **SourceTable** *N* 을 제공하는 명명 규칙은 사용하지 않는 것이 좋습니다. 이미 있는 이름을 제공하면 예외가 throw됩니다.

## <a name="handle-multiple-result-sets"></a>다중 결과 집합 처리

**SelectCommand** 가 여러 개의 테이블을 반환하면 **Fill** 은 **DataSet** 의 테이블에 대해 지정된 테이블 이름으로 시작하여 **TableName** *N*(**TableName1** 로 시작) 형식으로 계속되는 증분 값을 갖는 테이블 이름을 자동으로 생성합니다. 테이블 매핑을 사용하여 자동 생성된 테이블 이름을 **DataSet** 의 테이블에 대해 지정하려는 이름으로 매핑할 수 있습니다. 예를 들어, **Customers** 와 **Orders** 라는 두 테이블을 반환하는 **SelectCommand** 의 경우 **Fill** 에 대해 다음과 같이 호출합니다.

```csharp
adapter.Fill(customersDataSet, "Customers");
```

두 테이블은 **DataSet**: **Customers** 와 **Customers1** 에 만들어집니다. 테이블 매핑을 사용하면 두 번째 테이블이 **Customers1** 대신 **Orders** 로 명명되도록 할 수 있습니다. 이를 수행하려면 다음 예제와 같이 **Customers1** 의 원본 테이블을 **DataSet** 테이블 **Orders** 로 매핑합니다.

[!code-csharp[SqlDataAdapter_TableMappings#3](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#3)]

## <a name="see-also"></a>참고 항목

- [DataAdapters 및 DataReaders](dataadapters-datareaders.md)
- [ADO.NET에서 데이터 검색 및 수정](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
