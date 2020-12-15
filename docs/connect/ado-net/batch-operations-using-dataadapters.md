---
title: DataAdapter를 사용하여 일괄 작업 수행
description: DataSet에서 업데이트를 적용할 때 SQL Server 왕복 수를 줄임으로써 애플리케이션 성능을 향상하는 방법을 설명합니다.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: e72ed5af-b24f-486c-8429-c8fd2208f844
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 1b720dff0678c68396fe7d8cf1f60f3ade70dd9d
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772337"
---
# <a name="batch-operations-using-dataadapters"></a>DataAdapter를 사용하여 일괄 작업 수행

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

ADO.NET의 배치 지원을 사용하면 <xref:System.Data.Common.DataAdapter>를 통해 INSERT, UPDATE 및 DELETE 작업을 한 번에 하나씩 보내지 않고 <xref:System.Data.DataSet> 또는 <xref:System.Data.DataTable>에서 서버로 그룹화할 수 있습니다. 서버로의 라운드트립 횟수가 줄어들면 일반적으로 성능이 크게 개선됩니다. 일괄 업데이트는 Microsoft SqlClient Data Provider for SQL Server(<xref:Microsoft.Data.SqlClient>)에서 지원됩니다.

이전 버전의 ADO.NET에서는 데이터베이스를 <xref:System.Data.DataSet>의 변경 내용으로 업데이트하는 경우 `Update`의 `DataAdapter` 메서드에서 데이터베이스에 대해 한 번에 한 행씩 업데이트를 수행했습니다. 또한 지정한 <xref:System.Data.DataTable>의 행에서 반복될 때 수정되었는지 여부를 확인하기 위해 각 <xref:System.Data.DataRow>를 검사했습니다. 행이 수정된 경우에는 해당 행의 `UpdateCommand` 속성 값에 따라 적절한 `InsertCommand`, `DeleteCommand` 또는 <xref:System.Data.DataRow.RowState%2A>를 호출했습니다. 그리고 행을 업데이트할 때마다 데이터베이스에 대한 네트워크 라운드트립이 수반되었습니다.

Microsoft SqlClient Data Provider for SQL Server에서 <xref:Microsoft.Data.SqlClient.SqlDataAdapter>는 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateBatchSize%2A> 속성을 노출합니다. `UpdateBatchSize`를 양의 정수 값으로 설정하면 데이터베이스에 대한 업데이트가 지정된 크기의 배치로 전송됩니다. 예를 들어 `UpdateBatchSize`를 10으로 설정하면 10개의 개별적인 문을 그룹화하여 하나의 배치로 제출합니다. `UpdateBatchSize`를 0으로 설정하면 <xref:Microsoft.Data.SqlClient.SqlDataAdapter>가 서버에서 처리할 수 있는 최대 배치 크기를 사용합니다. 1로 설정할 경우에는 행이 한 번에 하나씩 전송되므로 배치 업데이트를 사용할 수 없습니다.

> [!NOTE]
> 매우 큰 일괄 처리를 실행하면 성능이 저하될 수 있습니다. 따라서 애플리케이션을 구현하기 전에 최적의 배치 크기 설정을 테스트해야 합니다.

## <a name="use-the-updatebatchsize-property"></a>UpdateBatchSize 속성 사용

배치 업데이트를 사용할 수 있을 때는 DataAdapter <xref:System.Data.IDbCommand.UpdatedRowSource%2A>, `UpdateCommand` 및 `InsertCommand`의 `DeleteCommand` 속성 값을 <xref:System.Data.UpdateRowSource.None> 또는 <xref:System.Data.UpdateRowSource.OutputParameters>로 설정해야 합니다. 배치 업데이트를 수행하는 경우 명령의 <xref:System.Data.IDbCommand.UpdatedRowSource%2A> 속성 값 <xref:System.Data.UpdateRowSource.FirstReturnedRecord> 또는 <xref:System.Data.UpdateRowSource.Both>는 유효하지 않습니다.
  
다음 프로시저에서는 `UpdateBatchSize` 속성을 사용하는 방법을 보여 줍니다. 이 프로시저에서는 **Production.ProductCategory** 테이블의 **ProductCategoryID** 및 **Name** 필드를 표시하는 열이 포함된 <xref:System.Data.DataSet> 개체와 일괄 처리 크기를 나타내는 정수(일괄 처리의 행 개수) 등 두 가지 인수를 사용합니다. 이 코드에서는 <xref:Microsoft.Data.SqlClient.SqlDataAdapter>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> 및 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> 속성을 설정하여 새 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> 개체를 만듭니다. 또한 <xref:System.Data.DataSet> 개체에 수정된 행이 있다고 가정합니다. 그리고 `UpdateBatchSize` 속성을 설정한 다음 업데이트를 실행합니다.

[!code-csharp[SqlDataAdapter_Batch#1](~/../sqlclient/doc/samples/SqlDataAdapter_Batch.cs#1)]

## <a name="handle-batch-update-related-events-and-errors"></a>일괄 업데이트 관련 이벤트 및 오류 처리

**DataAdapter** 에는 두 가지 업데이트 관련 이벤트인 **RowUpdating** 및 **RowUpdated** 가 있습니다. 자세한 내용은 [DataAdapter 이벤트 처리](handle-dataadapter-events.md)를 참조하세요.

### <a name="event-behavior-changes-with-batch-updates"></a>일괄 업데이트를 사용하여 이벤트 동작 변경

일괄 처리가 활성화되면 한 번의 데이터베이스 동작으로 여러 개의 행이 업데이트됩니다. 따라서 `RowUpdated` 이벤트는 배치마다 한 번씩만 발생하지만 `RowUpdating` 이벤트는 행이 처리될 때마다 발생합니다. 일괄 처리가 비활성화되면 일대일 인터리빙으로 두 개의 이벤트가 발생합니다. 이 경우 `RowUpdating` 이벤트 하나와 `RowUpdated` 이벤트 하나가 한 행에 대해 발생한 후 모든 행이 처리될 때까지 `RowUpdating` 및 `RowUpdated` 이벤트가 다음 행에 대해 하나씩 발생합니다.

### <a name="access-updated-rows"></a>업데이트된 행에 액세스

일괄 처리가 비활성화되면 <xref:System.Data.Common.RowUpdatedEventArgs.Row%2A> 클래스의 <xref:System.Data.Common.RowUpdatedEventArgs> 속성을 사용하여 업데이트되는 행에 액세스할 수 있습니다.

일괄 처리가 활성화되면 여러 행에 대해 하나의 `RowUpdated` 이벤트가 생성됩니다. 따라서 각 행에 대한 `Row` 속성 값은 null입니다. `RowUpdating` 이벤트는 계속해서 각 행에 대해 생성됩니다. <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> 클래스의 <xref:System.Data.Common.RowUpdatedEventArgs> 메서드를 사용하면 행에 대한 참조를 배열에 복사하여 처리된 행에 액세스할 수 있습니다. 처리 중인 행이 없으면 `CopyToRows`에서 <xref:System.ArgumentNullException>이 throw됩니다. <xref:System.Data.Common.RowUpdatedEventArgs.RowCount%2A> 메서드를 호출하기 전에 <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> 속성을 사용하여 처리된 행 수를 반환합니다.

### <a name="handle-data-errors"></a>데이터 오류 처리

배치를 실행하면 각각의 개별 문을 실행하는 것과 동일한 효과가 나타납니다. 문은 배치에 추가된 순서대로 실행됩니다. 오류는 배치 모드가 비활성화되어 있는 상태와 동일하게 처리됩니다. 행은 각각 개별적으로 처리됩니다. 데이터베이스에서 성공적으로 처리된 행만 <xref:System.Data.DataRow> 내의 해당 <xref:System.Data.DataTable>에서 업데이트됩니다.

> [!NOTE]
> Microsoft SqlClient Data Provider for SQL Server와 백 엔드 데이터베이스 서버는 일괄 처리 실행이 지원되는 SQL 구문을 결정합니다. 실행을 위해 지원되지 않는 문을 전송하면 예외가 throw될 수 있습니다.

## <a name="see-also"></a>참고 항목

- [DataAdapters 및 DataReaders](dataadapters-datareaders.md)
- [DataAdapter로 데이터 원본 업데이트](update-data-sources-with-dataadapters.md)
- [DataAdapter 이벤트 처리](handle-dataadapter-events.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
