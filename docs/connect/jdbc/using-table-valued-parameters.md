---
title: 테이블 반환 매개 변수 사용
description: 테이블 반환 매개 변수는 매개 변수가 있는 단일 명령으로 클라이언트에서 SQL Server로 여러 데이터 행을 전송하는 효율적인 방법을 제공합니다.
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 698cf6e4e44210ea5f4575d4021514c07fe4255d
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81631943"
---
# <a name="using-table-valued-parameters"></a>테이블 반환 매개 변수 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

테이블 반환 매개 변수를 사용하면 데이터를 처리하는 데 여러 번 왕복하거나 서버 측 특수 논리를 설정하지 않고도 데이터의 여러 행을 클라이언트 애플리케이션에서 SQL Server로 쉽게 마샬링할 수 있습니다. 또한 테이블 반환 매개 변수를 사용하면 클라이언트 애플리케이션에서 데이터 행을 캡슐화하고 매개 변수가 있는 단일 명령으로 데이터를 서버에 보낼 수 있습니다. 들어오는 데이터 행을 테이블 변수에 저장한 다음 Transact-SQL을 사용하여 연산할 수 있습니다.  
  
테이블 반환 매개 변수의 열 값은 표준 Transact-SQL SELECT 문을 사용하여 액세스할 수 있습니다. 테이블 반환 매개 변수는 강력한 형식이며 해당 구조체의 유효성 검사가 자동으로 수행됩니다. 테이블 반환 매개 변수의 크기는 서버 메모리에 의해서만 제한됩니다.  
  
> [!NOTE]  
> Microsoft JDBC Driver 6.0 for SQL Server부터 테이블 반환 매개 변수에 대한 지원이 제공됩니다.
>
> 테이블 반환 매개 변수에는 데이터를 반환할 수 없습니다. 테이블 반환 매개 변수는 입력 전용입니다. OUTPUT 키워드는 지원되지 않습니다.  
  
 테이블 반환 매개 변수에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
| 리소스                                                                                                             | Description                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [테이블 반환 매개 변수(데이터베이스 엔진)](https://go.microsoft.com/fwlink/?LinkId=98363)(SQL Server 온라인 설명서) | 테이블 반환 매개 변수를 만들고 사용하는 방법을 설명합니다.                             |
| SQL Server 온라인 설명서의 [사용자 정의 테이블 형식](https://go.microsoft.com/fwlink/?LinkId=98364)                  | 테이블 반환 매개 변수를 선언하는 데 사용되는 사용자 정의 테이블 형식에 대해 설명합니다. |
| CodePlex의 [Microsoft SQL Server 데이터베이스 엔진](https://go.microsoft.com/fwlink/?LinkId=120507) 섹션        | SQL Server의 특성과 기능을 사용하는 방법을 보여 주는 샘플을 포함합니다.  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>이전 버전의 SQL Server에서 여러 행 전달  

SQL Server 2008에 테이블 반환 매개 변수가 도입되기 전에는 여러 행의 데이터를 저장 프로시저나 매개 변수화된 SQL 명령에 전달하는 옵션이 제한적이었습니다. 개발자는 서버에 여러 행을 전달하기 위해 다음 옵션 중에서 선택할 수 있습니다.  
  
- 일련의 개별 매개 변수를 사용하여 여러 열과 데이터 행의 값을 나타냅니다. 이 방법을 사용하여 전달할 수 있는 데이터의 양은 허용되는 매개 변수의 개수에 의해 제한됩니다. SQL Server 프로시저에는 매개 변수를 2100개까지 사용할 수 있습니다. 이러한 개별 값을 테이블 변수 또는 처리를 위한 임시 테이블로 조합하는 데 서버 쪽 논리가 필요합니다.  
  
- 여러 데이터 값을 구분된 문자열 또는 XML 문서로 번들로 묶은 다음 해당 텍스트 값을 프로시저 또는 문에 전달합니다. 이렇게 하려면 프로시저 또는 문이 데이터 구조의 유효성을 검사하고 값을 번들에서 해제하는 데 필요한 논리를 포함해야 합니다.  
  
- 여러 행에 영향을 주는 데이터 수정을 위한 일련의 개별 SQL 문을 만듭니다. 변경 내용을 개별적으로 서버에 제출하거나 그룹으로 일괄 처리할 수 있습니다. 그러나 여러 문이 포함된 일괄 처리로 전송된 경우에도 각 문은 서버에서 개별적으로 실행됩니다.  
  
- bcp 유틸리티 프로그램 또는 [SQLServerBulkCopy](using-bulk-copy-with-the-jdbc-driver.md)를 사용하여 많은 데이터 행을 테이블에 로드할 수 있습니다. 이 기법은 매우 효율적이지만 데이터를 임시 테이블 또는 테이블 변수에 로드하지 않는 한 서버 쪽 처리를 지원하지 않습니다.
  
## <a name="creating-table-valued-parameter-types"></a>테이블 반환 매개 변수 형식 만들기  

테이블 반환 매개 변수는 Transact-SQL `CREATE TYPE` 문을 사용하여 정의된 강력한 형식의 테이블 구조를 기반으로 합니다. 클라이언트 애플리케이션에서 테이블 반환 매개 변수를 사용할 수 있으려면 먼저 SQL Server에서 테이블 형식을 만들고 구조를 정의해야 합니다. 테이블 형식 만들기에 대한 자세한 내용은 SQL Server 온라인 설명서에서 [사용자 정의 테이블 형식](https://go.microsoft.com/fwlink/?LinkID=98364)을 참조하세요.  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

테이블 형식을 만든 후에는 해당 형식을 기반으로 테이블 반환 매개 변수를 선언할 수 있습니다. 다음 Transact-SQL 조각은 저장 프로시저 정의에 테이블 반환 매개 변수를 선언하는 방법을 보여 줍니다. 테이블 반환 매개 변수를 선언하려면 `READONLY` 키워드가 필요합니다.  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>테이블 반환 매개 변수를 사용하여 데이터 수정(Transact-SQL)  

단일 문을 실행하여 여러 행에 영향을 주는 집합 기반 데이터 수정에 테이블 반환 매개 변수를 사용할 수 있습니다. 예를 들어 테이블 반환 매개 변수에서 모든 행을 선택하여 데이터베이스 테이블에 삽입하거나 테이블 반환 매개 변수를 업데이트하려는 테이블에 조인하여 update 문을 만들 수 있습니다.  
  
다음 Transact-SQL UPDATE 문은 테이블 반환 매개 변수를 Categories 테이블에 조인하여 사용하는 방법을 보여 줍니다. FROM 절에서 JOIN과 함께 테이블 반환 매개 변수를 사용하는 경우 별칭을 지정해야 합니다. 여기서는 테이블 반환 매개 변수에 대한 별칭을 "ec"로 지정했습니다.  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

이 Transact-SQL 예제에서는 테이블 반환 매개 변수에서 행을 선택하여 단일 집합 기반 작업으로 INSERT를 수행하는 방법을 보여 줍니다.

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>테이블 반환 매개 변수의 제한 사항

테이블 반환 매개 변수에는 다음과 같은 몇 가지 제한 사항이 있습니다.  
  
- 사용자 정의 함수에는 테이블 반환 매개 변수를 전달할 수 없습니다.  
  
- 테이블 반환 매개 변수는 UNIQUE 또는 PRIMARY KEY 제약 조건을 지원하기 위해서만 인덱싱할 수 있습니다. SQL Server는 테이블 반환 매개 변수에 대한 통계를 유지 관리하지 않습니다.  
  
- 테이블 반환 매개 변수는 Transact-SQL 코드에서 읽기 전용입니다. 테이블 반환 매개 변수 행의 열 값은 업데이트할 수 없으며 행을 삽입하거나 삭제할 수 없습니다. 테이블 반환 매개 변수에서 저장 프로시저 또는 매개 변수화된 문에 전달되는 데이터를 수정하려면 데이터를 임시 테이블 또는 테이블 변수에 삽입해야 합니다.  
  
- ALTER TABLE 문을 사용하여 테이블 반환 매개 변수의 디자인을 수정할 수 없습니다.

- 많은 개체를 테이블 반환 매개 변수로 스트리밍할 수 있습니다.  
  
## <a name="configuring-a-table-valued-parameter"></a>테이블 반환 매개 변수 구성

Microsoft JDBC Driver 6.0 for SQL Server부터 테이블 반환 매개 변수는 매개 변수가 있는 문 또는 매개 변수가 있는 저장 프로시저에서 지원됩니다. 테이블 반환 매개 변수는 SQLServerDataTable, ResultSet, 또는 ISQLServerDataRecord 인터페이스의 사용자 제공 구현에서 채워질 수 있습니다. 준비된 쿼리에 대한 테이블 반환 매개 변수를 설정할 때는 이전에 서버에서 만든 호환 가능한 형식의 이름과 일치해야 하는 형식 이름을 지정해야 합니다.  
  
다음 두 코드 조각에서는 SQLServerPreparedStatement 및 SQLServerCallableStatement로 테이블 반환 매개 변수를 구성하여 데이터를 삽입하는 방법을 보여 줍니다. 여기서 sourceTVPObject는 SQLServerDataTable, 또는 ResultSet 또는 ISQLServerDataRecord 개체일 수 있습니다. 이 예제에서는 연결이 활성 연결 개체라고 가정합니다.  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement("INSERT INTO dbo.Categories SELECT * FROM ?");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```

```java
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```

> [!NOTE]  
> 테이블 반환 매개 변수를 설정하는 데 사용할 수 있는 API의 전체 목록은 아래의 **JDBC 드라이버용 테이블 반환 매개 변수 API** 섹션을 참조하세요.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>테이블 반환 매개 변수를 SQLServerDataTable 개체로 전달  

Microsoft JDBC Driver 6.0 for SQL Server부터 SQLServerDataTable 클래스는 관계형 데이터의 메모리 내 테이블을 나타냅니다. 이 예제에서는 SQLServerDataTable 개체를 사용하여 메모리 내 데이터에서 테이블 반환 매개 변수를 생성하는 방법을 보여 줍니다. 이 코드는 먼저 SQLServerDataTable 개체를 만들고 해당 스키마를 정의한 다음, 테이블에 데이터를 채웁니다. 그런 다음 이 데이터 테이블을 테이블 반환 매개 변수로 SQL Server로 전달하도록 SQLServerPreparedStatement를 구성합니다.  

```java
/* Assumes connection is an active Connection object. */

// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");
sourceDataTable.addRow(2, "CategoryNameValue2");
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```

> [!NOTE]  
> 테이블 반환 매개 변수를 설정하는 데 사용할 수 있는 API의 전체 목록은 아래의 **JDBC 드라이버용 테이블 반환 매개 변수 API** 섹션을 참조하세요.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>테이블 반환 매개 변수를 ResultSet 개체로 전달  

이 예제에서는 ResultSet의 데이터 행을 테이블 반환 매개 변수로 스트림하는 방법을 보여 줍니다. 이 코드는 먼저 SQLServerDataTable 개체의 원본 테이블에서 데이터를 검색하고 해당 스키마를 정의한 다음, 테이블에 데이터를 채웁니다. 그런 다음 이 데이터 테이블을 테이블 반환 매개 변수로 SQL Server로 전달하도록 SQLServerPreparedStatement를 구성합니다.  

```java
/* Assumes connection is an active Connection object. */

// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  

// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```

> [!NOTE]  
> 테이블 반환 매개 변수를 설정하는 데 사용할 수 있는 API의 전체 목록은 아래의 **JDBC 드라이버용 테이블 반환 매개 변수 API** 섹션을 참조하세요.  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>테이블 반환 매개 변수를 ISQLServerDataRecord 개체로 전달  

Microsoft JDBC Driver 6.0 for SQL Server부터 테이블 반환 매개 변수를 사용하여 사용자가 제공하는 구현 방법에 따라 새 인터페이스 ISQLServerDataRecord를 스트리밍 데이터에 사용할 수 있습니다. 다음 예제에서는 ISQLServerDataRecord 인터페이스를 구현하는 방법과 이 인터페이스를 테이블 반환 매개 변수로 전달하는 방법을 보여 줍니다. 간단한 설명을 위해 다음 예제에서는 하드 코딩된 값을 가진 행을 테이블 반환 매개 변수에 한 개만 전달합니다. 사용자는 모든 원본(예: 텍스트 파일)에서 행을 스트림하도록 이 인터페이스를 구현하는 것이 가장 좋습니다.  

```java
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }
}

// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```

> [!NOTE]  
> 테이블 반환 매개 변수를 설정하는 데 사용할 수 있는 API의 전체 목록은 아래의 **JDBC 드라이버용 테이블 반환 매개 변수 API** 섹션을 참조하세요.

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC 드라이버용 테이블 반환 매개 변수 API

### <a name="sqlservermetadata"></a>SQLServerMetaData

이 클래스는 열에 대한 메타데이터를 나타냅니다. ISQLServerDataRecord 인터페이스에서 열 메타데이터를 테이블 반환 매개 변수로 전달하는 데 사용됩니다. 이 클래스의 메서드는 다음과 같습니다.  

| 속성                                                                                                                                                                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData(String columnName, int sqlType, int precision, int scale, boolean useServerDefault, boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | 지정한 열 이름, sql 형식, 전체 자릿수, 소수 자릿수 및 서버 기본값을 사용하여 SQLServerMetaData의 새 인스턴스를 초기화합니다. 이 형식의 생성자는 테이블 반환 매개 변수에서 열이 고유한지 여부, 열의 정렬 순서 및 정렬 열의 서수를 지정할 수 있도록 하여 테이블 반환 매개 변수를 지원합니다. <br/><br/>useServerDefault - 이 열에서 기본 서버 값을 사용해야 하는지 여부를 지정합니다. 기본값은 false입니다.<br>isUniqueKey - 테이블 반환 매개 변수의 열이 고유한 열인지 여부를 나타냅니다. 기본값은 false입니다.<br>sortOrder - 열의 정렬 순서를 나타냅니다. 기본값은 SQLServerSortOrder.Unspecified입니다.<br>sortOrdinal - 정렬 열의 서수를 지정합니다. sortOrdinal은 0부터 시작합니다. 기본값은 -1입니다. |
| public SQLServerMetaData( String columnName, int sqlType)                                                                                                                        | 열 이름과 sql 형식을 사용하여 SQLServerMetaData의 새 인스턴스를 초기화합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData( String columnName, int sqlType, int length)                                                                                                                        | 열 이름, sql 형식 및 길이(문자열 데이터의 경우)를 사용하여 SQLServerMetaData의 새 인스턴스를 초기화합니다. 길이는 4,000자 미만 문자열에서 긴 문자열을 구분하는 데 사용됩니다. JDBC 드라이버 버전 7.2에서 도입되었습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData( String columnName, int sqlType, int precision, int scale)                                                                                              | 열 이름, sql 형식, 전체 자릿수 및 소수 자릿수를 사용하여 SQLServerMetaData의 새 인스턴스를 초기화합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | 다른 SQLServerMetaData 개체에서 SQLServerMetaData의 새 인스턴스를 초기화합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | 열 이름을 검색합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | Java sql 형식을 검색합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision()                                                                                                                                                        | 열에 전달된 형식의 전체 자릿수를 검색합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | 열에 전달된 형식의 소수 자릿수를 검색합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | 정렬 순서를 검색합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | 정렬 서수를 검색합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | 열이 고유한지 여부를 반환합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | 열이 기본 서버 값을 사용하는지 여부를 반환합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

정렬 순서를 정의하는 열거형입니다. 가능한 값은 오름차순, 내림차순 및 지정되지 않음입니다.
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

이 클래스는 테이블 반환 매개 변수와 함께 사용되는 메모리 내 데이터 테이블을 나타냅니다. 이 클래스의 메서드는 다음과 같습니다.  

| 속성                                                          | Description                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | SQLServerDataTable의 새 인스턴스를 초기화합니다.    |
| public Iterator<Entry\<Integer, Object[]>> getIterator()      | 데이터 테이블의 행에 대한 반복기를 검색합니다. |
| public void addColumnMetadata(String columnName, int sqlType) | 지정한 열의 메타데이터를 추가합니다.              |
| public void addColumnMetadata(SQLServerDataColumn column)     | 지정한 열의 메타데이터를 추가합니다.              |
| public void addRow(Object... values)                          | 데이터 테이블에 데이터 행 하나를 추가합니다.              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | 이 데이터 테이블의 열 메타데이터를 검색합니다.       |
| public void clear()                                           | 이 데이터 테이블을 지웁니다.                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

이 클래스는 SQLServerDataTable로 표시되는 메모리 내 데이터 테이블의 열을 나타냅니다. 이 클래스의 메서드는 다음과 같습니다.  

| 속성                                                       | Description                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn(String columnName, int sqlType) | 열 이름 및 형식을 사용하여 SQLServerDataColumn의 새 인스턴스를 초기화합니다. |
| public String getColumnName()                              | 열 이름을 검색합니다.                                                       |
| public int getColumnType()                                 | 열 형식을 검색합니다.                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

이 클래스는 사용자가 테이블 반환 매개 변수로 데이터를 스트림하기 위해 구현할 수 있는 인터페이스를 나타냅니다. 이 인터페이스의 메서드는 다음과 같습니다.  
  
| 속성                                                    | Description                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | 지정된 열 인덱스의 열 메타데이터를 검색합니다.                                               |
| public int getColumnCount();                            | 총 열 수를 검색합니다.                                                                  |
| public Object[] getRowData();                           | 현재 행에 대한 데이터를 개체의 배열로 검색합니다.                                          |
| public boolean next();                                  | 다음 행으로 이동합니다. 이동이 성공하고 다음 행이 있으면 true를 반환하고, 그렇지 않으면 false를 반환합니다. |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

테이블 반환 매개 변수 전달을 지원하기 위해 이 클래스에 다음 메서드가 추가되었습니다.  

| 속성                                                                                                    | Description                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | 데이터 테이블에 테이블 반환 매개 변수를 채웁니다. parameterIndex는 매개 변수 인덱스이고, tvpName은 테이블 반환 매개 변수의 이름이고, tvpDataTable은 원본 데이터 테이블 개체입니다.                                                                                                          |
| public final void setStructured(int parameterIndex, String tvpName, ResultSet tvpResultSet)             | 테이블 반환 매개 변수에 다른 테이블에서 검색된 ResultSet를 채웁니다. parameterIndex는 매개 변수 인덱스이고, tvpName은 테이블 반환 매개 변수의 이름이고, tvpResultSet는 원본 결과 집합 개체입니다.                                                                               |
| public final void setStructured(int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | ISQLServerDataRecord 개체를 테이블 반환 매개 변수에 채웁니다. ISQLServerDataRecord는 스트리밍 데이터에 사용되며 사용자가 이를 사용하는 방법을 결정합니다. parameterIndex는 매개 변수 인덱스이고, tvpName은 테이블 반환 매개 변수의 이름이고, tvpDataRecord는 ISQLServerDataRecord 개체입니다. |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

테이블 반환 매개 변수 전달을 지원하기 위해 이 클래스에 다음 메서드가 추가되었습니다.  
  
| 속성                                                                                                        | Description                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | 저장 프로시저에 전달된 테이블 반환 매개 변수에 데이터 테이블을 채웁니다. paratemeterName은 매개 변수의 이름이고, tvpName은 TVP 형식의 이름이고, tvpDataTable은 데이터 테이블 개체입니다.                                                                                                                 |
| public final void setStructured(String paratemeterName, String tvpName, ResultSet tvpResultSet)             | 저장 프로시저에 전달된 테이블 반환 매개 변수에 다른 테이블에서 검색된 ResultSet를 채웁니다. paratemeterName은 매개 변수의 이름이고, tvpName은 TVP 형식의 이름이고, tvpResultSet은 원본 결과 집합 개체입니다.                                                                              |
| public final void setStructured(String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | 저장 프로시저에 전달된 테이블 반환 매개 변수에 ISQLServerDataRecord 개체를 채웁니다. ISQLServerDataRecord는 스트리밍 데이터에 사용되며 사용자가 이를 사용하는 방법을 결정합니다. paratemeterName은 매개 변수의 이름이고, tvpName은 TVP 형식의 이름이고, tvpDataRecord는 ISQLServerDataRecord 개체입니다. |

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 개요](overview-of-the-jdbc-driver.md)  
