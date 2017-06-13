---
title: "외부 데이터 집합을 사용 하 여 Reporting Services를 사용한 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataSet objects [Reporting Services]
- data processing extensions [Reporting Services], custom DataSet objects
- custom DataSet objects [Reporting Services]
- external DataSet objects [Reporting Services]
ms.assetid: 11daa013-ec17-4760-80e3-6d84cd8d5722
caps.latest.revision: 49
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1521035e49494a2e183ea35a6ad981a710ff52ff
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="using-an-external-dataset-with-reporting-services"></a>Reporting Services에서 외부 데이터 집합 사용
  **DataSet** 분산 데이터 시나리오를 연결이 끊긴 개체는 지원 하기 위해 핵심 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]합니다. **DataSet** 개체는 데이터 소스에 관계 없이 일관성 있는 관계형 프로그래밍 모델을 제공 하는 데이터의 메모리 상주 표현입니다. 다양한 데이터 원본 또는 XML 데이터와 함께 사용하거나 응용 프로그램의 로컬 데이터를 관리하는 데 사용할 수 있습니다. **DataSet** 개체 관련된 테이블, 제약 조건 및 테이블 간의 관계를 포함 하 여 데이터의 전체 집합을 나타냅니다. 때문에 **DataSet** 저장 하 고 표시할 데이터를 데이터에 개체의 다양 한 기능 종종 처리 방식과로 변환 될 수 있습니다는 **데이터 집합** 발생 해당 데이터에 보고 하기 전에 개체입니다.  
  
 와 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 사용자 지정을 통합할 수 있습니다 **DataSet** 외부 응용 프로그램에서 만들어지는 개체입니다. 에 사용자 지정 데이터 처리 확장 프로그램을 만들면이를 위해 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 사이의 다리 처럼 작동 하 여 **데이터 집합** 개체와 보고서 서버. 이 처리 하기 위한 코드의 대부분 **데이터 집합** 개체에 포함 되어는 **DataReader** 만드는 클래스입니다.  
  
 노출 하는 첫 번째 단계는 프로그램 **데이터 집합** 에서 공급자별 메서드를 구현 하는 개체를 보고서 서버 프로그램 **DataReader** 채울 수 있는 클래스는 **데이터 집합** 개체입니다. 정적 데이터를 로드 하는 방법을 보여 주는 다음 예제는 **DataSet** 에서 공급자별 메서드를 사용 하 여 개체 프로그램 **DataReader** 클래스입니다.  
  
```vb  
'Private members of the DataReader class  
Private m_dataSet As System.Data.DataSet  
Private m_currentRow As Integer  
  
'Method to create a dataset  
Friend Sub CreateDataSet()  
   ' Create a dataset.  
   Dim ds As New System.Data.DataSet("myDataSet")  
   ' Create a data table.   
   Dim dt As New System.Data.DataTable("myTable")  
   ' Create a data column and set various properties.   
   Dim dc As New System.Data.DataColumn()  
   dc.DataType = System.Type.GetType("System.Decimal")  
   dc.AllowDBNull = False  
   dc.Caption = "Number"  
   dc.ColumnName = "Number"  
   dc.DefaultValue = 25  
   ' Add the column to the table.   
   dt.Columns.Add(dc)  
   ' Add 10 rows and set values.   
   Dim dr As System.Data.DataRow  
   Dim i As Integer  
   For i = 0 To 9  
      dr = dt.NewRow()  
      dr("Number") = i + 1  
      ' Be sure to add the new row to the DataRowCollection.   
      dt.Rows.Add(dr)  
   Next i  
  
   ' Fill the dataset.  
   ds.Tables.Add(dt)  
  
   ' Use a private variable to store the dataset in your  
   ' DataReader.  
   m_dataSet = ds  
  
   ' Set the current row to -1.  
   m_currentRow = - 1  
End Sub 'CreateDataSet  
```  
  
```csharp  
// Private members of the DataReader class  
private System.Data.DataSet m_dataSet;  
private int m_currentRow;  
  
// Method to create a dataset  
internal void CreateDataSet()  
{  
   // Create a dataset.  
   System.Data.DataSet ds = new System.Data.DataSet("myDataSet");  
   // Create a data table.   
   System.Data.DataTable dt = new System.Data.DataTable("myTable");  
   // Create a data column and set various properties.   
   System.Data.DataColumn dc = new System.Data.DataColumn();   
   dc.DataType = System.Type.GetType("System.Decimal");   
   dc.AllowDBNull = false;   
   dc.Caption = "Number";   
   dc.ColumnName = "Number";   
   dc.DefaultValue = 25;   
   // Add the column to the table.   
   dt.Columns.Add(dc);   
   // Add 10 rows and set values.   
   System.Data.DataRow dr;   
   for(int i = 0; i < 10; i++)  
   {   
      dr = dt.NewRow();   
      dr["Number"] = i + 1;   
      // Be sure to add the new row to the DataRowCollection.   
      dt.Rows.Add(dr);  
   }  
  
   // Fill the dataset.  
   ds.Tables.Add(dt);  
  
   // Use a private variable to store the dataset in your  
   // DataReader.  
   m_dataSet = ds;  
  
   // Set the current row to -1.  
   m_currentRow = -1;  
}  
```  
  
```csharp  
public bool Read()  
{  
   m_currentRow++;  
   if (m_currentRow >= m_dataSet.Tables[0].Rows.Count)   
   {  
      return (false);  
   }   
   else   
   {  
      return (true);  
   }  
}  
  
public int FieldCount  
{  
   // Return the count of the number of columns, which in  
   // this case is the size of the column metadata  
   // array.  
   get { return m_dataSet.Tables[0].Columns.Count; }  
}  
  
public string GetName(int i)  
{  
   return m_dataSet.Tables[0].Columns[i].ColumnName;  
}  
  
public Type GetFieldType(int i)  
{  
   // Return the actual Type class for the data type.  
   return m_dataSet.Tables[0].Columns[i].DataType;  
}  
  
public Object GetValue(int i)  
{  
   return m_dataSet.Tables[0].Rows[m_currentRow][i];  
}  
  
public int GetOrdinal(string name)  
{  
   // Look for the ordinal of the column with the same name and return it.  
   // Returns -1 if not found.  
   return m_dataSet.Tables[0].Columns[name].Ordinal;  
}  
```  
  
 만들거나 데이터 집합을 검색 한 후 사용할 수 있습니다는 **DataSet** 구현에는 개체는 **읽기**, **GetValue**, **GetName**, **GetOrdinal**, **GetFieldType**, 및 **FieldCount** 의 멤버는 **DataReader** 클래스입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
