---
title: 쿼리 결과를 통해 페이징
description: 쿼리 결과를 데이터 페이지로 보는 예제를 제공합니다.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 2de305e1069964f2d1a67b7f201578c7448d3e09
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772280"
---
# <a name="paging-through-a-query-result"></a>쿼리 결과를 통해 페이징

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

쿼리 결과 페이징은 쿼리의 결과를 작은 단위의 데이터 하위 집합, 즉 페이지로 반환하는 프로세스입니다. 이 방법은 관리하기 쉬운 작은 청크 단위로 결과를 표시하기 위해 일반적으로 사용됩니다.

<xref:Microsoft.Data.SqlClient.SqlDataAdapter>는 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 메서드를 오버로드하여 데이터를 한 페이지씩만 반환하는 기능을 제공합니다. 그러나 **DataAdapter** 에서 요청된 레코드로만 대상 <xref:System.Data.DataTable> 또는 <xref:System.Data.DataSet>를 채우더라도 전체 쿼리를 반환하기 위한 리소스는 계속 사용되기 때문에 대량의 쿼리 결과를 페이징할 경우에는 다른 방법을 사용하는 것이 좋습니다.

전체 쿼리를 반환하기 위한 리소스를 사용하지 않고 데이터 소스에서 데이터 페이지를 반환하려면 필요한 쿼리에만 반환되는 행을 줄이도록 쿼리에 추가 조건을 지정합니다.

<xref:System.Data.Common.DbDataAdapter.Fill%2A> 메서드를 사용하여 데이터 페이지를 반환하려면 데이터 페이지의 첫 번째 레코드에는 **startRecord** 매개 변수를 지정하고, 데이터 페이지의 레코드 수에는 **maxRecords** 매개 변수를 지정합니다.

## <a name="example"></a>예제

다음 코드 예제에서는 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 메서드를 사용하여 페이지 크기가 다섯 개의 레코드인 쿼리 결과의 첫 번째 페이지를 반환하는 방법을 보여 줍니다.

[!code-csharp[SqlDataAdapter_Paging#1](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#1)]

이전 예제에서 **DataSet** 는 다섯 개의 레코드로만 채워지지만 **Orders** 테이블 전체가 반환됩니다. **DataSet** 를 이와 동일한 다섯 개의 레코드로 채우지만 레코드 다섯 개만 반환하려면 다음 코드 예제와 같이 SQL 문에 `TOP` 및 `WHERE` 절을 사용합니다.

[!code-csharp[SqlDataAdapter_Paging#2](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#2)]

> [!NOTE]
> 이러한 방식으로 쿼리 결과를 페이징할 때 다음 코드 예제와 같이 고유 ID를 명령에 전달하여 다음 레코드 페이지를 반환하려면 행을 정렬하는 `unique identifier`를 유지해야 합니다.

[!code-csharp[SqlDataAdapter_Paging#4](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#4)]

**startRecord** 와 **maxRecords** 매개 변수를 사용하는 **Fill** 메서드를 오버로드하여 `next page of records`를 반환하려면 현재 레코드 인덱스를 페이지 크기만큼 증가시키고 테이블을 채웁니다.

> [!NOTE]
> 데이터베이스 서버에서는 **DataSet** 에 레코드 페이지가 하나만 추가되더라도 전체 쿼리 결과를 반환합니다.

다음 코드 예제에서는 다음 데이터 페이지로 채워지기 전에 테이블 행이 지워집니다. 데이터베이스 서버로의 트립을 줄이기 위해 반환되는 행의 일부를 로컬 캐시에 보존할 수도 있습니다.

[!code-csharp[SqlDataAdapter_Paging#3](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#3)]

데이터베이스 서버에서 전체 쿼리를 반환하지 않고 다음 레코드 페이지를 반환하도록 하려면 SELECT 문에 제한 조건을 지정합니다. 이전 예제에서는 마지막 반환 레코드를 유지하므로 해당 레코드를 WHERE 절에 사용하여 다음 코드 예제와 같이 쿼리에 시작 지점을 지정할 수 있습니다.

[!code-csharp[SqlDataAdapter_Paging#5](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#5)]

## <a name="see-also"></a>참고 항목

- [DataAdapters 및 DataReaders](dataadapters-datareaders.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
