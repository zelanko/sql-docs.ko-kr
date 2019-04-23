---
title: 테이블 표현 (테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: a636fc13-4054-4cea-bce1-192ec4796063
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c733fbf1e8a075d0d240f5cb69d888310fc6009f
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60155420"
---
# <a name="tables-representation-tabular"></a>테이블 표현(테이블 형식)
  테이블 형식 모델에서 테이블은 데이터의 기본 표현입니다.  
  
## <a name="tables-representation"></a>테이블 표현  
  
### <a name="tables-in-amo"></a>AMO의 테이블  
 AMO를 사용하여 테이블을 관리하는 경우 일 대 일 개체 일치 관계가 없습니다. AMO에서 테이블은 <xref:Microsoft.AnalysisServices.Dimension> 및 <xref:Microsoft.AnalysisServices.MeasureGroup>으로 표현됩니다. 측정값 그룹이 존재하려면 측정값 그룹을 호스팅하도록 <xref:Microsoft.AnalysisServices.Cube>를 정의해야 합니다. 또한 차원, 측정값 그룹 및 큐브가 존재하려면 데이터 원본에 대한 바인딩 정의를 포함하도록 데이터 원본 뷰 개체를 정의해야 합니다.  
  
 절차상의 관점에서 볼 때 데이터 원본 뷰는 다른 개체를 정의하기 전에 만들어야 합니다. 데이터 원본 뷰 개체는 데이터 원본 내에 모든 관련 개체에 대한 매핑을 포함합니다. 관계형 모델의 매핑은 .Net DataSet 개체로 데이터 원본 뷰에 포함되고 DSV의 Schema 속성에 저장됩니다.  
  
 다음 코드 조각에서는 테이블 형식 모델에 나타내려는 관계형 모델에 있는 모든 테이블로 매핑될 Select 문의 사전인 SQL 클라이언트 연결 문자열과 데이터 원본 뷰의 이름(대개 관계형 데이터베이스의 이름)이 포함된 변수 newDataSourceViewName을 보유하고 있다고 가정합니다.  
  
```  
  
DataSet newDataSourceViewDataSet = new DataSet(newDataSourceViewName);  
  
Foreach( String tableName in listOfSqlStatements.Keys)  
{  
    String sqlStmt = listOfSqlStatements[tableName];  
  
    DataTable newTable = new DataTable(tableName);  
  
    using (SqlConnection SqlCnx = new SqlConnection(SqlCnxStr))  
    {  
        SqlDataAdapter dataAdapter = new SqlDataAdapter(sqlStmt, SqlCnx);  
        dataAdapter.FillSchema(newTable, SchemaType.Source);  
    }  
    newDataSourceViewDataSet.Tables.Add(newTable);  
}  
  
AMO.DataSourceView newDatasourceView = newDatabase.DataSourceViews.AddNew(newDataSourceViewName, newDataSourceViewName);  
newDatasourceView.DataSourceID = newDatasource.ID; //This is the ID of the DataSource object   
newDatasourceView.Schema = newDataSourceViewDataSet; //Here you are storing all the relational schema in the DSV  
newDatasourceView.Update();  
  
```  
  
 데이터 원본 뷰를 만들고 업데이트하면 큐브 개체를 만들어야 하지만 첫 테이블을 만들 때까지 서버에서 업데이트하면 안 됩니다. 비어 있는 큐브 개체를 만들 수는 없습니다. 다음 코드 조각에서는 큐브를 만드는 방법을 보여 줍니다. 이 조각에서는 비어 있지 않은 문자열 newCubeName을 보유하고 있으며 큐브의 이름은 이미 중복성 검사를 완료한 것으로 가정합니다.  
  
```  
  
modelCube = newDatabase.Cubes.Add(newCubeName, newCubeName);  
modelCube.Source = new AMO.DataSourceViewBinding(newDatasourceView.ID);  
modelCube.StorageMode = AMO.StorageMode.InMemory;  
modelCube.Language = newDatabase.Language;  
modelCube.Collation = newDatabase.Collation;  
//Create initial MdxScript  
AMO.MdxScript mdxScript = modelCube.MdxScripts.Add("MdxScript", "MdxScript");  
StringBuilder initialCommand = new StringBuilder();  
initialCommand.AppendLine("CALCULATE;");  
initialCommand.AppendLine("CREATE MEMBER CURRENTCUBE.Measures.[__No measures defined] AS 1;");  
initialCommand.AppendLine("ALTER CUBE CURRENTCUBE UPDATE DIMENSION Measures, Default_Member = [__No measures defined];");  
mdxScript.Commands.Add(new AMO.Command(initialCommand.ToString()));  
  
```  
  
 큐브가 로컬에서 정의되면 테이블을 만들고 업데이트할 수 있습니다. 다음 절차에서는 테이블을 만들기 위한 필수 단계를 요약해서 보여 줍니다.  
  
1.  테이블을 나타내는 차원을 만들고 아직 서버에서 업데이트하지 않습니다.  
  
2.  RowNumber 특성을 만들고 차원의 키 특성으로 정의합니다.  
  
3.  차원 특성을 만들고 RowNumber에 대해 일 대 다 관계로 표시합니다.  
  
4.  큐브 차원에 차원을 추가합니다.  
  
5.  테이블을 나타내는 측정값 그룹도 만듭니다.  
  
6.  측정값 그룹에 차원을 추가합니다.  
  
7.  측정값 그룹에 AMO 기본 측정값 개체를 만듭니다. 참고로, 이때가 AMO 측정값 개체를 사용하는 유일한 경우입니다. 테이블 형식 모델에서 계산 측정값은 AMO MdxScripts["MdxScript"] 개체에 정의됩니다.  
  
8.  기본 파티션을 만듭니다.  
  
9. 데이터베이스를 업데이트합니다.  
  
 다음 코드 조각에서는 테이블을 만드는 방법을 보여 줍니다.  
  
```  
  
private Boolean CreateTable(  
                       AMO.Database db      //the AMO database object where dimension are created  
                     , AMO.Cube cb          //the AMO cube where measure group is created  
                     , DataTable dataTable  //the schema of the table to be created  
                     )  
{  
    String tableID = dataTable.TableName;  
  
    if (db.Dimensions.Contains(tableID))  
    {  
        if (cb.MeasureGroups.Contains(tableID))  
        {  
            cb.MeasureGroups[tableID].Measures.Clear();  
            cb.MeasureGroups[tableID].Partitions.Clear();  
            cb.MeasureGroups.Remove(tableID, true);  
        }  
        if (cb.Dimensions.Contains(tableID))  
        {  
            cb.Dimensions.Remove(tableID, true);  
        }  
        db.Dimensions.Remove(tableID);  
    }  
  
    #region Create Dimension  
    //Define Dimension general properties  
    AMO.Dimension currentDimension = db.Dimensions.AddNew(tableID, tableID);  
    currentDimension.Source = new AMO.DataSourceViewBinding(newDatasourceView.ID);  
    currentDimension.StorageMode = AMO.DimensionStorageMode.InMemory;  
    currentDimension.UnknownMember = AMO.UnknownMemberBehavior.AutomaticNull;  
    currentDimension.UnknownMemberName = "Unknown";  
    currentDimension.ErrorConfiguration = new AMO.ErrorConfiguration();  
    currentDimension.ErrorConfiguration.KeyNotFound = AMO.ErrorOption.IgnoreError;  
    currentDimension.ErrorConfiguration.KeyDuplicate = AMO.ErrorOption.ReportAndStop;  
    currentDimension.ErrorConfiguration.NullKeyNotAllowed = AMO.ErrorOption.ReportAndStop;  
    currentDimension.Language = db.Language;  
    currentDimension.Collation = db.Collation;  
    currentDimension.ProactiveCaching = new AMO.ProactiveCaching();  
    TimeSpan defaultProactiveChachingTimeSpan = new TimeSpan(0, 0, -1);  
    currentDimension.ProactiveCaching.SilenceInterval = defaultProactiveChachingTimeSpan;  
    currentDimension.ProactiveCaching.Latency = defaultProactiveChachingTimeSpan;  
    currentDimension.ProactiveCaching.SilenceOverrideInterval = defaultProactiveChachingTimeSpan;  
    currentDimension.ProactiveCaching.ForceRebuildInterval = defaultProactiveChachingTimeSpan;  
    currentDimension.ProactiveCaching.Source = new AMO.ProactiveCachingInheritedBinding();  
  
    //Manualy add a "RowNumber" attribute as the key attribute of the dimension, until a primary key is defined  
    //"RowNumber" a required column for a tabular model and has to be of type AMO.AttributeType.RowNumber and binding AMO.RowNumberBinding.  
    //The name of the "RowNumber" attribute can be any name, as long as type and binding are correctly set  
    //By default, the MS client tools set the column name and column ID of the RowNumber attribute to "RowNumber"  
    //In this sample, to avoid problems, on any customer table that contains a column named 'RowNumber'   
    //the Id value of the column (in the dimension object) will be renamed to 'RowNumber_in_<TableName>' and the Name of the column will remain "RowNumber"  
  
    AMO.DimensionAttribute currentAttribute = currentDimension.Attributes.Add("RowNumber", "RowNumber");  
    currentAttribute.Type = AMO.AttributeType.RowNumber;  
    currentAttribute.KeyUniquenessGuarantee = true;  
    currentAttribute.Usage = AMO.AttributeUsage.Key;  
    currentAttribute.KeyColumns.Add(new AMO.DataItem());  
    currentAttribute.KeyColumns[0].DataType = System.Data.OleDb.OleDbType.Integer;  
    currentAttribute.KeyColumns[0].DataSize = 4;  
    currentAttribute.KeyColumns[0].NullProcessing = AMO.NullProcessing.Error;  
    currentAttribute.KeyColumns[0].Source = new AMO.RowNumberBinding();  
    currentAttribute.NameColumn = new AMO.DataItem();  
    currentAttribute.NameColumn.DataType = System.Data.OleDb.OleDbType.WChar;  
    currentAttribute.NameColumn.DataSize = 4;  
    currentAttribute.NameColumn.NullProcessing = AMO.NullProcessing.ZeroOrBlank;  
    currentAttribute.NameColumn.Source = new AMO.RowNumberBinding();  
    currentAttribute.OrderBy = AMO.OrderBy.Key;  
    currentAttribute.AttributeHierarchyVisible = false;  
    //Deferring AttributeRelationships until after adding each other attribute  
    //Add each column in the table as an attribute in the dimension  
    foreach (DataColumn dataColumn in dataTable.Columns)  
    {  
        string attributeID, attributeName;  
        if (dataColumn.ColumnName != "RowNumber")  
        {  
            attributeID = dataColumn.ColumnName;  
        }  
        else  
        {  
            attributeID = string.Format("RowNumber_in_{0}", dataTable.TableName);  
        }  
        attributeName = dataColumn.ColumnName;  
        currentAttribute = currentDimension.Attributes.Add(attributeName, attributeID);  
        currentAttribute.Usage = AMO.AttributeUsage.Regular;  
        currentAttribute.KeyUniquenessGuarantee = false;  
        currentAttribute.KeyColumns.Add(new AMO.DataItem(dataTable.TableName, dataColumn.ColumnName, AMO.OleDbTypeConverter.GetRestrictedOleDbType(dataColumn.DataType)));  
        currentAttribute.KeyColumns[0].Source = new AMO.ColumnBinding(dataTable.TableName, dataColumn.ColumnName);  
        currentAttribute.KeyColumns[0].NullProcessing = AMO.NullProcessing.Preserve;  
        currentAttribute.NameColumn = new AMO.DataItem(dataTable.TableName, dataColumn.ColumnName, System.Data.OleDb.OleDbType.WChar);  
        currentAttribute.NameColumn.Source = new AMO.ColumnBinding(dataTable.TableName, dataColumn.ColumnName);  
        currentAttribute.NameColumn.NullProcessing = AMO.NullProcessing.ZeroOrBlank;  
        currentAttribute.OrderBy = AMO.OrderBy.Key;  
        AMO.AttributeRelationship currentAttributeRelationship = currentDimension.Attributes["RowNumber"].AttributeRelationships.Add(currentAttribute.ID);  
        currentAttributeRelationship.Cardinality = AMO.Cardinality.Many;  
        currentAttributeRelationship.OverrideBehavior = AMO.OverrideBehavior.None;  
    }  
    #endregion  
  
    #region Add Dimension to Model cube  
    cb.Dimensions.Add(tableID, tableID, tableID);  
    #endregion  
  
    #region Add MeasureGroup to Model cube  
    AMO.MeasureGroup currentMeasureGroup = cb.MeasureGroups.Add(tableID, tableID);  
    currentMeasureGroup.StorageMode = AMO.StorageMode.InMemory;  
    currentMeasureGroup.ProcessingMode = AMO.ProcessingMode.Regular;  
  
    //Adding Dimension  
    AMO.DegenerateMeasureGroupDimension currentMGDim = new AMO.DegenerateMeasureGroupDimension(tableID);  
    currentMeasureGroup.Dimensions.Add(currentMGDim);  
    currentMGDim.ShareDimensionStorage = AMO.StorageSharingMode.Shared;  
    currentMGDim.CubeDimensionID = tableID;  
    foreach (AMO.CubeAttribute ca in cb.Dimensions[tableID].Attributes)  
    {  
        AMO.MeasureGroupAttribute mga = new AMO.MeasureGroupAttribute(ca.AttributeID);  
        if (mga.AttributeID == "RowNumber")  
        {  
            mga.Type = AMO.MeasureGroupAttributeType.Granularity;  
            AMO.DataItem rowNumberKeyColumn = new AMO.DataItem(new AMO.ColumnBinding(tableID, "RowNumber"));  
            rowNumberKeyColumn.DataType = System.Data.OleDb.OleDbType.Integer;  
            mga.KeyColumns.Add(rowNumberKeyColumn);  
        }  
        else  
        {  
            foreach (AMO.DataItem di in ca.Attribute.KeyColumns)  
            {  
                AMO.DataItem keyColumn = new AMO.DataItem(new AMO.ColumnBinding(tableID, ((AMO.ColumnBinding)di.Source).ColumnID));  
                keyColumn.DataType = di.DataType;  
                keyColumn.NullProcessing = AMO.NullProcessing.Preserve;  
                keyColumn.InvalidXmlCharacters = AMO.InvalidXmlCharacters.Remove;  
                mga.KeyColumns.Add(keyColumn);  
            }  
        }  
        currentMGDim.Attributes.Add(mga);  
    }  
  
    //Adding default Measure  
    String defaultMeasureID = string.Concat("_Count ", tableID);  
    AMO.Measure currentMeasure = currentMeasureGroup.Measures.Add(defaultMeasureID, defaultMeasureID);  
    currentMeasure.AggregateFunction = AMO.AggregationFunction.Count;  
    currentMeasure.DataType = AMO.MeasureDataType.BigInt;  
    AMO.DataItem currentMeasureSource = new AMO.DataItem(new AMO.RowBinding(tableID));  
    currentMeasureSource.DataType = System.Data.OleDb.OleDbType.BigInt;  
    currentMeasure.Source = currentMeasureSource;  
  
    //Partitions  
    AMO.Partition currentPartition = new AMO.Partition(tableID, tableID);  
    currentPartition.StorageMode = AMO.StorageMode.InMemory;  
    currentPartition.ProcessingMode = AMO.ProcessingMode.Regular;  
    currentPartition.Source = new AMO.QueryBinding(newDatasource.ID, (String)dataTable.ExtendedProperties["sqlStmt"]);  
    currentMeasureGroup.Partitions.Add(currentPartition);  
  
    #endregion  
  
    #region Update new objects in database  
    db.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
    #endregion  
  
    return true;  
}  
  
```  
  
> [!CAUTION]  
>  위 코드 조각에는 오류 발생 시 오류 검사 또는 정리 프로시저가 없습니다.  
  
  
