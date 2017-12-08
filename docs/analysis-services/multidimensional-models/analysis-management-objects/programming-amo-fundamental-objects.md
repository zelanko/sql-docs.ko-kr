---
title: "AMO 기본 개체 프로그래밍 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- server objects [AMO]
- programming [AMO]
- AMO, database objects
- AMO, server objects
- Analysis Management Objects, server objects
- database objects [AMO]
- Analysis Management Objects, database objects
ms.assetid: 3f1ab656-f3bc-432d-8b6d-cdf204e5be10
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6eda664b7dbe009d5f82e0daffe0b428b26098d0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="programming-amo-fundamental-objects"></a>AMO 기본 개체 프로그래밍
  기본 개체는 일반적으로 단순하고 간단한 개체입니다. 이러한 개체는 대개 만들어지고 인스턴스화된 후 더 이상 필요하지 않게 되면 사용자가 개체와의 연결을 끊습니다. 기본 클래스에는 <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource> 및 <xref:Microsoft.AnalysisServices.DataSourceView> 개체가 포함됩니다. AMO 기본 개체 중 유일하게 복잡한 개체는 <xref:Microsoft.AnalysisServices.DataSourceView>로, 이 개체는 세부 정보가 있어야 데이터 원본 뷰를 나타내는 추상 모델을 빌드할 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.Server> 및 <xref:Microsoft.AnalysisServices.Database> 개체는 일반적으로 포함된 개체를 OLAP 개체나 데이터 마이닝 개체로 사용하는 데 필요합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [서버 개체](#ServerObjects)  
  
-   [AMOException 예외 개체](#AMO)  
  
-   [데이터베이스 개체](#DatabaseObjects)  
  
-   [DataSource 개체](#DataSource)  
  
-   [DataSourceView 개체](#DSV)  
  
##  <a name="ServerObjects"></a>서버 개체  
 <xref:Microsoft.AnalysisServices.Server> 개체를 사용하려면 서버에 연결한 다음 <xref:Microsoft.AnalysisServices.Server> 개체가 서버에 연결되어 있는지 확인하여 이 개체가 서버에 연결되어 있으면 서버에서 <xref:Microsoft.AnalysisServices.Server>의 연결을 끊어야 합니다.  
  
### <a name="connecting-to-the-server-object"></a>Server 개체에 연결  
 서버에 연결하려면 올바른 연결 문자열이 필요합니다.  
  
 다음 코드 예제 반환은 <xref:Microsoft.AnalysisServices.Server> 연결이 성공 하거나 반환 하는 경우 개체 **null** 오류가 발생 합니다. 연결 과정에서 발생하는 오류는 try/catch 구문에서 처리됩니다. AMO 오류는 <xref:Microsoft.AnalysisServices.AmoException> 예외 클래스를 사용하여 catch됩니다. 이 예에서는 메시지 상자에서 사용자에게 오류를 표시합니다.  
  
```  
static Server ServerConnect( String strStringConnection)  
{  
    string methodCaption = "ServerConnect method";  
    Server svr = new Server();  
    try  
    {  
        svr.Connect(strStringConnection);  
    }  
    #region ErrorHandling  
    catch (AmoException e)  
    {  
        MessageBox.Show( "AMO exception " + e.ToString());  
        svr = null;  
    }  
    catch (Exception e)  
    {  
        MessageBox.Show("General exception " + e.ToString());  
        svr = null;  
    }  
    #endregion  
  
    return svr;  
}  
```  
  
 연결 문자열의 구조는 다음과 같습니다.  
  
 "**데이터 원본 =**\<서버 이름 >"입니다.  
  
 연결 문자열에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Management.Common.OlapConnectionInfo.ConnectionString%2A>을 참조하십시오.  
  
### <a name="validating-the-connection"></a>연결 유효성 검사  
 <xref:Microsoft.AnalysisServices.Server> 개체를 프로그래밍하기 전에 서버에 아직 연결되어 있는지 확인해야 합니다. 다음 코드 예제에서는 이 방법을 보여 줍니다. 이 예제에서는 코드에 `svr`이라는 <xref:Microsoft.AnalysisServices.Server> 개체가 있다고 가정합니다.  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    // Do what it is needed if connection is good  
}  
```  
  
### <a name="disconnecting-from-the-server"></a>서버 연결 끊기  
 작업을 마치는 즉시 Disconnect 메서드를 사용하여 서버와의 연결을 끊을 수 있습니다. 다음 코드 예제에서는 이 방법을 보여 줍니다. 이 예제에서는 코드에 `svr`이라는 <xref:Microsoft.AnalysisServices.Server> 개체가 있다고 가정합니다.  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    svr.Disconnect()  
}  
```  
  
###  <a name="AMO"></a>AmoException 예외 개체  
 AMO는 다양한 문제가 발생할 때 예외를 throw합니다. 예외에 대 한 자세한 내용은 참조 하십시오. [AMO 기타 클래스 및 메서드](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)합니다. 다음 예제 코드에서는 AMO의 예외를 캡처하는 올바른 방법을 보여 줍니다.  
  
```  
try  
{  
   //... some AMO code in here  
}  
  
catch (  OutOfSynchException e)  
{  
   // error handling code for OutOfSynchException   
}  
  
catch (  OperationException e)  
{  
   // error handling code for OperationException   
}   
  
catch (  ResponseFormatException e)  
  
{  
   // error handling code for ResponseFormatException   
}   
  
catch (  ConnectionException e)  
  
{  
   // error handling code for ConnectionException   
}  
  
catch (  AMOException e)  
  
{  
   //... here is the place where you end if it is an AMO exception, but none of the previous exceptions  
   // if you start with AMOException in the first catch you will never see any one of the previous exceptions  
}  
```  
  
##  <a name="DatabaseObjects"></a>데이터베이스 개체  
 <xref:Microsoft.AnalysisServices.Database> 개체를 사용한 작업은 매우 단순하고 간단합니다. 기존 데이터베이스는 <xref:Microsoft.AnalysisServices.Server> 개체의 데이터베이스 컬렉션에서 가져옵니다.  
  
### <a name="creating-dropping-and-finding-a-database"></a>데이터베이스 만들기, 삭제 및 찾기  
 다음 코드 예제에서는 데이터베이스 이름을 사용하여 데이터베이스를 만드는 방법을 보여 줍니다. 데이터베이스를 만들기 전에는 서버의 <xref:Microsoft.AnalysisServices.DatabaseCollection>을 쿼리하여 해당 데이터베이스가 있는지 여부를 확인합니다. 해당 데이터베이스가 있으면 삭제된 후에 다시 만들어지고, 해당 데이터베이스가 없으면 새로 만들어집니다. 데이터베이스를 삭제할 경우에는 먼저 데이터베이스 컬렉션에서 해당 데이터베이스를 가져옵니다.  
  
```  
static Database CreateDatabase(Server svr, String DatabaseName)  
{  
    Database db = null;  
    if ( (svr != null) && ( svr.Connected))  
    {  
        // Drop the database if it already exists  
        db = svr.Databases.FindByName(DatabaseName);  
        if (db != null)  
        {  
            db.Drop();  
        }  
  
        // Create the database  
        db = svr.Databases.Add(DatabaseName);  
        db.Update();  
    }  
  
    return db;  
}  
```  
  
 데이터베이스가 데이터베이스 컬렉션에 있는지 확인하는 데는 FindByName 메서드가 사용됩니다. 데이터베이스가 있으면 이 메서드는 발견된 데이터베이스 개체를 반환하고, 그렇지 않으면 null 개체를 반환합니다.  
  
 <xref:Microsoft.AnalysisServices.Database> 개체를 데이터베이스 컬렉션에 추가하는 즉시 Update 메서드를 사용하여 서버를 업데이트해야 합니다. 서버를 업데이트하지 못하면 서버에 <xref:Microsoft.AnalysisServices.Database> 개체가 만들어지지 않습니다.  
  
### <a name="processing-a-database"></a>데이터베이스 처리  
 <xref:Microsoft.AnalysisServices.Database> 개체에는 Process 메서드가 포함되어 있으므로 데이터베이스와 모든 자식 개체를 처리하는 것은 매우 간단합니다.  
  
 Process 메서드에는 매개 변수가 포함될 수 있지만 매개 변수가 반드시 필요한 것은 아닙니다. 매개 변수가 지정 된 경우와 모든 자식 개체를 처리할지 자신의 **ProcessDefault** 옵션입니다. 처리 옵션에 대 한 자세한 내용은 참조 <xref:Microsoft.AnalysisServices.Database>합니다.  
  
1.  다음 예제 코드에서는 기본값에 따라 데이터베이스를 처리합니다.  
  
```  
static Database ProcessDatabase(Database db, ProcessType pt)  
{  
    db.Process( pt);  
    return db;  
}  
```  
  
##  <a name="DataSource"></a>DataSource 개체  
 <xref:Microsoft.AnalysisServices.DataSource> 개체는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]와 데이터가 있는 데이터베이스를 연결합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 기본 모델을 나타내는 스키마는 <xref:Microsoft.AnalysisServices.DataSourceView> 개체에 정의됩니다. <xref:Microsoft.AnalysisServices.DataSource> 개체는 데이터가 있는 데이터베이스에 대한 연결 문자열로 표시될 수 있습니다.  
  
 다음 예제 코드에서는 <xref:Microsoft.AnalysisServices.DataSource> 개체를 만드는 방법을 보여 줍니다. 이 예제에서는 서버가 아직 있고 <xref:Microsoft.AnalysisServices.Server> 개체가 연결되어 있으며 데이터베이스가 있는지 확인합니다. <xref:Microsoft.AnalysisServices.DataSource> 개체가 있으면 해당 개체는 삭제된 후 다시 만들어집니다. 이때 <xref:Microsoft.AnalysisServices.DataSource> 개체는 기존 개체와 동일한 이름 및 내부 ID로 만들어집니다. 이 예제에서는 연결 문자열에 대해 이를 확인하기 위한 검사를 수행하지 않습니다.  
  
```  
static string CreateDataSource(Database db, string strDataSourceName, string strConnectionString)  
{  
        Server svr = db.Parent;  
        DataSource ds = db.DataSources.FindByName(strDataSourceName);  
        if (ds != null)  
            ds.Drop();  
        // Create the data source  
        ds = db.DataSources.Add(strDataSourceName, strDataSourceName);  
        ds.ConnectionString = strConnectionString;  
  
        // Send the data source definition to the server.  
        ds.Update();  
  
        return ds.Name;  
}  
```  
  
##  <a name="DSV"></a>DataSourceView 개체  
 <xref:Microsoft.AnalysisServices.DataSourceView> 개체에는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 스키마 모델이 포함됩니다. <xref:Microsoft.AnalysisServices.DataSourceView> 개체에 스키마를 포함하려면 먼저 스키마를 생성해야 합니다. 스키마는 System.Data 네임스페이스에서 DataSet 개체에 대해 생성됩니다.  
  
 다음 예제 코드에서는 AdventureWorks 기반의 Analysis Services 예제 프로젝트에 포함된 스키마의 일부를 만듭니다. 예제에서는 테이블, 계산 열, 관계 및 복합 관계에 대한 스키마 정의를 만듭니다. 스키마는 데이터 집합에 저장됩니다.  
  
 이 예제 코드에서는 다음을 수행합니다.  
  
1.  <xref:Microsoft.AnalysisServices.DataSourceView> 개체를 만듭니다.  
  
     하는 경우 먼저 확인 된 <xref:Microsoft.AnalysisServices.DataSource> 개체가 있는지 **true**, 다음 삭제는 <xref:Microsoft.AnalysisServices.DataSource> 만들어야 합니다. <xref:Microsoft.AnalysisServices.DataSource> 개체가 없으면 새로 만듭니다.  
  
2.  <xref:Microsoft.AnalysisServices.DataSource> 연결 문자열을 사용하여 데이터베이스에 대한 연결을 엽니다.  
  
3.  스키마를 만듭니다.  
  
     스키마는 다음 항목으로 구성됩니다.  
  
    -   테이블 정의, `AddTable()` 메서드  
  
    -   선택적 계산 열 집합, `AddComputedColumn()` 메서드  
  
    -   선택적 관계 집합, `AddRelation`  
  
    -   선택적 복합 관계 집합, `AddCompositeRelations`  
  
4.  서버를 업데이트합니다.  
  
> [!NOTE]  
>  다음 예제 코드는 읽기 쉽도록 일부가 잘려 있습니다. 전체 코드는 이 항목의 맨 끝에 포함되어 있습니다.  
  
> [!NOTE]  
>  다음 방법의 샘플 코드의 일부인: `AddTable`, `AddComputedColumn`, `AddRelation`, 및 `AddCompositeRelation`합니다.  
  
> [!NOTE]  
>  절은 `'WHERE 1=0'` 행을 반환 하는 쿼리를 방지 하는 것은 **데이터 집합** 개체입니다.  
  
```  
        static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
        {  
            // Create the data source view  
            DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
            if ( dsv != null)  
               dsv.Drop();  
            dsv = db.DataSourceViews.Add(strDataSourceName);  
            dsv.DataSourceID = strDataSourceName;  
            dsv.Schema = new DataSet();  
            dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
            // Open a connection to the data source  
            OleDbConnection connection  
                = new OleDbConnection(dsv.DataSource.ConnectionString);  
            connection.Open();  
  
            #region Create tables  
  
            // Add the DimTime table  
            AddTable(dsv, connection, "DimTime");  
            AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
  
            // Add the DimProductCategory table  
            AddTable(dsv, connection, "DimProductCategory");  
  
            // Add the DimProductSubcategory table  
            AddTable(dsv, connection, "DimProductSubcategory");  
            AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
            // Add the FactInternetSales table  
            AddTable(dsv, connection, "FactInternetSales");  
"DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
  
            // Add the FactInternetSalesReason table  
            AddTable(dsv, connection, "FactInternetSalesReason");  
            AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
            dsv.Update();  
  
            #endregion  
  
            // Send the data source view definition to the server  
            dsv.Update();  
  
            return dsv;  
        }  
  
        static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
        {  
            string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
            OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
            DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
  
            dataTable.ExtendedProperties.Add("TableType", "Table");  
            dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
            dataTable.ExtendedProperties.Add("DbTableName", tableName);  
            dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
        }  
  
        static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
        {  
            DataSet tmpDataSet = new DataSet();  
            tmpDataSet.Locale = CultureInfo.CurrentCulture;  
            OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
                + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
                + tableName + "] WHERE 1=0", connection);  
            DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
            DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
            dataTable.Constraints.Clear();  
            dataTable.Columns.Remove(dataColumn);  
  
            dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
            dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
                expression);  
            dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
            dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
            dataColumn = null;  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
            tmpDataSet = null;  
        }  
  
        static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
        {  
            DataColumn fkColumn  
                = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
            DataColumn pkColumn  
                = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
                + fkColumnName, pkColumn, fkColumn, true);  
        }  
  
        static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
        {  
            DataColumn[] fkColumns = new DataColumn[2];  
            fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
            fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
            DataColumn[] pkColumns = new DataColumn[2];  
            pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
            pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
                + "_" + columnName2, pkColumns, fkColumns, true);  
        }  
  
```  
  
 샘플 코드에서는 `AddTable` 및 `AddComputedColumn` 메서드를 사용 하 여는 `FillSchema` 의 메서드는 **DataAdapter** 추가할 개체는 **DataTable** 에 **데이터집합**및 데이터 원본에 일치 하도록 스키마를 구성 하도록 합니다. 확장 속성은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 스키마를 구성하는 데 필요한 정보를 추가합니다.  
  
 예제 코드에서 `AddRelation` 및 `AddCompositeRelation` 메서드는 기존 스키마와 모델에 있는 기존 열에 따라 관계 열을 추가합니다. 이러한 메서드가 작동하기 위해서는 열이 스키마에 정의된 테이블의 일부여야 합니다.  
  
 다음은 전체 코드 예제입니다.  
  
```  
static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
{  
    // Create the data source view  
    DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
    if ( dsv != null)  
       dsv.Drop();  
    dsv = db.DataSourceViews.Add(strDataSourceName);  
    dsv.DataSourceID = strDataSourceName;  
    dsv.Schema = new DataSet();  
    dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
    // Open a connection to the data source  
    OleDbConnection connection  
        = new OleDbConnection(dsv.DataSource.ConnectionString);  
    connection.Open();  
  
    #region Create tables  
  
    // Add the DimTime table  
    AddTable(dsv, connection, "DimTime");  
    AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarYearDesc", "'CY' + ' ' + CalendarYear");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarSemesterDesc", "CASE WHEN CalendarSemester = 1 THEN 'H1'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) ELSE 'H2'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarQuarterDesc", "'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "MonthName", "EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalYearDesc", "'FY' + ' ' + FiscalYear");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalSemesterDesc", "CASE WHEN FiscalSemester = 1 THEN 'H1'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) ELSE 'H2'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalQuarterDesc", "'Q' + CONVERT(CHAR (1), FiscalQuarter) +' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalMonthNumberOfYear", "CASE WHEN MonthNumberOfYear = '1'  THEN CONVERT(int,'7') WHEN MonthNumberOfYear = '2'  THEN CONVERT(int,'8') WHEN MonthNumberOfYear = '3'  THEN CONVERT(int,'9') WHEN MonthNumberOfYear = '4'  THEN CONVERT(int,'10') WHEN MonthNumberOfYear = '5'  THEN CONVERT(int,'11') WHEN MonthNumberOfYear = '6'  THEN CONVERT(int,'12') WHEN MonthNumberOfYear = '7'  THEN CONVERT(int,'1') WHEN MonthNumberOfYear = '8'  THEN CONVERT(int,'2') WHEN MonthNumberOfYear = '9'  THEN CONVERT(int,'3') WHEN MonthNumberOfYear = '10' THEN CONVERT(int,'4') WHEN MonthNumberOfYear = '11' THEN CONVERT(int,'5') WHEN MonthNumberOfYear = '12' THEN CONVERT(int,'6') END");  
    dsv.Update();  
  
    // Add the DimGeography table  
    AddTable(dsv, connection, "DimGeography");  
  
    // Add the DimProductCategory table  
    AddTable(dsv, connection, "DimProductCategory");  
  
    // Add the DimProductSubcategory table  
    AddTable(dsv, connection, "DimProductSubcategory");  
    AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
    // Add the DimProduct table  
    AddTable(dsv, connection, "DimProduct");  
    AddComputedColumn(dsv, connection, "DimProduct", "ProductLineName", "CASE ProductLine WHEN 'M' THEN 'Mountain' WHEN 'R' THEN 'Road' WHEN 'S' THEN 'Accessory' WHEN 'T' THEN 'Touring' ELSE 'Components' END");  
    AddRelation(dsv, "DimProduct", "ProductSubcategoryKey", "DimProductSubcategory", "ProductSubcategoryKey");  
    dsv.Update();  
  
    // Add the DimCustomer table  
    AddTable(dsv, connection, "DimCustomer");  
    AddComputedColumn(dsv, connection, "DimCustomer", "FullName", "CASE WHEN MiddleName IS NULL THEN FirstName + ' ' + LastName ELSE FirstName + ' ' + MiddleName + ' ' + LastName END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "GenderDesc", "CASE WHEN Gender = 'M' THEN 'Male' ELSE 'Female' END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "MaritalStatusDesc", "CASE WHEN MaritalStatus = 'S' THEN 'Single' ELSE 'Married' END");  
    AddRelation(dsv, "DimCustomer", "GeographyKey", "DimGeography", "GeographyKey");  
  
    // Add the DimReseller table  
    AddTable(dsv, connection, "DimReseller");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderFrequencyDesc", "CASE WHEN OrderFrequency = 'A' THEN 'Annual' WHEN OrderFrequency = 'S' THEN 'Bi-Annual' ELSE 'Quarterly' END");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderMonthDesc", "CASE WHEN OrderMonth = '1' THEN 'January' WHEN OrderMonth = '2' THEN 'February' WHEN OrderMonth = '3' THEN 'March' WHEN OrderMonth = '4' THEN 'April' WHEN OrderMonth = '5' THEN 'May' WHEN OrderMonth = '6' THEN 'June' WHEN OrderMonth = '7' THEN 'July' WHEN OrderMonth = '8' THEN 'August' WHEN OrderMonth = '9' THEN 'September' WHEN OrderMonth = '10' THEN 'October' WHEN OrderMonth = '11' THEN 'November' WHEN OrderMonth = '12' THEN 'December' ELSE 'Never Ordered' END");  
  
    // Add the DimCurrency table  
    AddTable(dsv, connection, "DimCurrency");  
    dsv.Update();  
  
    // Add the DimSalesReason table  
    AddTable(dsv, connection, "DimSalesReason");  
  
    // Add the FactInternetSales table  
    AddTable(dsv, connection, "FactInternetSales");  
    AddRelation(dsv, "FactInternetSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactInternetSales", "CustomerKey", "DimCustomer", "CustomerKey");  
    AddRelation(dsv, "FactInternetSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    dsv.Update();  
  
    // Add the FactResellerSales table  
    AddTable(dsv, connection, "FactResellerSales");  
    AddRelation(dsv, "FactResellerSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactResellerSales", "ResellerKey", "DimReseller", "ResellerKey");  
    AddRelation(dsv, "FactResellerSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
  
    // Add the FactInternetSalesReason table  
    AddTable(dsv, connection, "FactInternetSalesReason");  
    AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
    dsv.Update();  
  
    // Add the FactCurrencyRate table  
    AddTable(dsv, connection, "FactCurrencyRate");  
    AddRelation(dsv, "FactCurrencyRate", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    AddRelation(dsv, "FactCurrencyRate", "TimeKey", "DimTime", "TimeKey");  
  
    #endregion  
  
    // Send the data source view definition to the server  
    dsv.Update();  
  
    return dsv;  
}  
  
static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
{  
    string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
    OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
    DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
  
    dataTable.ExtendedProperties.Add("TableType", "Table");  
    dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
    dataTable.ExtendedProperties.Add("DbTableName", tableName);  
    dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
}  
  
static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
{  
    DataSet tmpDataSet = new DataSet();  
    tmpDataSet.Locale = CultureInfo.CurrentCulture;  
    OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
        + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
        + tableName + "] WHERE 1=0", connection);  
    DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
    DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
    dataTable.Constraints.Clear();  
    dataTable.Columns.Remove(dataColumn);  
  
    dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
    dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
        expression);  
    dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
    dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
    dataColumn = null;  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
    tmpDataSet = null;  
}  
  
static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
{  
    DataColumn fkColumn  
        = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
    DataColumn pkColumn  
        = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
        + fkColumnName, pkColumn, fkColumn, true);  
}  
  
static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
{  
    DataColumn[] fkColumns = new DataColumn[2];  
    fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
    fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
    DataColumn[] pkColumns = new DataColumn[2];  
    pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
    pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
        + "_" + columnName2, pkColumns, fkColumns, true);  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices>   
 [AMO 클래스 소개](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO 기본 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [논리적 아키텍처 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
