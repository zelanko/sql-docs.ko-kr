---
title: AdomdDataReader를 사용 하 여 데이터를 검색 합니다. | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9c52978621631f263011d0340f8d9b67b971ea10
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="retrieving-data-using-the-adomddatareader"></a>AdomdDataReader를 사용하여 데이터 검색
  분석 데이터 검색 시 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체는 오버헤드와 상호 작용 간에 적절한 균형을 맞춥니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체는 분석 데이터 원본에서 정방향 및 읽기 전용의 평면화된 데이터 스트림을 검색합니다. 이 버퍼링되지 않은 데이터 스트림을 사용하면 절차적인 논리에서 분석 데이터 원본의 결과를 순차적으로 처리할 수 있습니다. 따라서 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>는 데이터가 메모리에 캐시되지 않기 때문에 표시를 목적으로 많은 양의 데이터를 검색할 때 유용하게 사용할 수 있습니다.  
  
 또한 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>는 쿼리의 전체 결과가 반환될 때까지 기다리지 않고 사용 가능한 데이터를 바로 검색하기 때문에 응용 프로그램 성능을 높일 수 있으며, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 도 기본적으로이 판독기에서는 메모리에 한 번에 하나의 행을 저장 하기 때문에 시스템 오버 헤드를 감소 합니다.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체는 성능을 최적화하지만 검색된 데이터에 대해 제공하는 정보량이 다른 데이터 검색 메서드보다 적습니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체는 데이터 또는 메타데이터를 나타내기 위한 큰 개체 모델을 지원하지 않으며 이 개체 모델에는 셀 쓰기 저장(writeback)과 같이 복잡한 분석 기능도 사용할 수 없습니다. 하지만 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체는 셀 집합 데이터를 검색하는 강력한 형식의 메서드 집합과 셀 집합 메타데이터를 테이블 형식으로 검색하는 메서드를 제공합니다. 또한 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 구현 하는 **지** 데이터 바인딩을 지원 하 고 사용 하 여 데이터를 검색 하기 위한 인터페이스는 **SelectCommand** 메서드를에서 **System.Data**  Microsoft.NET Framework 클래스 라이브러리의 네임 스페이스입니다.  
  
## <a name="retrieving-data-from-the-adomddatareader"></a>AdomdDataReader에서 데이터 검색  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체를 사용하여 데이터를 검색하려면 다음 단계를 수행하십시오.  
  
1.  **개체의 새 인스턴스를 만듭니다.**  
  
     <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 클래스의 새 인스턴스를 만들려면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 메서드를 호출합니다.  
  
2.  **데이터를 검색 합니다.**  
  
     ADOMD.NET에 결과 반환 쿼리 명령이 실행 되는 **결과 집합** 형식으로 테이블 형식에 대 한 데이터를 병합 하려면 XML for Analysis 사양에에서 설명 된 대로 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체입니다. 테이블 형식은 분석 데이터의 일정하지 않은 차원 때문에 분석 데이터 쿼리에는 잘 사용되지 않습니다.  
  
     다음 메서드 중 하나를 사용하여 테이블 형식의 결과를 요청할 때까지 ADOMD.NET은 클라이언트의 네트워크 버퍼에 결과를 저장합니다.  
  
    -   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Read%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 메서드를 호출합니다.  
  
         <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Read%2A> 메서드는 쿼리 결과에서 행을 가져옵니다. 이름 또는 열의 서 수 참조를 전달할 수 있습니다는 [항목](https://msdn.microsoft.com/en-us/library/ms131793(v=sql.130).aspx) 속성을 반환된 된 행의 각 열에 액세스 합니다. 예를 들어 현재 행의 첫째 열 이름이 ColumnName인 경우 `reader[0].ToString()` 또는 `reader["ColumnName"].ToString()`은 현재 행의 첫째 열에 있는 내용을 반환합니다.  
  
    -   형식화된 접근자 메서드 중 하나를 호출합니다.  
  
         <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>에서 제공하는 일련의 형식화된 접근자 메서드를 사용하여 네이티브 데이터 형식으로 열 값에 액세스할 수 있습니다. 열 값의 기본 데이터 형식을 알고 있으면 형식화된 접근자 메서드에서 열 값을 검색할 때 수행해야 하는 형식 변환이 줄기 때문에 최고의 높은 성능을 얻을 수 있습니다.  
  
         사용할 수 있는 형식화된 접근자 메서드로는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDateTime%2A>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDouble%2A>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetInt32%2A> 등이 있습니다. 형식화된 접근자 메서드의 전체 목록은 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>를 참조하십시오.  
  
3.  **판독기를 닫습니다.**  
  
     <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Close%2A> 개체의 사용을 마친 후에는 항상 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 메서드를 호출해야 합니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체의 인스턴스가 열려 있으면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>은 해당 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>에서 배타적으로 사용됩니다. 인스턴스의 모든 명령을 실행할 수 없게 됩니다는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, 하는 등 다른 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 또는 **System.Xml.XmlReader**원래를 닫을 때까지, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>합니다.  
  
### <a name="example-of-retrieving-data-from-the-adomddatareader"></a>AdomdDataReader에서 데이터 검색 예  
 다음 코드 예제에서는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체를 반복한 후 각 행의 처음 두 값을 문자열로 반환합니다.  
  
```vb  
If Reader.HasRows Then  
    Do While objReader.Read()  
        Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
            objReader.GetString(0), objReader.GetString(1))  
    Loop  
Else  
  Console.WriteLine("No rows returned.")  
End If  
  
objReader.Close()  
```  
  
```csharp  
if (objReader.HasRows)  
  while (objReader.Read())  
    Console.WriteLine("\t{0}\t{1}", _  
        objReader.GetString(0), objReader.GetString(1));  
else  
  Console.WriteLine("No rows returned.");  
  
objReader.Close();  
```  
  
## <a name="retrieving-metadata-from-the-adomddatareader"></a>AdomdDataReader에서 메타데이터 검색  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체의 인스턴스가 열려 있는 동안 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetSchemaTable%2A> 메서드를 사용하여 현재 레코드 집합에 대한 스키마 정보 또는 메타데이터를 검색할 수 있습니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetSchemaTable%2A>반환 된 **DataTable** 현재 레코드 집합에 대 한 스키마 정보로 채워지는 개체입니다. **DataTable**은 레코드 집합의 열마다 행을 하나씩 포함합니다. 스키마 테이블 행의 각 열은 셀 집합에서 반환된 열의 속성에 매핑됩니다. 여기서 **ColumnName**은 속성의 이름이며, 열의 값은 속성의 값입니다.  
  
### <a name="example-of-retrieving-metadata-from-the-adomddatareader"></a>AdomdDataReader에서 메타데이터 검색 예  
 다음 코드 예제에서는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체에 대한 스키마 정보를 작성합니다.  
  
```vb  
Dim schemaTable As DataTable = objReader.GetSchemaTable()  
  
Dim objRow As DataRow  
Dim objColumn As DataColumn  
  
For Each objRow In schemaTable.Rows  
  For Each objColumn In schemaTable.Columns  
    Console.WriteLine(objColumn.ColumnName & " = " & objRow(objColumn).ToString())  
  Next  
  Console.WriteLine()  
Next  
DataTable schemaTable = objReader.GetSchemaTable();  
```  
  
```csharp  
foreach (DataRow objRow in schemaTable.Rows)  
{  
  foreach (DataColumn objColumn in schemaTable.Columns)  
    Console.WriteLine(objColumn.ColumnName + " = " + objRow[objColumn]);  
  Console.WriteLine();  
}  
```  
  
## <a name="retrieving-multiple-result-sets"></a>다중 결과 집합 검색  
 데이터 마이닝은 ADOMD.NET에서 중첩 행 집합으로 표시되는 중첩 테이블이라는 개념을 지원합니다. 각 행에 연결된 중첩 행 집합을 검색하려면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDataReader%2A> 메서드를 호출합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [분석 데이터 원본에서 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [셀 집합을 사용 하 여 데이터를 검색 합니다.](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)   
 [XmlReader를 사용 하 여 데이터를 검색 합니다.](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)  
  
  
