---
title: 테이블 반환 매개 변수 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98863afb5a47eddfd311563bd03a1c7c7120b161
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025713"
---
# <a name="using-table-valued-parameters"></a>테이블 반환 매개 변수 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

테이블 반환 매개 변수를 사용하면 데이터를 처리하는 데 여러 번 왕복하거나 서버 측 특수 논리를 설정하지 않고도 데이터의 여러 행을 클라이언트 애플리케이션에서 SQL Server로 쉽게 마샬링할 수 있습니다. 또한 테이블 반환 매개 변수를 사용하면 클라이언트 애플리케이션에서 데이터 행을 캡슐화하고 매개 변수가 있는 단일 명령으로 데이터를 서버에 보낼 수 있습니다. 들어오는 데이터 행을 테이블 변수에 저장한 다음 Transact-SQL을 사용하여 연산할 수 있습니다.  
  
테이블 반환 매개 변수의 열 값은 표준 Transact-sql SELECT 문을 사용 하 여 액세스할 수 있습니다. 테이블 반환 매개 변수는 강력한 형식이 며 해당 구조체의 유효성을 자동으로 검사 합니다. 테이블 반환 매개 변수의 크기는 서버 메모리에 의해서만 제한 됩니다.  
  
> [!NOTE]  
> SQL Server 용 Microsoft JDBC Driver 6.0부터 테이블 반환 매개 변수에 대 한 지원이 제공 됩니다.
>
> 테이블 반환 매개 변수에는 데이터를 반환할 수 없습니다. 테이블 반환 매개 변수는 입력 전용입니다. OUTPUT 키워드는 지원 되지 않습니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 다음 리소스를 참조 하세요.  
  
| 리소스                                                                                                             | 설명                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| SQL Server 온라인 설명서의 [테이블 반환 매개 변수 (데이터베이스 엔진)](https://go.microsoft.com/fwlink/?LinkId=98363) | 테이블 반환 매개 변수를 만들고 사용 하는 방법을 설명 합니다.                             |
| SQL Server 온라인 설명서의 [사용자 정의 테이블 형식](https://go.microsoft.com/fwlink/?LinkId=98364)                  | 테이블 반환 매개 변수를 선언 하는 데 사용 되는 사용자 정의 테이블 형식에 대해 설명 합니다. |
| CodePlex의 [Microsoft SQL Server 데이터베이스 엔진](https://go.microsoft.com/fwlink/?LinkId=120507) 섹션        | SQL Server 기능 및 기능을 사용 하는 방법을 보여 주는 샘플이 포함 되어 있습니다.  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>이전 버전의 SQL Server에서 여러 행 전달  

SQL Server 2008에 대 한 테이블 반환 매개 변수가 도입 되기 전에는 여러 행의 데이터를 저장 프로시저나 매개 변수화 된 SQL 명령에 전달 하는 옵션이 제한 되었습니다. 개발자는 서버에 여러 행을 전달 하기 위해 다음 옵션 중에서 선택할 수 있습니다.  
  
- 일련의 개별 매개 변수를 사용 하 여 여러 열과 데이터 행의 값을 나타냅니다. 이 메서드를 사용 하 여 전달할 수 있는 데이터의 양은 허용 되는 매개 변수 수에 의해 제한 됩니다. SQL Server 프로시저에는 최대 2100 개의 매개 변수가 있을 수 있습니다. 서버 쪽 논리는 이러한 개별 값을 테이블 변수나 처리를 위한 임시 테이블로 조합 하는 데 필요 합니다.  
  
- 여러 데이터 값을 구분 된 문자열 또는 XML 문서로 묶음 한 다음 해당 텍스트 값을 프로시저 또는 문에 전달 합니다. 이렇게 하려면 프로시저 또는 문이 데이터 구조의 유효성을 검사 하 고 값을 제거 하는 데 필요한 논리를 포함 해야 합니다.  
  
- 여러 행에 영향을 주는 데이터 수정을 위한 일련의 개별 SQL 문을 만듭니다. 변경 내용을 개별적으로 서버에 제출 하거나 그룹으로 일괄 처리할 수 있습니다. 그러나 여러 문이 포함 된 일괄 처리로 전송 된 경우에도 각 문은 서버에서 개별적으로 실행 됩니다.  
  
- Bcp 유틸리티 프로그램이 나 [SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx) 개체를 사용 하 여 여러 행의 데이터를 테이블에 로드할 수 있습니다. 이 기법은 매우 효율적 이지만 데이터를 임시 테이블 또는 테이블 변수에 로드 하지 않는 한 서버 쪽 처리를 지원 하지 않습니다.  
  
## <a name="creating-table-valued-parameter-types"></a>테이블 반환 매개 변수 형식 만들기  

테이블 반환 매개 변수는 transact-sql `CREATE TYPE` 문을 사용 하 여 정의 된 강력한 형식의 테이블 구조를 기반으로 합니다. 클라이언트 응용 프로그램에서 테이블 반환 매개 변수를 사용 하려면 먼저 테이블 형식을 만들고 SQL Server 구조를 정의 해야 합니다. 테이블 형식을 만드는 방법에 대 한 자세한 내용은 SQL Server 온라인 설명서에서 [사용자 정의 테이블 형식](https://go.microsoft.com/fwlink/?LinkID=98364) 을 참조 하세요.  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

테이블 형식을 만든 후에는 해당 형식을 기반으로 테이블 반환 매개 변수를 선언할 수 있습니다. 다음 Transact-sql 조각은 저장 프로시저 정의에서 테이블 반환 매개 변수를 선언 하는 방법을 보여 줍니다. 테이블 반환 매개 `READONLY` 변수를 선언 하려면 키워드가 필요 합니다.  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>테이블 반환 매개 변수를 사용 하 여 데이터 수정 (Transact-sql)  

단일 문을 실행 하 여 여러 행에 영향을 주는 집합 기반 데이터 수정에 테이블 반환 매개 변수를 사용할 수 있습니다. 예를 들어 테이블 반환 매개 변수에서 모든 행을 선택 하 여 데이터베이스 테이블에 삽입 하거나 테이블 반환 매개 변수를 업데이트 하려는 테이블에 조인 하 여 update 문을 만들 수 있습니다.  
  
다음 Transact-sql UPDATE 문은 테이블 반환 매개 변수를 Categories 테이블에 조인 하 여 사용 하는 방법을 보여 줍니다. FROM 절에서 JOIN과 함께 테이블 반환 매개 변수를 사용 하는 경우 테이블 반환 매개 변수를 "ec"로 별칭으로 지정 하는 여기에 표시 된 대로 별칭을 지정 해야 합니다.  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

이 Transact-sql 예제에서는 테이블 반환 매개 변수에서 행을 선택 하 여 단일 집합 기반 작업에서 삽입을 수행 하는 방법을 보여 줍니다.

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>테이블 반환 매개 변수의 제한 사항

테이블 반환 매개 변수에는 다음과 같은 몇 가지 제한 사항이 있습니다.  
  
- 사용자 정의 함수에는 테이블 반환 매개 변수를 전달할 수 없습니다.  
  
- 테이블 반환 매개 변수는 UNIQUE 또는 PRIMARY KEY 제약 조건을 지원 하기 위해서만 인덱싱할 수 있습니다. SQL Server는 테이블 반환 매개 변수에 대한 통계를 유지 관리하지 않습니다.  
  
- 테이블 반환 매개 변수는 Transact-sql 코드에서 읽기 전용입니다. 테이블 반환 매개 변수 행의 열 값은 업데이트할 수 없으며 행을 삽입 하거나 삭제할 수 없습니다. 테이블 반환 매개 변수에서 저장 프로시저 또는 매개 변수화 된 문에 전달 되는 데이터를 수정 하려면 데이터를 임시 테이블 또는 테이블 변수에 삽입 해야 합니다.  
  
- ALTER TABLE 문을 사용 하 여 테이블 반환 매개 변수의 디자인을 수정할 수 없습니다.

- 많은 개체를 테이블 반환 매개 변수로 스트리밍할 수 있습니다.  
  
## <a name="configuring-a-table-valued-parameter"></a>테이블 반환 매개 변수 구성

SQL Server에 대 한 Microsoft JDBC Driver 6.0부터 테이블 반환 매개 변수는 매개 변수가 있는 문이나 매개 변수가 있는 저장 프로시저에서 지원 됩니다. 테이블 반환 매개 변수는 SQLServerDataTable, ResultSet 또는 ISQLServerDataRecord 인터페이스의 사용자 제공 구현에서 채워질 수 있습니다. 준비 된 쿼리에 대 한 테이블 반환 매개 변수를 설정할 때는 이전에 서버에서 만든 호환 가능한 형식의 이름과 일치 해야 하는 형식 이름을 지정 해야 합니다.  
  
다음 두 코드 조각에서는 SQLServerPreparedStatement 및 SQLServerCallableStatement를 사용 하 여 테이블 반환 매개 변수를 구성 하 여 데이터를 삽입 하는 방법을 보여 줍니다. 여기서 sourceTVPObject는 SQLServerDataTable 또는 ResultSet 또는 ISQLServerDataRecord 개체 일 수 있습니다. 이 예에서는 연결이 활성 연결 개체 라고 가정 합니다.  

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
> 테이블 반환 매개 변수를 설정 하는 데 사용할 수 있는 Api의 전체 목록은 아래의 **JDBC 드라이버에 대 한 테이블 반환 매개 변수 API** 섹션을 참조 하세요.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>테이블 반환 매개 변수를 SQLServerDataTable 개체로 전달  

SQL Server에 대 한 Microsoft JDBC Driver 6.0부터 SQLServerDataTable 클래스는 관계형 데이터의 메모리 내 테이블을 나타냅니다. 이 예에서는 SQLServerDataTable 개체를 사용 하 여 메모리 내 데이터에서 테이블 반환 매개 변수를 생성 하는 방법을 보여 줍니다. 이 코드는 먼저 SQLServerDataTable 개체를 만들고, 해당 스키마를 정의 하 고, 테이블을 데이터로 채웁니다. 그런 다음이 데이터 테이블을 SQL Server에 대 한 테이블 반환 매개 변수로 전달 하는 SQLServerPreparedStatement를 구성 합니다.  

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
> 테이블 반환 매개 변수를 설정 하는 데 사용할 수 있는 Api의 전체 목록은 아래의 **JDBC 드라이버에 대 한 테이블 반환 매개 변수 API** 섹션을 참조 하세요.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>테이블 반환 매개 변수를 ResultSet 개체로 전달  

이 예에서는 결과 집합의 데이터 행을 테이블 반환 매개 변수로 스트리밍하는 방법을 보여 줍니다. 코드는 먼저의 원본 테이블에서 데이터를 검색 하 고, SQLServerDataTable 개체를 만들고, 해당 스키마를 정의 하 고, 테이블을 데이터로 채웁니다. 그런 다음이 데이터 테이블을 SQL Server에 대 한 테이블 반환 매개 변수로 전달 하는 SQLServerPreparedStatement를 구성 합니다.  

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
> 테이블 반환 매개 변수를 설정 하는 데 사용할 수 있는 Api의 전체 목록은 아래의 **JDBC 드라이버에 대 한 테이블 반환 매개 변수 API** 섹션을 참조 하세요.  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>테이블 반환 매개 변수를 ISQLServerDataRecord 개체로 전달  

SQL Server에 대 한 Microsoft JDBC Driver 6.0부터, 테이블 반환 매개 변수를 사용 하 여 사용자가이에 대 한 구현을 제공 하는 방법에 따라 새 인터페이스 ISQLServerDataRecord을 스트리밍 데이터에 사용할 수 있습니다. 다음 예제에서는 ISQLServerDataRecord 인터페이스를 구현 하는 방법과이 인터페이스를 테이블 반환 매개 변수로 전달 하는 방법을 보여 줍니다. 편의상 다음 예에서는 하드 코딩 된 값을 가진 행을 테이블 반환 매개 변수에 한 개만 전달 합니다. 사용자는 텍스트 파일 등의 모든 원본에서 행을 스트림 하기 위해이 인터페이스를 구현 하는 것이 가장 좋습니다.  

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
> 테이블 반환 매개 변수를 설정 하는 데 사용할 수 있는 Api의 전체 목록은 아래의 **JDBC 드라이버에 대 한 테이블 반환 매개 변수 API** 섹션을 참조 하세요.

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC 드라이버에 대 한 테이블 반환 매개 변수 API

### <a name="sqlservermetadata"></a>SQLServerMetaData

이 클래스는 열에 대 한 메타 데이터를 나타냅니다. ISQLServerDataRecord 인터페이스에서 열 메타 데이터를 테이블 반환 매개 변수로 전달 하는 데 사용 됩니다. 이 클래스의 메서드는 다음과 같습니다.  

| 속성                                                                                                                                                                             | 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData (문자열 columnName, int sqlType, int precision, int scale, boolean useServerDefault, boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | 지정한 열 이름, sql 유형, 전체 자릿수, 소수 자릿수 및 서버 기본값을 사용 하 여 SQLServerMetaData의 새 인스턴스를 초기화 합니다. 이 형식의 생성자는 테이블 반환 매개 변수에서 열이 고유한 지 여부, 열의 정렬 순서 및 정렬 열의 서 수를 지정할 수 있도록 하 여 테이블 반환 매개 변수를 지원 합니다. <br/><br/>useServerDefault-이 열에서 기본 서버 값을 사용 해야 하는지 여부를 지정 합니다. 기본값은 false입니다.<br>isUniqueKey-테이블 반환 매개 변수의 열이 고유한 열 인지 여부를 나타냅니다. 기본값은 false입니다.<br>sortOrder-열에 대 한 정렬 순서를 나타냅니다. 기본값은 SQLServerSortOrder입니다.<br>sortOrdinal-정렬 열의 서 수를 지정 합니다. sortOrdinal은 0부터 시작 합니다. 기본값은-1입니다. |
| public SQLServerMetaData (문자열 columnName, int sqlType)                                                                                                                        | 열 이름과 sql 유형을 사용 하 여 SQLServerMetaData의 새 인스턴스를 초기화 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData (문자열 columnName, int sqlType, int length)                                                                                                                        | 열 이름, sql 형식 및 길이 (문자열 데이터의 경우)를 사용 하 여 SQLServerMetaData의 새 인스턴스를 초기화 합니다. 길이는 4000 자 미만의 문자열에서 긴 문자열을 구분 하는 데 사용 됩니다. JDBC 드라이버 버전 7.2에서 도입 되었습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData (문자열 columnName, int sqlType, int precision, int scale)                                                                                              | 열 이름, sql 형식, 전체 자릿수 및 소수 자릿수를 사용 하 여 SQLServerMetaData의 새 인스턴스를 초기화 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | 다른 SQLServerMetaData 개체에서 SQLServerMetaData의 새 인스턴스를 초기화 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | 열 이름을 검색 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | Java sql 형식을 검색 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision()                                                                                                                                                        | 열에 전달 된 형식의 전체 자릿수를 검색 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | 열에 전달 된 형식의 소수 자릿수를 검색 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | 정렬 순서를 검색 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | 정렬 서 수를 검색 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | 열이 고유한 지 여부를 반환 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | 열이 기본 서버 값을 사용 하는지 여부를 반환 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

정렬 순서를 정의 하는 열거형입니다. 가능한 값은 오름차순, 내림차순 및 지정 되지 않음입니다.
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

이 클래스는 테이블 반환 매개 변수와 함께 사용 되는 메모리 내 데이터 테이블을 나타냅니다. 이 클래스의 메서드는 다음과 같습니다.  

| 속성                                                          | 설명                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | SQLServerDataTable의 새 인스턴스를 초기화 합니다.    |
| 공용 반복기 < 항목\<정수, Object [] > > getiterator ()      | 데이터 테이블의 행에 대 한 반복기를 검색 합니다. |
| public void addColumnMetadata(String columnName, int sqlType) | 지정 된 열에 대 한 메타 데이터를 추가 합니다.              |
| public void addColumnMetadata (SQLServerDataColumn 열)     | 지정 된 열에 대 한 메타 데이터를 추가 합니다.              |
| public void addRow (개체 ... 값인                          | 데이터 테이블에 데이터 행 하나를 추가 합니다.              |
| public Map\<Integer, SQLServerDataColumn > getColumnMetadata () | 이 데이터 테이블의 열 메타 데이터를 검색 합니다.       |
| public void clear()                                           | 이 데이터 테이블을 지웁니다.                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

이 클래스는 SQLServerDataTable으로 표시 되는 메모리 내 데이터 테이블의 열을 나타냅니다. 이 클래스의 메서드는 다음과 같습니다.  

| 속성                                                       | 설명                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn (문자열 columnName, int sqlType) | 열 이름과 유형을 사용 하 여 SQLServerDataColumn의 새 인스턴스를 초기화 합니다. |
| public String getColumnName()                              | 열 이름을 검색 합니다.                                                       |
| public int getColumnType()                                 | 열 형식을 검색 합니다.                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

이 클래스는 사용자가 테이블 반환 매개 변수로 데이터를 스트림 하기 위해 구현할 수 있는 인터페이스를 나타냅니다. 이 인터페이스의 메서드는 다음과 같습니다.  
  
| 속성                                                    | 설명                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | 지정 된 열 인덱스의 열 메타 데이터를 검색 합니다.                                               |
| public int getColumnCount();                            | 총 열 수를 검색 합니다.                                                                  |
| public Object[] getRowData();                           | 현재 행에 대한 데이터를 개체의 배열로 검색합니다.                                          |
| public boolean next();                                  | 다음 행으로 이동 합니다. 이동에 성공 하 고 다음 행이 있으면 True를 반환 하 고, 그렇지 않으면 false를 반환 합니다. |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

다음 메서드는이 클래스에 추가 되어 테이블 반환 매개 변수의 전달을 지원 합니다.  

| 속성                                                                                                    | 설명                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured (int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | 테이블 반환 매개 변수를 데이터 테이블로 채웁니다. parameterIndex는 매개 변수 인덱스이 고, tvpName은 테이블 반환 매개 변수의 이름이 고, tvpDataTable는 원본 데이터 테이블 개체입니다.                                                                                                          |
| public final void setStructured 된 (int parameterIndex, String tvpName, ResultSet tvpResultSet)             | 다른 테이블에서 검색 된 ResultSet으로 테이블 반환 매개 변수를 채웁니다. parameterIndex는 매개 변수 인덱스이 고, tvpName은 테이블 반환 매개 변수의 이름이 고, tvpResultSet는 원본 결과 집합 개체입니다.                                                                               |
| public final void setStructured (int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | ISQLServerDataRecord 개체를 사용 하 여 테이블 반환 매개 변수를 채웁니다. ISQLServerDataRecord은 스트리밍 데이터에 사용 되며 사용자는이를 사용 하는 방법을 결정 합니다. parameterIndex는 매개 변수 인덱스이 고, tvpName은 테이블 반환 매개 변수의 이름이 고, tvpDataRecord은 ISQLServerDataRecord 개체입니다. |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

다음 메서드는이 클래스에 추가 되어 테이블 반환 매개 변수의 전달을 지원 합니다.  
  
| 속성                                                                                                        | 설명                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured 된 (String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | 데이터 테이블을 사용 하 여 저장 프로시저에 전달 된 테이블 반환 매개 변수를 채웁니다. paratemeterName은 매개 변수의 이름이 고, tvpName은 TVP 형식의 이름이 고, tvpDataTable은 데이터 테이블 개체입니다.                                                                                                                 |
| public final void setStructured 된 (String paratemeterName, String tvpName, ResultSet tvpResultSet)             | 다른 테이블에서 검색 된 결과 집합을 사용 하 여 저장 프로시저에 전달 된 테이블 반환 매개 변수를 채웁니다. paratemeterName은 매개 변수의 이름이 고, tvpName은 TVP 형식의 이름이 고, tvpResultSet은 원본 결과 집합 개체입니다.                                                                              |
| public final void setStructured 된 (String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | ISQLServerDataRecord 개체를 사용 하 여 저장 프로시저에 전달 된 테이블 반환 매개 변수를 채웁니다. ISQLServerDataRecord은 스트리밍 데이터에 사용 되며 사용자는이를 사용 하는 방법을 결정 합니다. paratemeterName은 매개 변수의 이름이 고, tvpName은 TVP 형식의 이름이 고, tvpDataRecord는 ISQLServerDataRecord 개체입니다. |

## <a name="see-also"></a>관련 항목:

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
