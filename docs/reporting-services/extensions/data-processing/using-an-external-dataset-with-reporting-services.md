---
title: Reporting Services에서 외부 데이터 집합 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: afcf3dd2d15f38b3c7f54e6facbd4692cc1db899
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33016280"
---
# <a name="using-an-external-dataset-with-reporting-services"></a>Reporting Services에서 외부 데이터 집합 사용
  **DataSet** 개체는 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]에서 연결이 끊긴 분산 데이터 시나리오를 지원하는 데 있어 핵심적인 역할을 합니다. **DataSet** 개체는 데이터 원본과 상관없이 일관성 있는 관계형 프로그래밍 모델을 제공하는 데이터의 메모리 상주 표현입니다. 다양한 데이터 원본 또는 XML 데이터와 함께 사용하거나 응용 프로그램의 로컬 데이터를 관리하는 데 사용할 수 있습니다. **DataSet** 개체는 관련 테이블, 제약 조건, 테이블 간의 관계 등을 포함한 전체 데이터 집합을 나타냅니다. **DataSet** 개체는 데이터를 유연하게 저장하고 표시할 수 있기 때문에 데이터에 대한 보고가 이루어지기 전에 데이터가 처리되고 **DataSet** 개체로 변환되는 경우도 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 사용하여 외부 응용 프로그램으로 만든 사용자 지정 **DataSet** 개체를 통합할 수 있습니다. 그러려면 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 **DataSet** 개체와 보고서 서버를 연결하는 사용자 지정 데이터 처리 확장 프로그램을 만듭니다. 이 **DataSet** 개체를 처리하기 위한 코드의 대부분은 사용자가 만드는 **DataReader** 클래스에 포함됩니다.  
  
 **DataSet** 개체를 보고서 서버에 표시하는 첫 단계는 **DataReader** 클래스에서 **DataSet** 개체를 채울 수 있는 공급자별 메서드를 구현하는 것입니다. 다음 예는 **DataReader** 클래스에서 공급자별 메서드를 사용하여 **DataSet** 개체에 정적 데이터를 로드하는 방법을 보여 줍니다.  
  
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
  
 데이터 집합을 만들거나 검색하면 **DataReader** 클래스의 **Read**, **GetValue**, **GetName**, **GetOrdinal**, **GetFieldType** 및 **FieldCount** 멤버 구현에서 **DataSet** 개체를 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
