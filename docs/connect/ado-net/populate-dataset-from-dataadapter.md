---
title: DataAdapter에서 DataSet 채우기
description: 데이터 원본에 독립적인 일관된 관계형 프로그래밍 모델을 제공하는 ADO.NET의 DataAdapter에서 DataSet를 채우는 방법을 알아봅니다.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 3fa0ac7d-e266-4954-bfac-3fbe2f913153
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: c632d83b092f5f68ce5bbca32d4315821252603c
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772298"
---
# <a name="populate-a-dataset-from-a-dataadapter"></a>DataAdapter에서 DataSet 채우기

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

ADO.NET <xref:System.Data.DataSet>는 데이터 원본에 독립적인 일관성 있는 관계형 프로그래밍 모델을 제공하는 데이터의 메모리 상주 표현입니다. `DataSet` 은 테이블 및 제약 조건과 테이블 간의 관계를 포함하는 완전한 데이터 집합을 나타냅니다. `DataSet` 은 데이터 소스에 독립적입니다. 따라서 `DataSet` 은 애플리케이션에 대해 로컬인 데이터뿐 아니라 여러 데이터 소스의 데이터도 포함할 수 있습니다. 기존 데이터 소스와의 상호 작용은 `DataAdapter`를 통해 제어됩니다.

`SelectCommand` 의 `DataAdapter` 속성은 데이터 소스에서 데이터를 검색하는 `Command` 개체입니다. `InsertCommand`의 `UpdateCommand`, `DeleteCommand` 및 `DataAdapter` 속성은 `Command` 의 데이터에 대한 수정 내용에 따라 데이터 소스의 데이터에 대한 업데이트를 관리하는 `DataSet`개체입니다. 이러한 속성은 [DataAdapter로 데이터 원본 업데이트](update-data-sources-with-dataadapters.md)에서 자세히 설명합니다.

`Fill` 의 `DataAdapter` 메서드는 `DataSet` 의 `SelectCommand` 결과로 `DataAdapter`을 채우는 데 사용됩니다. `Fill` 은 채울 `DataSet` 과 `DataTable` 개체 또는 `DataTable` 에서 반환된 행으로 채울 `SelectCommand`의 이름을 인수로 사용합니다.

> [!NOTE]
> `DataAdapter` 를 사용하여 모든 테이블을 검색하는 경우 시간이 많이 걸리며, 특히 테이블에 많은 행이 있는 경우 더욱 그렇습니다. 이는 데이터베이스에 액세스하여 데이터를 찾아서 처리한 다음 클라이언트로 데이터를 전송하는 데 많은 시간이 걸리기 때문입니다. 모든 테이블을 클라이언트로 가져오는 경우 서버의 모든 행이 잠기는 문제도 있습니다. 이 경우 `WHERE` 절을 사용하여 클라이언트에 반환되는 행 수를 대폭 줄이면 성능을 개선할 수 있습니다. `SELECT` 문에 필요한 열을 명시적으로 나열하여 클라이언트에 반환되는 데이터의 양을 줄일 수도 있습니다. 한 번에 몇 백 개씩 행을 일괄적으로 검색함으로써 클라이언트에서 현재 일괄 검색 작업이 완료되면 다음 일괄 검색 작업을 시작하는 것도 좋은 방법입니다.

`Fill` 메서드는 `DataReader` 개체를 암시적으로 사용하여 `DataSet`의 테이블 행을 채울 데이터와 `DataSet`에 테이블을 만드는 데 사용되는 열 이름 및 형식을 반환합니다. 테이블과 열은 없는 경우에만 만들어지고 있는 경우 `Fill` 에서 기존의 `DataSet` 스키마를 사용합니다. 열 형식은 [ADO.NET의 데이터 형식 매핑](data-type-mappings-ado-net.md)의 테이블에 따라 .NET Framework 형식으로 만들어집니다. 기본 키가 데이터 원본에 없으면 기본 키는 만들어지지 않고 `DataAdapter` **.** `MissingSchemaAction`이 `MissingSchemaAction` **.** `AddWithKey`로 설정됩니다. `Fill` 에서 테이블의 기본 키가 있음을 발견하면 기본 키 열 값이 데이터 소스에서 반환된 행의 값과 일치하는 행의 데이터 소스 데이터로 `DataSet` 의 데이터를 덮어씁니다. 기본 키가 없으면 해당 데이터가 `DataSet`의 테이블에 추가됩니다. `Fill`은 `DataSet`를 채울 때 있을 수 있는 매핑을 사용합니다([DataAdapter, DataTable 및 DataColumn 매핑](dataadapter-datatable-datacolumn-mappings.md) 참조).

> [!NOTE]
> `SelectCommand` 가 OUTER JOIN의 결과를 반환하면 `DataAdapter` 는 결과 `PrimaryKey` 에 대해 `DataTable`값을 설정하지 않습니다. 행 중복 문제를 해결하려면 `PrimaryKey` 를 직접 정의해야 합니다.

다음 코드 예제에서는 Microsoft SQL Server <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 데이터베이스에 대한 <xref:Microsoft.Data.SqlClient.SqlConnection> 을 사용하는 `Northwind` 의 인스턴스를 만들고 <xref:System.Data.DataTable> 의 `DataSet` 을 고객 목록으로 채웁니다. <xref:Microsoft.Data.SqlClient.SqlConnection> 생성자에 전달되는 <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 인수와 SQL 문은 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> 의 <xref:Microsoft.Data.SqlClient.SqlDataAdapter>속성을 만드는 데 사용됩니다.

## <a name="example"></a>예제

[!code-csharp[SqlDataAdapter_FillDataSet#1](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#1)]

> [!NOTE]
> 이 예제의 코드에서는 `Connection`을 명시적으로 열거나 닫지 않습니다. `Fill` 메서드는 연결이 아직 열려 있지 않으면 `Connection` 에서 사용하고 있는 `DataAdapter` 을 암시적으로 엽니다. `Fill` 에서 연결을 연 경우 `Fill` 이 완료되면 연결도 닫힙니다. `Fill` 또는 `Update`와 같은 단일 작업을 처리할 경우 이렇게 하면 코드가 간단해집니다. 그러나 연결이 열려 있어야 하는 여러 작업을 수행 중인 경우에는 `Open` 의 `Connection`메서드를 명시적으로 호출하고 데이터 소스에 대한 작업을 수행한 다음 `Close` 의 `Connection`메서드를 호출하여 애플리케이션의 성능을 향상시킬 수 있습니다. 다른 클라이언트 애플리케이션에서 사용할 리소스를 사용 가능한 상태로 만들려면 데이터 소스에 연결되어 있는 시간을 가능한 한 짧게 유지하도록 해야 합니다.

## <a name="multiple-result-sets"></a>다중 결과 집합

`DataAdapter` 는 여러 결과 집합을 발견하면 `DataSet`에 여러 테이블을 만듭니다. 테이블에는 Table0부터 시작하는 증분 기본 이름인 Table *N* 이 지정됩니다. 테이블 이름이 인수로 `Fill` 메서드에 전달되면 테이블에는 TableName0부터 시작하는 증분 기본 이름인 TableName *N* 이 지정됩니다.  
  
## <a name="populating-a-dataset-from-multiple-dataadapters"></a>여러 개의 DataAdapter에서 DataSet 채우기  

 여러 개의 `DataAdapter` 개체를 하나의 `DataSet`와 함께 사용할 수 있습니다. `DataAdapter` 는 각각 하나 이상의 `DataTable` 개체를 채우고 업데이트를 다시 관련 데이터 소스에 적용하는 데 사용할 수 있습니다. `DataRelation` 및 `Constraint` 개체를 `DataSet` 에 로컬로 추가하면 각기 다른 데이터 소스의 데이터를 연결할 수 있습니다. 예를 들어, `DataSet` 은 Microsoft SQL Server 데이터베이스, OLE DB를 통해 노출된 IBM DB2 데이터베이스, XML을 스트리밍하는 데이터 소스의 데이터를 포함할 수 있습니다. 하나 이상의 `DataAdapter` 개체에서 각 데이터 소스와의 통신을 처리할 수 있습니다.  
  
### <a name="example"></a>예제  

 다음 코드 예제에서는 Microsoft SQL Server에 있는 `Northwind` 데이터베이스의 고객 목록과 Microsoft Access 2000에 저장된 `Northwind` 데이터베이스의 주문 목록을 채웁니다. 채워진 테이블은 `DataRelation`에 연결되고 고객 목록이 해당 고객의 주문과 함께 표시됩니다.

[!code-csharp[SqlDataAdapter_FillDataSet#2](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#2)]

## <a name="sql-server-decimal-type"></a>SQL Server 10진수 형식

기본적으로 `DataSet`는 .NET 데이터 형식을 사용하여 데이터를 저장합니다. 대부분의 애플리케이션에서 이 형식을 사용하면 데이터 소스 정보를 간편하게 나타낼 수 있습니다. 그러나 이 표현은 데이터 소스의 데이터 형식이 SQL Server decimal 또는 숫자 데이터 형식인 경우 문제를 일으킬 수 있습니다. .NET `decimal` 데이터 형식은 최대 28개의 유효 숫자를 허용하는 한편, SQL Server `decimal` 데이터 형식은 38개의 유효 숫자를 허용합니다. `SqlDataAdapter` 작업 중에 `Fill` 에서 SQL Server `decimal` 필드의 정밀도가 28자보다 크다고 판단하면 현재 행은 `DataTable`에 추가되지 않습니다. 대신 `FillError` 이벤트가 발생하므로 정밀도가 손실되는지 여부를 확인하여 적절하게 대응할 수 있습니다. `FillError` 이벤트에 대한 자세한 내용은 [DataAdapter 이벤트 처리](handle-dataadapter-events.md)를 참조하세요. `decimal` 개체를 사용하고 <xref:Microsoft.Data.SqlClient.SqlDataReader> 메서드를 호출하여 SQL Server <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A> 값을 확인할 수도 있습니다.

ADO.NET에서는 `DataSet`의 <xref:System.Data.SqlTypes>에 대한 지원이 향상되었습니다. 자세한 내용은 [SqlTypes and the DataSet](./sql/sqltypes-dataset.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [DataAdapters 및 DataReaders](dataadapters-datareaders.md)
- [ADO.NET에서 데이터 형식 매핑](data-type-mappings-ado-net.md)
- [MARS(Multiple Active Result Sets)](./sql/multiple-active-result-sets-mars.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
