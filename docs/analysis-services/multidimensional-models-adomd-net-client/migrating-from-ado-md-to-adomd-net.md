---
title: ADO MD에서 ADOMD.NET으로 마이그레이션 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dc5c88301ac6d777372c66a3e702710ae45b7177
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-from-ado-md-to-adomdnet"></a>ADO MD에서 ADOMD.NET으로 마이그레이션
  ADOMD.NET 라이브러리는 COM(구성 요소 개체 모델) 기반 클라이언트 응용 프로그램의 다차원 데이터에 액세스하는 데 사용되는 ADO(ActiveX Data Objects) 라이브러리의 확장인 ADO MD(ActiveX Data Objects Multidimensional) 라이브러리와 비슷합니다. ADO MD는 C++ 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic과 같은 관리되지 않는 언어의 다차원 데이터에 쉽게 액세스할 수 있은 방법을 제공합니다. ADOMD.NET은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] C# 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET과 같은 관리되는 언어의 분석(다차원 및 데이터 마이닝) 데이터에 쉽게 액세스할 수 있는 방법을 제공합니다. 또한 향상된 메타데이터 개체 모델도 제공합니다.  
  
 기존 클라이언트 응용 프로그램을 ADO MD에서 ADOMD.NET으로 마이그레이션하는 과정은 간단하지만 마이그레이션과 관련하여 몇 가지 중요한 차이점이 있습니다.  
  
 **클라이언트 응용 프로그램에 대 한 연결 및 데이터 액세스를 제공 하려면**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Adodb.dll 및 Adomd.dll에 대한 참조가 필요합니다.|Microsoft.AnalysisServices.AdomdClient.dll에 대한 단일 참조가 필요합니다.|  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 클래스는 연결 지원과 메타데이터에 대한 액세스를 제공합니다.  
  
 **다차원 개체에 대 한 메타 데이터를 검색**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|카탈로그 클래스를 사용 합니다.|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A>의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 속성을 사용합니다.|  
  
 **개체 쿼리를 실행 하 고 셀 집합을 반환 하려면**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|셀 집합 클래스를 사용 합니다.|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 클래스를 사용합니다.|  
  
 **셀 집합을 표시 하는 데 사용 되는 메타 데이터에 액세스 하려면**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|위치 클래스를 사용 합니다.|<xref:Microsoft.AnalysisServices.AdomdClient.Set> 및 <xref:Microsoft.AnalysisServices.AdomdClient.Tuple> 개체를 사용합니다.|  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdClient.Position> 클래스는 이전 버전과의 호환성을 위해 지원됩니다.  
  
 **마이닝 모델 메타 데이터를 검색**  
 ADO MD에서 클래스가 제공 됩니다. ADOMD.NET에서 데이터 마이닝 컬렉션 중 하나를 사용 합니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection>에는 데이터 원본의 모든 마이닝 모델 목록이 들어 있습니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection>은 사용 가능한 마이닝 알고리즘에 대한 정보를 제공합니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection>은 서버의 마이닝 구조에 대한 정보를 표시합니다.  
  
 이러한 차이점을 보여 주기 위해 다음 마이그레이션 예제에서는 기존 ADO MD 응용 프로그램과 이와 동일한 기능을 수행하는 ADOMD.NET 응용 프로그램을 비교합니다.  
  
## <a name="looking-at-a-migration-example"></a>마이그레이션 예제 보기  
 이 섹션에서 설명하는 기존 ADO MD 코드 예제와 이와 동일한 기능을 수행하는 ADOMD.NET 코드 예제는 연결을 만들고, MDX(Multidimensional Expressions) 문을 실행하며, 메타데이터 및 데이터를 검색하는 동일한 동작을 수행합니다. 그러나 두 코드 집합은 서로 다른 개체를 사용하여 태스크를 수행합니다.  
  
### <a name="existing-ado-md-code"></a>기존 ADO MD 코드  
 ADO MD 2.8 설명서에서 가져온 다음 코드 예제에서는 작성 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic® 6.0 및 ADO MD를 사용 하 여 연결 하 고 쿼리 하는 방법을 보여 주기 위해는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본입니다. 이 ADO MD 예제는 다음과 같은 개체를 사용합니다.  
  
-   연결을 만듭니다는 **카탈로그** 개체입니다.  
  
-   사용 하 여 MDX (Multidimensional Expressions) 문 실행에서 **셀 집합** 개체입니다.  
  
-   메타 데이터와 데이터를 검색 된 **위치** 에서 검색 된 개체는 **셀 집합** 개체입니다.  
  
```  
Private Sub cmdCellSettoDebugWindow_Click()  
Dim cat As New ADOMD.Catalog  
Dim cst As New ADOMD.Cellset  
Dim i As Integer  
Dim j As Integer  
Dim k As Integer  
Dim strServer As String  
Dim strSource As String  
Dim strColumnHeader As String  
Dim strRowText As String  
  
On Error GoTo Error_cmdCellSettoDebugWindow_Click  
Screen.MousePointer = vbHourglass  
'*-----------------------------------------------------------------------  
'* Set server to local host.  
'*-----------------------------------------------------------------------  
    strServer = "LOCALHOST"  
  
'*-----------------------------------------------------------------------  
'* Set MDX query string source.  
'*-----------------------------------------------------------------------  
    strSource = strSource & "SELECT "  
    strSource = strSource & "{[Measures].members} ON COLUMNS,"  
    strSource = strSource & _  
        "NON EMPTY [Store].[Store City].members ON ROWS"  
    strSource = strSource & " FROM Sales"  
  
'*-----------------------------------------------------------------------  
'* Set active connection.  
'*-----------------------------------------------------------------------  
        cat.ActiveConnection = "Data Source=" & strServer & _  
            ";Provider=msolap;"  
  
'*-----------------------------------------------------------------------  
'* Set cellset source to MDX query string.  
'*-----------------------------------------------------------------------  
        cst.Source = strSource  
  
'*-----------------------------------------------------------------------  
'* Set cellset active connection to current connection  
'*-----------------------------------------------------------------------  
    Set cst.ActiveConnection = cat.ActiveConnection  
  
'*-----------------------------------------------------------------------  
'* Open cellset.  
'*-----------------------------------------------------------------------  
    cst.Open  
  
'*-----------------------------------------------------------------------  
'* Allow space for row header text.  
'*-----------------------------------------------------------------------  
strColumnHeader = vbTab & vbTab & vbTab & vbTab & vbTab & vbTab  
  
'*-----------------------------------------------------------------------  
'* Loop through column headers.  
'*-----------------------------------------------------------------------  
       For i = 0 To cst.Axes(0).Positions.Count - 1  
            strColumnHeader = strColumnHeader & _  
                cst.Axes(0).Positions(i).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
       Next  
       Debug.Print vbTab & strColumnHeader & vbCrLf  
  
'*-----------------------------------------------------------------------  
'* Loop through row headers and provide data for each row.  
'*-----------------------------------------------------------------------  
        strRowText = ""  
        For j = 0 To cst.Axes(1).Positions.Count - 1  
            strRowText = strRowText & _  
                cst.Axes(1).Positions(j).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
            For k = 0 To cst.Axes(0).Positions.Count - 1  
                strRowText = strRowText & cst(k, j).FormattedValue & _  
                    vbTab & vbTab & vbTab & vbTab  
            Next  
            Debug.Print strRowText & vbCrLf  
            strRowText = ""  
        Next  
  
    Screen.MousePointer = vbDefault  
Exit Sub  
  
Error_cmdCellSettoDebugWindow_Click:  
   Beep  
   Screen.MousePointer = vbDefault  
   MsgBox "The following error has occurred:" & vbCrLf & _  
      Err.Description, vbCritical, " Error!"  
   Exit Sub  
End Sub  
```  
  
### <a name="equivalent-adomdnet-code"></a>동일한 기능을 수행하는 ADOMD.NET 코드  
 Visual Basic .NET으로 작성되었으며 ADOMD.NET을 사용하는 다음 예제는 이전 Visual Basic 6.0 예제와 같은 동작을 수행하는 방법을 보여 줍니다. 다음 예제와 이전 ADO MD 예제의 주요 차이점은 동작을 수행하는 데 사용되는 개체가 다르다는 것입니다. ADOMD.NET 예제는 다음과 같은 개체를 사용합니다.  
  
-   연결을 만듭니다는 **AdomdConnection** 개체입니다.  
  
-   사용 하 여 MDX 문을 실행 한 **AdomdCommand** 개체입니다.  
  
-   메타 데이터와 데이터를 검색 된 **설정** 에서 검색 된 개체는 **셀 집합** 개체입니다.  
  
```  
Private Sub DisplayCellSetInOutputWindow()  
    Dim conn As AdomdConnection  
    Dim cmd As AdomdCommand  
    Dim cst As CellSet  
    Dim i As Integer  
    Dim j As Integer  
    Dim k As Integer  
    Dim strServer As String = "LOCALHOST"  
    Dim strSource As String = "SELECT [Measures].members ON COLUMNS, " & _  
        "NON EMPTY [Store].[Store City].members ON ROWS FROM SALES"  
    Dim strOutput As New System.IO.StringWriter  
  
    '*-----------------------------------------------------------------------  
    '* Open connection.  
    '*-----------------------------------------------------------------------  
    Try  
        ' Create a new AdomdConnection object, providing the connection  
        ' string.  
        conn = New AdomdConnection("Data Source=" & strServer & _  
        ";Provider=msolap;")  
        ' Open the connection.  
        conn.Open()  
    Catch ex As Exception  
        Throw New ApplicationException( _  
            "An error occurred while connecting.")  
    End Try  
  
    Try  
    '*-----------------------------------------------------------------------  
    '* Open cellset.  
    '*-----------------------------------------------------------------------  
        ' Create a new AdomdCommand object, providing the MDX query string.  
        cmd = New AdomdCommand(strSource, conn)  
        ' Run the command and return a CellSet object.  
        cst = cmd.ExecuteCellSet()  
  
    '*-----------------------------------------------------------------------  
    '* Concatenate output.  
    '*-----------------------------------------------------------------------  
  
    ' Include spacing to account for row headers.  
    strOutput.Write(vbTab, 6)  
  
    ' Iterate through the first axis of the CellSet object and  
    ' retrieve column headers.  
    For i = 0 To cst.Axes(0).Set.Tuples.Count - 1  
        strOutput.Write(cst.Axes(0).Set.Tuples(i).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
    Next  
    strOutput.WriteLine()  
  
    ' Iterate through the second axis of the CellSet object and  
    ' retrieve row headers and cell data.  
    For j = 0 To cst.Axes(1).Set.Tuples.Count - 1  
        ' Append the row header.  
        strOutput.Write(cst.Axes(1).Set.Tuples(j).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
  
        ' Append the cell data for that row.  
        For k = 0 To cst.Axes(0).Set.Tuples.Count - 1  
            strOutput.Write(cst.Cells(k, j).FormattedValue)  
            strOutput.Write(vbTab, 4)  
        Next  
        strOutput.WriteLine()  
    Next  
  
    ' Display the output.  
    Debug.WriteLine(strOutput.ToString)  
  
    '*-----------------------------------------------------------------------  
    '* Release resources.  
    '*-----------------------------------------------------------------------  
        conn.Close()  
    Catch ex As Exception  
        ' Ignore or handle errors.  
    Finally  
        cst = Nothing  
        cmd = Nothing  
        conn = Nothing  
    End Try  
End Sub  
```  
  
  
