---
title: CommandBuilder를 사용하여 명령 생성
description: 명령 작성기를 사용하여 단일 테이블 SELECT 명령이 있는 `DataAdapter`에 대한 INSERT, UPDATE, DELETE 명령을 자동으로 생성하는 방법을 설명합니다.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 6e3fb8b5-373b-4f9e-ab03-a22693df8e91
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 091f7c2736c240951beb0f434fdcd2efb39a9b59
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428249"
---
# <a name="generating-commands-with-commandbuilders"></a>CommandBuilder를 사용하여 명령 생성

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:System.Data.Common.DbDataAdapter> 개체의 `SelectCommand` 속성이 런타임에 동적으로 지정되는 경우(예: 사용자 로부터 텍스트 명령을 받는 쿼리 도구를 통해) 디자인 타임에 적절한 `InsertCommand`, `UpdateCommand` 또는 `DeleteCommand`를 지정하지 못할 수 있습니다. <xref:System.Data.DataTable>이 단일 데이터베이스 테이블에 매핑되거나 단일 데이터베이스 테이블에서 생성된 경우에는 <xref:System.Data.Common.DbCommandBuilder> 개체를 사용하여 `DeleteCommand`의 `InsertCommand`, `UpdateCommand` 및 <xref:System.Data.Common.DbDataAdapter>를 자동으로 생성할 수 있습니다.

> [!NOTE]
> Microsoft SqlClient Data Provider for SQL Server에서 <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 클래스는 <xref:System.Data.Common.DbDataAdapter> 클래스에서 파생되고, <xref:Microsoft.Data.SqlClient.SqlCommandBuilder> 클래스는 <xref:System.Data.Common.DbCommandBuilder> 클래스에서 파생됩니다.

자동 명령 생성이 작동하도록 하려면 최소한 `SelectCommand` 속성을 설정해야 합니다. `SelectCommand` 속성에서 검색하는 테이블 스키마에 따라 자동으로 생성되는 INSERT, UPDATE 및 DELETE 문의 구문이 결정됩니다.

<xref:System.Data.Common.DbCommandBuilder>는 INSERT, UPDATE 및 DELETE SQL 명령을 생성하는 데 필요한 메타데이터를 반환하기 위해 `SelectCommand`를 실행해야 합니다. 결과적으로 데이터 소스에 추가로 이동해야 하므로 성능이 낮아질 수 있습니다. 최적의 성능을 얻으려면 <xref:System.Data.Common.DbCommandBuilder>를 사용하는 대신 명령을 명시적으로 지정합니다.

> [!NOTE]
> `SelectCommand`는 또한 하나 이상의 기본 키 또는 고유한 열을 반환해야 합니다. 없는 경우 `InvalidOperation` 예외가 생성되고 명령이 생성되지 않습니다.

`DataAdapter`와 연결되어 있는 경우 <xref:System.Data.Common.DbCommandBuilder>는 `InsertCommand`의 `UpdateCommand`, `DeleteCommand` 및 `DataAdapter` 속성을 자동으로 생성합니다(속성이 null 참조인 경우). 속성에 대한 `Command`가 이미 있으면 기존 `Command`가 사용됩니다.

테이블을 두 개 이상 조인하여 만든 데이터베이스 뷰는 단일 데이터베이스 테이블로 간주되지 않습니다. 이 인스턴스에서는 <xref:System.Data.Common.DbCommandBuilder>를 사용하여 자동으로 명령을 생성할 수 없으며, 명시적으로 명령을 지정해야 합니다.

출력 매개 변수를 `DataSet`의 업데이트된 행에 다시 매핑할 수도 있습니다. 일반적인 작업은 자동으로 생성된 ID 필드의 값이나 타임스탬프를 데이터 소스에서 검색하는 것입니다. <xref:System.Data.Common.DbCommandBuilder>는 기본적으로 출력 매개 변수를 업데이트된 행의 열에 매핑하지 않습니다. 이 인스턴스에서는 명령을 명시적으로 지정해야 합니다.

## <a name="rules-for-automatically-generated-commands"></a>자동 생성된 명령에 대한 규칙

다음 표에서는 자동 생성된 명령을 생성하는 방법에 대한 규칙을 보여 줍니다.

|명령|규칙|  
|-------------|----------|  
|`InsertCommand`|<xref:System.Data.DataRow.RowState%2A>의 <xref:System.Data.DataRowState.Added>를 사용하여 테이블의 모든 행에 대해 데이터 소스에 행을 삽입합니다. ID, 식 또는 타임스탬프와 같은 열이 아니라 업데이트할 수 있는 모든 열의 값을 삽입합니다.|  
|`UpdateCommand`|`RowState`의 <xref:System.Data.DataRowState.Modified>를 사용하여 테이블의 모든 행에 대해 데이터 소스의 행을 업데이트합니다. ID 또는 식과 같이 업데이트할 수 없는 열을 제외한 모든 열의 값을 업데이트합니다. 데이터 소스의 열 값이 해당 행의 기본 키 열 값과 일치하고 데이터 소스의 나머지 열이 해당 행의 원래 값과 일치하는 모든 행을 업데이트합니다. 자세한 내용은 이 항목 뒷부분의 "업데이트 및 삭제에 대한 낙관적 동시성 모델"을 참조하세요.|  
|`DeleteCommand`|`RowState`의 <xref:System.Data.DataRowState.Deleted>를 사용하여 테이블의 모든 행에 대해 데이터 소스의 행을 삭제합니다. 열 값이 해당 행의 기본 키 열 값과 일치하고 데이터 소스의 나머지 열이 해당 행의 원래 값과 일치하는 모든 행을 삭제합니다. 자세한 내용은 이 항목 뒷부분의 [업데이트 및 삭제를 위한 낙관적 동시성 모델](#optimistic-concurrency-model-for-updates-and-deletes)을 참조하세요.|

## <a name="optimistic-concurrency-model-for-updates-and-deletes"></a>업데이트 및 삭제를 위한 낙관적 동시성 모델

UPDATE 및 DELETE 문을 위한 명령을 자동으로 생성하는 논리는 낙관적 동시성에 기초합니다. 즉, 레코드가 편집할 수 없도록 잠기지 않으므로 언제든지 다른 사용자나 프로세스가 레코드를 수정할 수 있습니다. SELECT 문에서 반환된 후 UPDATE 또는 DELETE 문이 발행되기 전에 레코드를 수정할 수 있었으므로 자동으로 생성되는 UPDATE 또는 DELETE 문에는 행이 원래 값을 모두 포함하고 데이터 소스에서 삭제되지 않은 경우에만 업데이트되도록 지정하는 WHERE 절이 포함되어 있습니다. 따라서 새 데이터를 덮어쓰는 상황이 발생하지 않습니다.
 
> [!NOTE]
> 자동 생성된 업데이트가 삭제되었거나 <xref:System.Data.DataSet>에 있는 원래 값을 포함하지 않는 행을 업데이트하려고 하는 경우 이 명령은 모든 레코드에 영향을 주지 않으며 <xref:System.Data.DBConcurrencyException>이 throw됩니다.

원래 값에 관계없이 UPDATE나 DELETE가 완료되도록 하려면 자동 명령 생성을 사용하는 대신 `UpdateCommand`에 대해 `DataAdapter`를 명시적으로 설정해야 합니다.

## <a name="limitations-of-automatic-command-generation-logic"></a>자동 명령 생성 논리의 제한 사항

자동 명령 생성에는 다음과 같은 제한 사항이 있습니다.

### <a name="unrelated-tables-only"></a>관련이 없는 테이블만

자동 명령 생성 논리는 데이터 소스에 있는 다른 테이블과의 관계를 고려하지 않고 독립 실행형 테이블에 대해 INSERT, UPDATE 또는 DELETE 문을 생성합니다. 결과적으로 데이터베이스에서 외래 키 제약 조건에 참여하는 열에 대한 변경 내용을 전송하기 위해 `Update`를 호출하면 오류가 발생할 수 있습니다. 이 예외가 발생하지 않도록 하려면 외래 키 제약 조건에 관련된 열을 업데이트하는 데 <xref:System.Data.Common.DbCommandBuilder>를 사용하는 대신 해당 작업을 수행하는 데 사용되는 문을 명시적으로 지정합니다.

### <a name="table-and-column-names"></a>테이블 이름 및 열 이름

열 이름이나 테이블 이름에 공백, 마침표, 인용 부호 및 기타 영숫자가 아닌 문자 등의 특수 문자가 있으면 이러한 문자가 대괄호로 구분되어 있더라도 자동 명령 생성 논리가 실패할 수 있습니다. 공급자에 따라서는 QuotePrefix 및 QuoteSuffix 매개 변수를 설정함으로써 생성 논리에서 공백이 허용되도록 할 수 있지만 특수 문자를 이스케이프할 수는 없습니다. *catalog.schema.table* 형식의 정규화된 테이블 이름이 지원됩니다.

## <a name="using-the-commandbuilder-to-automatically-generate-an-sql-statement"></a>CommandBuilder를 사용하여 SQL 문 자동 생성

`DataAdapter`에 대한 SQL 문을 자동으로 생성하려면 먼저 `SelectCommand`의 `DataAdapter` 속성을 설정한 다음 `CommandBuilder` 개체를 만들고 `DataAdapter`에서 SQL 문을 자동으로 생성할 `CommandBuilder`를 인수로 지정합니다.

[!code-csharp[SqlCommandBuilder_Create#1](~/../sqlclient/doc/samples/SqlCommandBuilder_Create.cs#1)]

## <a name="modifying-the-selectcommand"></a>SelectCommand 수정

INSERT, UPDATE 또는 DELETE 명령이 자동으로 생성된 후에 `CommandText`의 `SelectCommand` 수정하면 예외가 발생할 수 있습니다. 수정된 `SelectCommand.CommandText`에 Insert, Update 또는 Delete 명령이 자동으로 생성되었을 때 사용한 `SelectCommand.CommandText`와 일치하지 않는 스키마 정보가 들어 있으면 이후 `DataAdapter.Update` 메서드를 호출할 때 `SelectCommand`가 참조하는 현재 테이블에 더 이상 없는 열에 액세스하려고 할 수 있으므로 예외가 throw됩니다.

`CommandBuilder`의 `RefreshSchema` 메서드를 호출함으로써 `CommandBuilder`에서 사용하는 스키마 정보를 새로 고쳐 명령을 자동으로 생성할 수 있습니다.

자동으로 생성되는 명령이 어떤 것인지 확인하려는 경우 `GetInsertCommand` 개체의 `GetUpdateCommand`, `GetDeleteCommand` 및 `CommandBuilder` 메서드를 사용하고 관련 명령의 `CommandText` 속성을 확인하여 자동으로 생성된 명령에 대한 참조를 얻을 수 있습니다.

다음 코드 예제에서는 자동 생성된 UPDATE 명령을 콘솔에 씁니다.

[!code-csharp[SqlCommandBuilder_Create#2](~/../sqlclient/doc/samples/SqlCommandBuilder_Create.cs#2)]

다음 예제에서는 데이터 세트에 테이블을 다시 만듭니다. 자동 생성된 명령을 이 새 열 정보로 새로 고치도록 **RefreshSchema** 메서드가 호출됩니다.

[!code-csharp[SqlCommandBuilder_Create#3](~/../sqlclient/doc/samples/SqlCommandBuilder_Create.cs#3)]

## <a name="see-also"></a>참조

- [명령 및 매개 변수](commands-parameters.md)
- [명령 실행](execute-command.md)
