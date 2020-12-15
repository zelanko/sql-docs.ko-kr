---
title: DataAdapter로 데이터 원본 업데이트
description: DataAdapter의 Update 메서드가 DataSet의 변경 내용을 ADO.NET 애플리케이션의 데이터 원본으로 다시 확인하는 방법을 알아봅니다.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: d1bd9a8c-0e29-40e3-bda8-d89176b72fb1
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 0be62b3c2a63f7b25889e25f88969aa5aaa9b50e
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772297"
---
# <a name="update-data-sources-with-dataadapters"></a>DataAdapter로 데이터 원본 업데이트

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

`Update`의 <xref:System.Data.Common.DataAdapter> 메서드를 호출하면 <xref:System.Data.DataSet>의 변경 내용이 데이터 소스에 다시 적용됩니다. `Update` 메서드는 `Fill` 메서드와 마찬가지로 `DataSet`의 인스턴스, 선택적 <xref:System.Data.DataTable> 개체 또는 `DataTable` 이름을 인수로 사용합니다. `DataSet` 인스턴스는 변경 내용을 포함하는 `DataSet`이며 `DataTable`은 변경 내용을 검색할 테이블을 식별합니다. `DataTable`을 지정하지 않으면 `DataTable`의 첫 번째 `DataSet`이 사용됩니다.

`Update` 메서드를 호출하면 `DataAdapter`가 변경 내용을 분석하여 INSERT, UPDATE, DELETE 등의 적절한 명령을 실행합니다. `DataAdapter`에 대한 변경 사항이 발견되면 <xref:System.Data.DataRow>는 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> 또는 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A>를 사용하여 변경 내용을 처리합니다.

이러한 속성을 사용하면 디자인 타임에 명령 구문을 지정하고 가능한 경우 저장 프로시저를 사용하여 ADO.NET 애플리케이션의 성능을 극대화할 수 있습니다. `Update`를 호출하기 전에 명령을 명시적으로 설정해야 합니다. `Update`를 호출했는데 삭제된 행에 대한 `DeleteCommand`가 없는 경우와 같이 특정 업데이트에 사용할 적절한 명령이 없으면 예외가 throw됩니다.

> [!IMPORTANT]
> `DataAdapter`를 사용하여 데이터를 편집하거나 삭제하기 위해 SQL Server 저장 프로시저를 사용하는 경우 저장 프로시저 정의에서 `SET NOCOUNT ON`을 사용하지 않아야 합니다. 사용할 경우에는 영향을 받는 행 수가 0으로 반환되어 `DataAdapter`가 동시성 충돌로 해석됩니다. 이 경우 <xref:System.Data.DBConcurrencyException>이 throw됩니다.

명령 매개 변수를 사용하여 `DataSet`의 수정된 각 행에 대해 SQL 문이나 저장 프로시저의 입력 및 출력 값을 지정할 수 있습니다. 자세한 내용은 [DataAdapter 매개 변수](dataadapter-parameters.md)를 참조하세요.

> [!NOTE]
> <xref:System.Data.DataTable>에서의 행 삭제 및 제거의 차이점을 이해하는 것이 중요합니다. `Remove` 또는 `RemoveAt` 메서드를 호출하면 행이 즉시 제거됩니다. `DataTable` 또는 `DataSet`를 `DataAdapter`에 전달하고 `Update`를 호출하는 경우 백 엔드 데이터 원본의 모든 해당 행은 **영향을 받지 않습니다**. `Delete` 메서드를 사용하면 행이 `DataTable`에 그대로 남아 있고 삭제 표시됩니다. 그런 다음, `DataTable` 또는 `DataSet`를 `DataAdapter`에 전달하고 `Update`를 호출하는 경우 백 엔드 데이터 원본의 해당 행이 **삭제됩니다**.

`DataTable`이 단일 데이터베이스 테이블에 매핑되거나 단일 데이터베이스 테이블에서 생성된 경우에는 <xref:System.Data.Common.DbCommandBuilder> 개체를 사용하여 `DeleteCommand`의 `InsertCommand`, `UpdateCommand` 및 `DataAdapter` 개체를 자동으로 생성할 수 있습니다. 자세한 내용은 [CommandBuilder를 사용하여 명령 생성](generate-commands-with-commandbuilders.md)을 참조하세요.

## <a name="use-updatedrowsource-to-map-values-to-a-dataset"></a>UpdatedRowSource를 사용하여 DataSet에 값 매핑

<xref:Microsoft.Data.SqlClient.SqlCommand> 개체의 <xref:Microsoft.Data.SqlClient.SqlCommand.UpdatedRowSource%2A> 속성을 사용함으로써 `DataAdapter`의 <xref:System.Data.Common.DbDataAdapter.Update%2A> 메서드에 대한 호출 이후 데이터 원본에서 반환된 값이 `DataTable`에 다시 매핑되는 방식을 제어할 수 있습니다. `UpdatedRowSource` 속성을 <xref:System.Data.UpdateRowSource> 열거형 값 중 하나로 설정하면 `DataAdapter` 명령에서 반환하는 출력 매개 변수를 무시할지 아니면 `DataSet`의 변경된 행에 적용할지 제어할 수 있습니다. 반환되는 첫 번째 행이 있는 경우 이를 `DataTable`의 변경된 행에 적용할지 여부도 지정할 수 있습니다.

다음 표에서는 `UpdateRowSource` 열거형의 여러 값과 각 값이 `DataAdapter`에 사용하는 명령의 동작에 미치는 영향에 대해 설명합니다.

|UpdatedRowSource 열거형|Description|
|----------------------------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|출력 매개 변수 및 반환된 결과 집합의 첫 번째 행 모두 `DataSet`의 변경된 행에 매핑할 수 있습니다.|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|반환된 결과 집합의 첫 번째 행 데이터만 `DataSet`의 변경된 행에 매핑할 수 있습니다.|
|<xref:System.Data.UpdateRowSource.None>|출력 매개 변수 또는 반환된 결과 집합의 행이 모두 무시됩니다.|
|<xref:System.Data.UpdateRowSource.OutputParameters>|출력 매개 변수만 `DataSet`의 변경된 행에 매핑할 수 있습니다.|

`Update` 메서드는 변경 내용을 데이터 소스에 다시 적용하지만 사용자가 `DataSet`을 마지막으로 채운 이후에 다른 클라이언트에서 데이터 소스의 데이터를 수정했을 수도 있습니다. 현재 데이터로 `DataSet`을 새로 고치려면 `DataAdapter` 및 `Fill` 메서드를 사용합니다. 그러면 새 행이 테이블에 추가되고 업데이트된 정보가 기존 행에 통합됩니다.

`Fill` 메서드는 `DataSet`에 있는 행과 `SelectCommand`에서 반환된 행의 기본 키 값을 검사하여 새 행을 추가할지 또는 기존 행을 업데이트할지 결정합니다. `Fill`가 반환한 결과 행의 기본 키 값과 일치하는 `DataSet` 행의 기본 키 값이 발견되면 `SelectCommand` 메서드는 기존 행을 `SelectCommand`가 반환한 행의 정보로 업데이트하고 기존 행의 <xref:System.Data.DataRow.RowState%2A>를 `Unchanged`로 설정합니다 `SelectCommand`가 반환한 행의 기본 키 값이 `DataSet` 행의 기본 키 값과 일치하지 않으면 `Fill` 메서드는 `RowState`가 `Unchanged`인 새 행을 추가합니다.

> [!NOTE]
> `SelectCommand`에서 **OUTER JOIN** 결과를 반환하는 경우 `DataAdapter`는 결과 `DataTable`에 대해 `PrimaryKey` 값을 설정하지 않습니다. 행 중복 문제를 해결하려면 `PrimaryKey`를 직접 정의해야 합니다.

`Update` 메서드를 호출할 때 발생할 수 있는 예외를 처리하려면 행 업데이트 오류가 발생했을 때 `RowUpdated` 이벤트를 사용하여 응답하거나([DataAdapter 이벤트 처리](handle-dataadapter-events.md) 참조), `Update`를 호출하기 전에 <xref:System.Data.Common.DataAdapter.ContinueUpdateOnError%2A>를 `true`로 설정하고 업데이트가 완료되면 특정 행의 `RowError` 속성에 저장된 오류 정보에 응답합니다.

> [!NOTE]
> `DataSet`, `DataTable` 또는 `DataRow`에 대해 `AcceptChanges`를 호출하면 `DataRow`의 `Current` 값으로 `DataRow`의 모든 `Original` 값을 덮어씁니다. 행을 고유하게 식별하는 필드 값을 수정한 경우 `AcceptChanges`를 호출하면 `Original` 값이 데이터 소스의 값과 더 이상 일치하지 않습니다. `DataAdapter`의 `Update` 메서드를 호출하는 동안 각 행에 대해 `AcceptChanges`가 자동으로 호출됩니다. 먼저 `AcceptChangesDuringUpdate`의 `DataAdapter` 속성을 false로 설정하거나 `RowUpdated` 이벤트에 대한 이벤트 처리기를 만들고 <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A>를 <xref:System.Data.UpdateStatus.SkipCurrentRow>로 설정하면 Update 메서드를 호출할 때 원래 값을 보존할 수 있습니다. 자세한 내용은 [DataAdapter 이벤트 처리](handle-dataadapter-events.md)를 참조하세요.

다음 예제에서는 `DataAdapter`의 `UpdateCommand`를 명시적으로 설정하고 `Update` 메서드를 호출하여 수정된 행에 대해 업데이트를 수행하는 방법을 보여 줍니다.

> [!NOTE]
> `UPDATE statement`의 `WHERE clause`에 지정된 매개 변수는 `SourceColumn`의 `Original` 값을 사용하도록 설정됩니다. `Current` 값이 수정되어 데이터 소스에 있는 값과 일치하지 않을 수 있기 때문에 이 설정은 매우 중요합니다. `Original` 값은 데이터 소스에서 `DataTable`을 채우는 데 사용한 값입니다.

[!code-csharp[SqlDataAdapter_Update#1](~/../sqlclient/doc/samples/SqlDataAdapter_Update.cs#1)]

## <a name="autoincrement-columns"></a>AutoIncrement 열

데이터 소스의 테이블에 자동 증분 열이 있으면 저장 프로시저의 출력 매개 변수로 자동 증분 값을 반환하여 테이블의 열에 매핑하거나, 저장 프로시저 또는 SQL 문에서 반환된 결과 집합의 첫 번째 행에 있는 자동 증분 값을 반환하거나, `DataSet`의 `RowUpdated` 이벤트를 통해 추가적인 SELECT 문을 실행하여 `DataAdapter`의 열을 채울 수 있습니다.

## <a name="ordering-of-inserts-updates-and-deletes"></a>삽입, 업데이트 및 삭제의 순서 지정

대부분의 경우에는 `DataSet`을 통해 변경된 내용이 데이터 소스에 전송되는 순서가 매우 중요합니다. 예를 들어 기존 행의 기본 키 값을 업데이트하고 새 기본 키 값이 외래 키로 지정된 새 행을 추가하는 경우에는 삽입하기 전에 업데이트를 처리해야 합니다.

`Select`의 `DataTable` 메서드를 사용하여 특정 `DataRow`의 행만 참조하는 `RowState` 배열을 반환할 수 있습니다. 그런 다음 반환된 `DataRow` 배열을 `Update`의 `DataAdapter` 메서드에 전달하여 수정된 행을 처리할 수 있습니다. 업데이트될 행의 하위 집합을 지정하여 삽입, 업데이트 및 삭제가 처리되는 순서를 제어할 수 있습니다.

## <a name="example"></a>예제

예를 들어, 다음 코드에서는 테이블의 삭제된 행이 먼저 처리되고 업데이트된 행과 삽입된 행이 차례로 처리되도록 합니다.

[!code-csharp[SqlDataAdapter_Update#2](~/../sqlclient/doc/samples/SqlDataAdapter_Update.cs#2)]

## <a name="use-a-dataadapter-to-retrieve-and-update-data"></a>DataAdapter를 사용하여 데이터 검색 및 업데이트

DataAdapter를 사용하여 데이터를 검색하고 업데이트할 수 있습니다.

- 이 샘플에서는 `DataAdapter.AcceptChangesDuringFill`을 사용하여 데이터베이스의 데이터를 복제합니다. 속성이 **false** 로 설정되면 테이블을 채울 때 **AcceptChanges** 가 호출되지 않고 새로 추가된 행이 삽입된 행으로 처리됩니다. 따라서 이 샘플에서는 이러한 행을 사용하여 새 행을 데이터베이스에 삽입합니다.

- 이 샘플에서는 `DataAdapter.TableMappings`를 사용하여 원본 테이블과 DataTable 간의 매핑을 정의합니다.

- 이 샘플에서는 `DataAdapter.FillLoadOption`을 사용하여 어댑터가 **DbDataReader** 에서 **DataTable** 을 채우는 방법을 결정합니다. DataTable을 만들면 속성을 **LoadOption.Upsert** 또는 **LoadOption.PreserveChanges** 로 설정하여 데이터베이스의 데이터를 현재 버전 또는 원래 버전에만 쓸 수 있습니다.

- 또한 이 샘플은 일괄 처리 작업을 수행하기 위해 `DbDataAdapter.UpdateBatchSize`를 사용하여 테이블을 업데이트합니다.

샘플을 컴파일 및 실행하기 전에 다음과 같이 샘플 데이터베이스를 만들어야 합니다.

```sql
USE [master]
GO

CREATE DATABASE [MySchool]

GO

USE [MySchool]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Course]([CourseID] [nvarchar](10) NOT NULL,
[Year] [smallint] NOT NULL,
[Title] [nvarchar](100) NOT NULL,
[Credits] [int] NOT NULL,
[DepartmentID] [int] NOT NULL,
 CONSTRAINT [PK_Course] PRIMARY KEY CLUSTERED
(
[CourseID] ASC,
[Year] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Department]([DepartmentID] [int] IDENTITY(1,1) NOT NULL,
[Name] [nvarchar](50) NOT NULL,
[Budget] [money] NOT NULL,
[StartDate] [datetime] NOT NULL,
[Administrator] [int] NULL,
 CONSTRAINT [PK_Department] PRIMARY KEY CLUSTERED
(
[DepartmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1045', 2012, N'Calculus', 4, 7)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1061', 2012, N'Physics', 4, 1)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2021', 2012, N'Composition', 3, 2)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2042', 2012, N'Literature', 4, 2)

SET IDENTITY_INSERT [dbo].[Department] ON

INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (1, N'Engineering', 350000.0000, CAST(0x0000999C00000000 AS DateTime), 2)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (2, N'English', 120000.0000, CAST(0x0000999C00000000 AS DateTime), 6)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (4, N'Economics', 200000.0000, CAST(0x0000999C00000000 AS DateTime), 4)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (7, N'Mathematics', 250024.0000, CAST(0x0000999C00000000 AS DateTime), 3)
SET IDENTITY_INSERT [dbo].[Department] OFF

ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
```

[!code-csharp[SqlDataAdapter_Properties#1](~/../sqlclient/doc/samples/SqlDataAdapter_Properties.cs#1)]

## <a name="see-also"></a>참고 항목

- [DataAdapters 및 DataReaders](dataadapters-datareaders.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
