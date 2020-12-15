---
title: DataAdapters 및 DataReaders
description: 데이터베이스에서 데이터를 검색하는 Microsoft SqlClient Data Provider for SQL Server DataReader와 데이터 원본에서 데이터를 검색하고 DataSet를 채우는 DataAdapter에 대해 알아봅니다.
ms.date: 11/30/2020
ms.assetid: cc952ca2-ec19-46ab-9189-15174b52cb74
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e71f6218c9fecd956a7c287581caa72a1a787462
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772292"
---
# <a name="dataadapters-and-datareaders"></a>DataAdapters 및 DataReaders

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient Data Provider for SQL Server **DataReader** 를 사용하여 데이터베이스에서 정방향 읽기 전용의 데이터 스트림을 검색할 수 있습니다. 결과는 쿼리가 실행될 때 반환되며 **DataReader** 의 **Read** 메서드를 사용하여 요청할 때까지 클라이언트의 네트워크 버퍼에 저장됩니다. **DataReader** 를 사용하면 사용이 가능해지는 즉시 데이터를 검색하고 기본적으로 한 번에 하나의 행만 메모리에 저장하여 시스템 오버헤드를 줄임으로써 애플리케이션의 성능을 높일 수 있습니다.

<xref:System.Data.Common.DataAdapter>는 데이터 소스에서 데이터를 검색하고 <xref:System.Data.DataSet> 내의 테이블을 채우는 데 사용됩니다. `DataAdapter`는 `DataSet`의 변경 내용을 다시 데이터 소스에 적용합니다. `DataAdapter`는 Microsoft SqlClient Data Provider for SQL Server의 `Connection` 개체를 사용하여 데이터 원본에 연결하고, `Command` 개체를 사용하여 데이터 원본에서 데이터를 검색하고 변경 내용을 확인합니다.

.NET에는 <xref:System.Data.Common.DbDataReader> 및 <xref:System.Data.Common.DbDataAdapter> 개체가 있습니다. Microsoft SqlClient Data Provider for SQL Server에는 <xref:Microsoft.Data.SqlClient.SqlDataReader> 및 <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 개체가 포함됩니다.

## <a name="in-this-section"></a>섹션 내용

[DataReader로 데이터 검색](retrieve-data-by-datareader.md)  
ADO.NET **DataReader** 개체 및 이 개체를 사용하여 데이터 원본에서 결과 스트림을 반환하는 방법을 설명합니다.

[DataAdapter에서 DataSet 채우기](populate-dataset-from-dataadapter.md)  
`DataSet`를 사용하여 테이블, 열 및 행으로 `DataAdapter`을 채우는 방법을 설명합니다.

[DataAdapter 매개 변수](dataadapter-parameters.md)  
`DataAdapter`의 열 내용을 명령 매개 변수에 매핑하는 방법을 비롯하여 `DataSet`의 명령 속성에 매개 변수를 사용하는 방법을 설명합니다.

[DataSet에 기존 제약 조건 추가](add-existing-constraints-to-dataset.md)  
`DataSet`에 기존 제약 조건을 추가하는 방법을 설명합니다.

[DataAdapter, DataTable 및 DataColumn 매핑](dataadapter-datatable-datacolumn-mappings.md)  
`DataTableMappings`에 대해 `ColumnMappings` 및 `DataAdapter`를 설정하는 방법을 설명합니다.

[쿼리 결과를 통해 페이징](paging-through-query-result.md)  
쿼리 결과를 데이터 페이지로 보는 예제를 제공합니다.

[DataAdapter로 데이터 원본 업데이트](update-data-sources-with-dataadapters.md)  
`DataAdapter`를 사용하여 `DataSet`의 변경 내용을 데이터베이스에 적용하는 방법을 설명합니다.

[DataAdapter 이벤트 처리](handle-dataadapter-events.md)  
`DataAdapter` 이벤트와 이벤트 사용 방법을 설명합니다.

[DataAdapter를 사용하여 일괄 작업 수행](batch-operations-using-dataadapters.md)  
`DataSet`의 업데이트를 적용할 때 SQL Server로의 라운드트립 횟수를 줄여 애플리케이션의 성능을 향상시키는 방법을 설명합니다.

## <a name="see-also"></a>참고 항목

- [데이터 원본에 연결](connecting-to-data-source.md)
- [명령 및 매개 변수](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
