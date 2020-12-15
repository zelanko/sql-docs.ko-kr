---
title: DataSet에 기존 제약 조건 추가
description: DataSet에 기존 제약 조건을 추가하는 방법을 설명합니다.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 9471f62c36604cb01ea78f558ac3bfbcb7f4bc01
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772345"
---
# <a name="add-existing-constraints-to-a-dataset"></a>DataSet에 기존 제약 조건 추가

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient.SqlDataAdapter>의 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 메서드는 데이터 원본의 테이블 열과 행으로만 <xref:System.Data.DataSet>를 채웁니다. 제약 조건은 일반적으로 데이터 원본에서 설정하지만 **Fill** 메서드는 기본적으로 이 스키마 정보를 **DataSet** 에 추가하지 않습니다.

데이터 원본의 기존 기본 키 제약 조건 정보로 **DataSet** 를 채우려면 **DataAdapter** 의 <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> 메서드를 호출하거나 **Fill** 을 호출하기 전에 **DataAdapter** 의 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> 속성을 **AddWithKey** 로 설정합니다. 이렇게 하면 **DataSet** 의 기본 키 제약 조건이 데이터 원본의 해당 제약 조건을 반영합니다.

> [!NOTE]
> 외래 키 제약 조건 정보는 포함되지 않으므로 명시적으로 만들어야 합니다.

**DataSet** 를 데이터로 채우기 전에 스키마 정보를 추가하면 기본 키 제약 조건이 <xref:System.Data.DataTable> 개체와 함께 **DataSet** 에 포함됩니다. 결과적으로 **DataSet** 의 Fill에 대한 추가 호출이 있으면 기본 키 열 정보를 사용하여 데이터 원본의 새 행을 각 **DataTable** 의 현재 행과 일치시키고 해당 테이블의 현재 데이터를 데이터 원본의 데이터로 덮어씁니다. 스키마 정보가 없으면 데이터 원본의 새 행이 **DataSet** 에 추가되어 결국 행이 중복됩니다.

> [!NOTE]
> 데이터 원본의 열이 자동 증분 열로 식별되면 <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> 메서드 또는 **AddWithKey** 의 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> 속성이 있는 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 메서드는 **AutoIncrement** 속성이 `true`로 설정된 **DataColumn** 을 만듭니다. 그러나 **AutoIncrementStep** 및 **AutoIncrementSeed** 값은 직접 설정해야 합니다.

> [!NOTE]
> **FillSchema** 를 사용하거나 **MissingSchemaAction** 을 **AddWithKey** 로 설정하려면 기본 키 열 정보를 확인하기 위해 데이터 원본에서 추가 처리를 수행해야 합니다. 이러한 추가 처리로 인해 성능이 낮아질 수 있습니다. 디자인 타임에 기본 키 정보를 알고 있으면 기본 키 열을 명시적으로 지정하여 최상의 성능을 얻을 수 있습니다.

다음 코드 예제에서는 <xref:System.Data.Common.DbDataAdapter.FillSchema%2A>를 사용하여 스키마 정보를 **DataSet** 에 추가하는 방법을 보여 줍니다.

[!code-csharp[SqlDataAdapter_FillDataSet#1](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#1)]

다음 코드 예제에서는 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> 속성 및 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 메서드를 사용하여 스키마 정보를 **DataSet** 에 추가하는 방법을 보여 줍니다.

[!code-csharp[SqlDataAdapter_FillDataSet#2](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#2)]

## <a name="handling-multiple-result-sets"></a>다중 결과 집합 처리

**DataAdapter** 는 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>에서 반환된 여러 개의 결과 집합이 충족되면 **DataSet** 에 여러 개의 테이블을 만듭니다. 테이블에는 0부터 시작하되 “Table0”이 아니라 **Table** 로 시작하는 증분 기본 이름 **Table** *N* 이 지정됩니다. 테이블 이름이 <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> 메서드에 인수로 전달되는 경우 테이블에는 0부터 시작하되 “TableName0”이 아니라 **TableName** 으로 시작하는 증분 기본 이름 **TableName** *N* 이 지정됩니다.

## <a name="see-also"></a>참고 항목

- [DataAdapters 및 DataReaders](dataadapters-datareaders.md)
- [ADO.NET에서 데이터 검색 및 수정](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
