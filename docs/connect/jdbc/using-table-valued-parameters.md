---
title: 테이블 반환 매개 변수를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6ac7155299100c0faecae67c8d8465a11305e26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-table-valued-parameters"></a>테이블 반환 매개 변수를 사용 하 여
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  테이블 반환 매개 변수는 쉽게 데이터 처리를 위한 여러 번 왕복 하거나 특수 한 서버측 논리를 요구 하지 않고 SQL Server 클라이언트 응용 프로그램에서 데이터의 여러 행을 마샬링할 수 있는 방법을 제공 합니다. 클라이언트 응용 프로그램에서 데이터 행을 캡슐화 하 고 서버는 단일 매개 변수가 있는 명령에는 데이터를 전송에 테이블 반환 매개 변수를 사용할 수 있습니다. 들어오는 데이터 행은 다음 작동 될 수 있는에 TRANSACT-SQL을 사용 하 여 테이블 변수에 저장 됩니다.  
  
 열 값에 테이블 반환 매개 변수는 표준 TRANSACT-SQL SELECT 문을 사용 하 여 액세스할 수 있습니다. 테이블 반환 매개 변수는 강력한 형식이 지정 하 고 해당 구조 자동으로 유효성을 검사 합니다. 테이블 반환 매개 변수 크기는 서버의 메모리 크기로 제한 됩니다.  
  
> [!NOTE]  
>  테이블 반환 매개 변수에 대 한 지원은 SQL Server 용 Microsoft JDBC Driver 6.0부터 제공 됩니다.  
  
> [!NOTE]  
>  테이블 반환 매개 변수에서 데이터를 반환할 수 없습니다. 테이블 반환 매개 변수는 입력 전용; OUTPUT 키워드도 지원 되지 않습니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 다음 리소스를 참조 합니다.  
  
|리소스|Description|  
|--------------|-----------------|  
|[테이블 반환 매개 변수 (데이터베이스 엔진)](http://go.microsoft.com/fwlink/?LinkId=98363) SQL Server 온라인 설명서의|만들고 테이블 반환 매개 변수를 사용 하는 방법에 설명|  
|[사용자 정의 테이블 형식을](http://go.microsoft.com/fwlink/?LinkId=98364) SQL Server 온라인 설명서의|테이블 반환 매개 변수를 선언 하는 데 사용 되는 사용자 정의 테이블 형식을 설명합니다|  
|[Microsoft SQL Server 데이터베이스 엔진](http://go.microsoft.com/fwlink/?LinkId=120507) CodePlex의 섹션|SQL Server 기능 및 기능을 사용 하는 방법을 보여 주는 샘플이 포함 되어|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>이전 버전의 SQL Server에서 여러 행 전달  
 테이블 반환 매개 변수를 SQL Server 2008 도입 되기 전에 저장된 프로시저 또는 매개 변수가 있는 SQL 명령에 여러 행의 데이터를 전달 하기 위한 옵션이 제한적 이었습니다. 개발자는 서버에 여러 행을 전달 하기 위한 다음 옵션 중에서 선택할 수 없습니다.  
  
-   일련의 개별 매개 변수를 사용 하 여 여러 개의 열과 데이터 행의 값을 나타냅니다. 이 방법을 사용 하 여 전달 될 수 있는 데이터의 양은 허용 하는 매개 변수 개수에 의해 제한 됩니다. SQL Server 프로시저 있을 수 있지만, 최대 2100 개의 매개 변수입니다. 서버 쪽 논리는 테이블 변수 또는 처리를 위해 임시 테이블에 이러한 개별 값을 조합 하는 데 필요 합니다.  
  
-   여러 데이터 값을 구분 기호로 분리 된 문자열 또는 XML 문서 묶고 그런 다음 이러한 텍스트 값을 프로시저나 문에 전달 합니다. 이렇게 하려면 프로시저 또는 데이터 구조 및 묶인 유효성을 검사 하는 데 필요한 논리를 포함 하도록 문을 값 합니다.  
  
-   일련의 여러 행에 영향을 주는 데이터 수정 위한 개별 SQL 문 만듭니다. 변경 내용은 서버에 개별적으로 제출 또는 그룹으로 일괄 처리할 수 있습니다. 그러나 여러 문이 포함 된 일괄 처리로 제출 하는 경우에 각 문이 실행 됩니다 개별적으로 서버에.  
  
-   Bcp 유틸리티 프로그램을 사용 하 여 또는 [SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx) 테이블에 많은 데이터 행을 로드 하는 개체입니다. 이 기술은 매우 효율적 이지만, 데이터가 로드 되 고 임시 테이블이 나 테이블 변수에 되지 않을 경우 서버 쪽 처리 지원 하지 않습니다.  
  
## <a name="creating-table-valued-parameter-types"></a>테이블 반환 매개 변수 형식 만들기  
 테이블 반환 매개 변수-CREATE TYPE 문을 사용 하 여 정의 된 강력한 형식의 테이블 구조를 기반으로 합니다. 테이블 형식을 만들고 클라이언트 응용 프로그램에서 테이블 반환 매개 변수를 사용 하려면 먼저 SQL Server의 구조를 정의 해야 합니다. 테이블 형식 만들기에 대 한 자세한 내용은 참조 [사용자 정의 테이블 형식](http://go.microsoft.com/fwlink/?LinkID=98364) SQL Server 온라인 설명서의 합니다.  
  
```  
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 테이블 형식을 만든 후 해당 형식에 따라 테이블 반환 매개 변수를 선언할 수 있습니다. 다음 TRANSACT-SQL 조각에는 저장된 프로시저 정의에 테이블 반환 매개 변수를 선언 하는 방법을 보여 줍니다. READONLY 키워드는 테이블 반환 매개 변수를 선언 하기 위한 필요 하다는 참고 합니다.  
  
```  
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>테이블 반환 매개 변수 (Transact SQL)로 데이터 수정  
 테이블 반환 매개 변수는 단일 문을 실행 하 여 여러 행에 영향을 주는 집합 기반 데이터 수정에 사용할 수 있습니다. 예를 들어 테이블 반환 매개 변수에서 모든 행을 선택 하 고 데이터베이스 테이블에 삽입 하거나 업데이트 하려는 테이블에는 테이블 반환 매개 변수를 조인 하 여 update 문을 만들 수 있습니다.  
  
 다음 TRANSACT-SQL UPDATE 문은 테이블 반환 매개 변수를 Categories 테이블에 조인 하 여 사용 하는 방법을 보여 줍니다. FROM 절에 JOIN과 함께 테이블 반환 매개 변수를 사용 하면 수행 해야 별칭을 다음과 같이, 여기서 테이블 반환 매개 변수는 이라는 별칭을 "ec".  
  
```  
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 이 TRANSACT-SQL 예제에서는 단일 집합 기반 작업에서 삽입을 수행 하는 테이블 반환 매개 변수에서 행을 선택 합니다.  
  
```  
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>테이블 반환 매개 변수의 제한 사항  
 테이블 반환 매개 변수에 몇 가지 제한 사항이 있습니다.  
  
-   사용자 정의 함수에 테이블 반환 매개 변수를 전달할 수 없습니다.  
  
-   테이블 반환 매개 변수는 UNIQUE 또는 PRIMARY KEY 제약 조건을 지원 하도록 인덱싱할 수만 있습니다. SQL Server 테이블 반환 매개 변수에 대 한 통계를 유지 하지 않습니다.  
  
-   테이블 반환 매개 변수는 Transact SQL 코드의 읽기 전용입니다. 테이블 반환 매개 변수의 행에서 열 값을 업데이트 및 삽입 하거나 행을 삭제할 수 없습니다. 매개 변수화 된 문에 테이블 반환 매개 변수 또는 저장된 프로시저에 전달 되는 데이터를 수정 하려면 임시 테이블로 또는 테이블 변수로 데이터를 삽입 해야 합니다.  
  
-   테이블 반환 매개 변수 디자인을 수정 하려면 ALTER TABLE 문을 사용할 수 없습니다.
-   테이블 반환 매개 변수에서 대형 개체를 스트리밍할 수 있습니다.  
  
## <a name="configuring-a-table-valued-parameter"></a>테이블 반환 매개 변수를 구성합니다.  
 SQL Server 용 Microsoft JDBC Driver 6.0부터, 테이블 반환 매개 변수는 매개 변수가 있는 저장된 프로시저 또는 매개 변수가 있는 문을 지원 합니다. 테이블 반환 매개 변수는 결과 집합에서 한 SQLServerDataTable에서 채워진 또는 사용자 로부터 ISQLServerDataRecord 인터페이스의 구현을 제공 수 있습니다. 준비 된 쿼리에 대 한 테이블 반환 매개 변수를 설정할 때는 서버에서 이전에 만든 호환 가능한 형식의 이름과 일치 해야 하는 형식 이름을 지정 해야 합니다.  
  
 다음 두 코드 조각을 SQLServerPreparedStatement 및 데이터를 삽입 하는 SQLServerCallableStatement 테이블 반환 매개 변수를 구성 하는 방법을 보여 줍니다. 여기서는 SQLServerDataTable 결과 집합 또는 ISQLServerDataRecord 개체 sourceTVPObject 수 있습니다. 예제에서는 연결이 활성 연결 개체를 사용 하는 것을 가정 합니다.  
  
```  
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =   
    (SQLServerPreparedStatement) connection.prepareStatement(“INSERT INTO dbo.Categories SELECT * FROM ?”);  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```  
  
```  
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =   
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");       
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```  
  
> [!NOTE]  
>  섹션을 참조 **JDBC 드라이버에 대 한 테이블 반환 매개 변수 API** 아래 테이블 반환 매개 변수 설정에 사용할 수 있는 Api의 전체 목록은 합니다.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>SQLServerDataTable 개체로 테이블 반환 매개 변수 전달  
 SQL Server 용 Microsoft JDBC Driver 6.0부터, SQLServerDataTable 클래스를 사용 하는 관계형 데이터의 메모리 내 테이블이 나타냅니다. 이 예제에서는 SQLServerDataTable 개체를 사용 하 여 메모리 데이터에서 테이블 반환 매개 변수를 생성 하는 방법을 보여 줍니다. 코드에서 먼저 SQLServerDataTable 개체를 만듭니다, 그리고 해당 스키마를 정의 하는 테이블을 데이터로 채웁니다. 코드는 다음이 데이터 테이블을 SQL server 테이블 반환 매개 변수로 전달 하는 SQLServerPreparedStatement를 구성 합니다.  
  
```  
// Assumes connection is an active Connection object.  
  
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
>  섹션을 참조 **JDBC 드라이버에 대 한 테이블 반환 매개 변수 API** 아래 테이블 반환 매개 변수 설정에 사용할 수 있는 Api의 전체 목록은 합니다.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>결과 집합 개체와 테이블 반환 매개 변수 전달  
 이 예에서는 테이블 반환 매개 변수를 결과 집합에서 데이터 행을 스트림 하는 방법을 보여 줍니다. 코드의 원본 테이블에서 데이터를 먼저 검색 한 SQLServerDataTable 개체를 만들고 해당 스키마를 정의 하는 테이블을 데이터로 채웁니다. 코드는 다음이 데이터 테이블을 SQL server 테이블 반환 매개 변수로 전달 하는 SQLServerPreparedStatement를 구성 합니다.  
  
```  
// Assumes connection is an active Connection object.  
  
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
>  섹션을 참조 **JDBC 드라이버에 대 한 테이블 반환 매개 변수 API** 아래 테이블 반환 매개 변수 설정에 사용할 수 있는 Api의 전체 목록은 합니다.  
  
## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>ISQLServerDataRecord 개체로 테이블 반환 매개 변수 전달  
 SQL Server 용 Microsoft JDBC Driver 6.0부터, 새로운 인터페이스 ISQLServerDataRecord ´ ü ± (에 따라 사용자에 대 한 구현을 제공 하는 방법) 데이터를 스트리밍 테이블 반환 매개 변수를 사용 합니다. 다음 예제에서는 테이블 반환 매개 변수로 전달 하는 방법과 ISQLServerDataRecord 인터페이스를 구현 하는 방법을 보여 줍니다. 간단한 설명을 위해 다음 예제에서는 테이블 반환 매개 변수를 하드 코드 된 값이 포함 된 하나의 행을 전달합니다. 이상적으로 사용자 예를 들어 텍스트 파일에서에서 모든 원본에서 데이터 행을 스트리밍할이이 인터페이스를 구현 합니다.  
  
```  
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
>  섹션을 참조 **JDBC 드라이버에 대 한 테이블 반환 매개 변수 API** 아래 테이블 반환 매개 변수 설정에 사용할 수 있는 Api의 전체 목록은 합니다.  
    
## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC 드라이버에 대 한 테이블 반환 매개 API  
 **SQLServerMetaData**  
  
 이 클래스는 열에 대 한 메타 데이터를 나타냅니다. 열 메타 데이터는 테이블 반환 매개 변수를 전달 하는 ISQLServerDataRecord 인터페이스에서 사용 됩니다. 이 클래스의 메서드는 있습니다.  
  
|이름|Description|  
|----------|-----------------|  
|공용 SQLServerMetaData (문자열 columnName, sqlType int, int 정밀도, int 배율, 부울 useServerDefault, 부울 isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal)|지정한 열 이름, sql 형식, 정밀도, 배율 및 서버 기본값 SQLServerMetaData의 새 인스턴스를 초기화합니다. 이 형식의 생성자는 열이 테이블 반환 매개 변수, 열 및 정렬 열의 서 수에 대 한 정렬 순서에서 고유 하는 경우 지정할 수 있도록 허용 하 여 테이블 반환 매개 변수를 지원 합니다. <br><br>이 열에서 기본 서버 값을 사용 해야 하는 경우-useServerDefault 지정 기본값은 false입니다.<br>isUniqueKey-테이블 반환 매개 변수의 열 고유; 인지 여부를 나타냅니다. 기본값은 false입니다.<br>sortOrder-열에 대 한 정렬 순서를 나타냅니다. 기본값은 SQLServerSortOrder.Unspecified입니다.<br>sortOrdinal-정렬 열의 서 수를 지정 합니다. sortOrdinal 0;에서 시작 됩니다. 기본값은-1입니다.|
|공용 SQLServerMetaData (문자열 columnName, int sqlType)|열 이름 및 sql 형식을 사용 하 여 SQLServerMetaData의 새 인스턴스를 초기화 합니다.|  
|공용 SQLServerMetaData (문자열 columnName, int sqlType, int 정밀도, 배율 int)|열 이름, sql 형식, 전체 자릿수 및 소수 자릿수를 사용 하 여 SQLServerMetaData의 새 인스턴스를 초기화 합니다.|  
|공용 SQLServerMetaData (SQLServerMetaData sqlServerMetaData)|다른 SQLServerMetaData 개체를 SQLServerMetaData에서 새 인스턴스를 초기화합니다.|  
|공용 문자열 getColumName()|열 이름을 검색합니다.|  
|공용 int getSqlType()|Java sql 형식을 검색합니다.|  
|공용 int getPrecision()|열에 전달 된 형식의 전체 자릿수를 검색 합니다.|  
|공용 int getScale()|열에 전달 된 형식의 소수 자릿수를 검색 합니다.|  
|공용 SQLServerSortOrder getSortOrder()|정렬 순서를 검색 합니다.|
|공용 int getSortOrdinal()|정렬 서 수를 검색합니다.|
|공용 부울 isUniqueKey()|열이 고유한 지 여부를 반환 합니다.|
|공용 부울 useServerDefault()|반환 wheher 열에서 기본 서버 값을 사용합니다.|
  
 **SQLServerSortOrder**
 
 정렬 순서를 정의 하는 열거형입니다. 가능한 값은 오름차순, 내림차순 및 지정 되지 않음. 
  
 **SQLServerDataTable**  
  
 이 클래스는 테이블 반환 매개 변수를 함께 사용 되는 메모리 내 데이터 테이블을 나타냅니다. 이 클래스의 메서드는 있습니다.  
  
|이름|Description|  
|----------|-----------------|  
|공용 SQLServerDataTable()|SQLServerDataTable의 새 인스턴스를 초기화합니다.|  
|공개 반복기 < 항목\<정수, Object >> getIterator()|데이터 테이블의 행에 대 한 반복기를 검색 합니다.|  
|public void addColumnMetadata (문자열 columnName, int sqlType)|지정된 된 열에 대 한 메타 데이터를 추가합니다.|  
|public void addColumnMetadata (SQLServerDataColumn 열)|지정된 된 열에 대 한 메타 데이터를 추가합니다.|  
|public void addRow (개체... 값).|데이터 테이블에 데이터의 한 행을 추가합니다.|  
|공용 맵\<정수, SQLServerDataColumn > getColumnMetadata()|이 데이터 테이블의 열 메타 데이터를 검색합니다.|
|public void clear) |이 데이터 테이블을 지웁니다. |  
  
 **SQLServerDataColumn**  
  
 이 클래스는 SQLServerDataTable로 표시 된 메모리 내 데이터 테이블의 열을 나타냅니다. 이 클래스의 메서드는 있습니다.  
  
|이름|Description|  
|----------|-----------------|  
|공용 SQLServerDataColumn (문자열 columnName, int sqlType)|열 이름 및 형식을 SQLServerDataColumn의 새 인스턴스를 초기화합니다.|  
|공용 문자열 getColumnName()|열 이름을 검색합니다.|  
|공용 int getColumnType()|열 유형을 검색합니다.|  
  
 **ISQLServerDataRecord**  
  
 이 클래스는 사용자가 데이터를 스트리밍하려면 테이블 반환 매개 변수를 구현할 수 있는 인터페이스를 나타냅니다. 이 인터페이스의 메서드는 있습니다.  
  
|이름|Description|  
|----------|-----------------|  
|공용 SQLServerMetaData getColumnMetaData (int 열);|지정된 된 열 인덱스의 열 메타 데이터를 검색합니다.|  
|공용 int getColumnCount();|열의 총 수를 검색합니다.|  
|개체 getRowData() 공용;|개체의 배열으로 현재 행에 대 한 데이터를 검색합니다.|  
|공용 부울 next ();|다음 행으로 이동 합니다. 성공적으로 이동 하 고 그렇지 않으면 false 다음 행이 있으면 True를 반환 합니다.|  
  
 **SQLServerPreparedStatement**  
  
 다음 방법 전달 하는 테이블 반환 매개 변수를 지원 하도록이 클래스에 추가 되었습니다.  
  
|이름|Description|  
|----------|-----------------|  
|공용 최종 void setStructured (int parameterIndex, 문자열 tvpName, SQLServerDataTable tvpDataTbale)|데이터 테이블과 함께 테이블 반환 매개 변수를 채웁니다. parameterIndex 매개 변수 인덱스, tvpName 테이블 반환 매개 변수의 이름을 이며 tvpDataTable 원본 데이터 테이블 개체입니다.|  
|공용 최종 void setStructured (int parameterIndex, 문자열 tvpName, 결과 집합 tvpResultSet)|다른 테이블에서 검색 된 결과 집합으로 테이블 반환 매개 변수를 채웁니다. parameterIndex 매개 변수 인덱스, tvpName 테이블 반환 매개 변수의 이름을 이며 tvpResultSet 소스 결과 집합 개체입니다.|  
|공용 최종 void setStructured (int parameterIndex, 문자열 tvpName, ISQLServerDataRecord tvpDataRecord)|ISQLServerDataRecord 개체는 테이블 반환 매개 변수를 채웁니다. ISQLServerDataRecord 스트리밍 데이터에 사용 되 고 사용자가 사용 하는 방법을 결정 합니다. parameterIndex 매개 변수 인덱스, tvpName 테이블 반환 매개 변수의 이름을 이며 tvpDataRecord는 ISQLServerDataRecord 개체입니다.|  
  
 **SQLServerCallableStatement**  
  
 다음 방법 전달 하는 테이블 반환 매개 변수를 지원 하도록이 클래스에 추가 되었습니다.  
  
|이름|Description|  
|----------|-----------------|  
|공용 최종 void setStructured (문자열 paratemeterName, 문자열 tvpName, SQLServerDataTable tvpDataTable)|데이터 테이블과 함께 저장된 프로시저에 전달 하는 테이블 반환 매개 변수를 채웁니다. paratemeterName 매개 변수의 이름, tvpName TVP 형식의 이름을 이며 tvpDataTable 데이터 테이블 개체입니다.|  
|공용 최종 void setStructured (문자열 paratemeterName, 문자열 tvpName, 결과 집합 tvpResultSet)|다른 테이블에서 검색 된 결과 집합으로 저장된 프로시저에 전달 하는 테이블 반환 매개 변수를 채웁니다. paratemeterName 매개 변수의 이름, tvpName TVP 형식의 이름을 이며 tvpResultSet 소스 결과 집합 개체입니다.|  
|공용 최종 void setStructured (문자열 paratemeterName, 문자열 tvpName, ISQLServerDataRecord tvpDataRecord)|ISQLServerDataRecord 개체와 저장된 프로시저에 전달 하는 테이블 반환 매개 변수를 채웁니다. ISQLServerDataRecord 스트리밍 데이터에 사용 되 고 사용자가 사용 하는 방법을 결정 합니다. paratemeterName 매개 변수의 이름, tvpName TVP 형식의 이름을 이며 tvpDataRecord는 ISQLServerDataRecord 개체입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
