---
title: Working with Excel Files with the Script Task | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Excel files
- Script task [Integration Services], examples
- Excel [Integration Services]
ms.assetid: b8fa110a-2c9c-4f5a-8fe1-305555640e44
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 46bf53c35663393ad600f02600961cf0295386bf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-excel-files-with-the-script-task"></a>스크립트 태스크를 사용한 Excel 파일 작업
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 파일 형식으로 스프레드시트에 저장된 데이터를 작업하기 위한 Excel 연결 관리자, Excel 원본 및 Excel 대상을 제공합니다. 이 항목에서는 스크립트 태스크를 사용하여 사용 가능한 Excel 데이터베이스(통합 문서 파일) 및 테이블(워크시트 및 명명된 범위)에 대한 정보를 가져오는 기술을 설명합니다. 이러한 예제는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB 공급자가 지원하는 다른 파일 기반 데이터 원본에도 사용할 수 있도록 쉽게 수정할 수 있습니다.  
  
 [예제를 테스트 하기 위한 패키지 구성](#configuring)  
  
 [예제 1: Excel 파일의 존재 여부 확인](#example1)  
  
 [예제 2: Excel 테이블의 존재 여부 확인](#example2)  
  
 [예 3: 폴더의 Excel 파일 목록 가져오기](#example3)  
  
 [예 4: Excel 파일의 테이블 목록 가져오기](#example4)  
  
 [예제 결과 표시합니다.](#testing)  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
##  <a name="configuring"></a>예제를 테스트 하기 위한 패키지 구성  
 단일 패키지에서 이 항목의 모든 예제를 테스트할 수 있도록 구성할 수 있습니다. 이 항목의 예제에서는 대개 동일한 여러 패키지 변수와 동일한 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스를 사용합니다.  
  
#### <a name="to-configure-a-package-for-use-with-the-examples-in-this-topic"></a>패키지를 이 항목의 예에 사용할 수 있도록 구성하려면  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 새 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 프로젝트를 만들고 편집을 위해 기본 패키지를 엽니다.  
  
2.  **변수**합니다. 열기는 **변수** 창 다음 변수를 정의 하 고 있습니다.  
  
    -   `ExcelFile`형식의 **문자열**합니다. 기존 Excel 통합 문서의 전체 경로와 파일 이름을 입력합니다.  
  
    -   `ExcelTable`형식의 **문자열**합니다. 기존 워크시트의 이름이나 `ExcelFile` 변수의 값에 명명된 통합 문서의 명명된 범위를 입력합니다. 이 값은 대/소문자를 구분합니다.  
  
    -   `ExcelFileExists`형식의 **부울**합니다.  
  
    -   `ExcelTableExists`형식의 **부울**합니다.  
  
    -   `ExcelFolder`형식의 **문자열**합니다. 적어도 하나의 Excel 통합 문서가 들어 있는 폴더의 전체 경로를 입력합니다.  
  
    -   `ExcelFiles`형식의 **개체**합니다.  
  
    -   `ExcelTables`형식의 **개체**합니다.  
  
3.  **문 가져오기**합니다. 대부분의 코드 예제에서는 스크립트 파일의 맨 위에서 다음 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 네임스페이스 중 하나 또는 둘 모두를 가져와야 합니다.  
  
    -   **System.IO**, 파일 시스템 작업에 대 한 합니다.  
  
    -   **System.Data.OleDb**을 데이터 소스로 Excel 파일을 엽니다.  
  
4.  **참조**합니다. Excel 파일에서 스키마 정보를 읽는 코드 샘플에는 스크립트 프로젝트에 대 한 추가 참조가 필요는 **System.Xml** 네임 스페이스입니다.  
  
5.  스크립트 구성 요소에 대 한 기본 스크립트 언어를 사용 하 여 설정는 **스크립트 언어** 옵션에 **일반** 의 페이지는 **옵션** 대화 상자. 자세한 내용은 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)을 참조하세요.  
  
##  <a name="example1"></a>예 1 설명: Excel 파일의 존재 여부 확인  
 이 예에서는 `ExcelFile` 변수에 지정된 Excel 통합 문서 파일이 존재하는지 확인한 다음 `ExcelFileExists` 변수의 부울 값을 이 결과로 설정합니다. 이 부울 값은 패키지의 워크플로에서 분기하는 데 사용할 수 있습니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가 하 고 해당 이름을 변경 **ExcelFileExists**합니다.  
  
2.  **스크립트 태스크 편집기**의 **스크립트** 탭을 클릭 **ReadOnlyVariables** 다음 방법 중 하나를 사용 하 여 속성 값을 입력 합니다.  
  
    -   형식 **ExcelFile**합니다.  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자를 선택은 **ExcelFile** 변수입니다.  
  
3.  클릭 **ReadWriteVariables** 다음 방법 중 하나를 사용 하 여 속성 값을 입력 합니다.  
  
    -   형식 **ExcelFileExists**합니다.  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자를 선택은 **ExcelFileExists** 변수입니다.  
  
4.  클릭 **스크립트 편집** 스크립트 편집기를 엽니다.  
  
5.  추가 **Imports** 문에 **System.IO** 스크립트 파일의 맨 위쪽에 네임 스페이스입니다.  
  
6.  다음 코드를 추가합니다.  
  
### <a name="example-1-code"></a>코드 예 1  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    If File.Exists(fileToTest) Then  
      Dts.Variables("ExcelFileExists").Value = True  
    Else  
      Dts.Variables("ExcelFileExists").Value = False  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    string fileToTest;  
  
    fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
    if (File.Exists(fileToTest))  
    {  
      Dts.Variables["ExcelFileExists"].Value = true;  
    }  
    else  
    {  
      Dts.Variables["ExcelFileExists"].Value = false;  
    }  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
##  <a name="example2"></a>예 2 설명: Excel 테이블의 존재 여부 확인  
 이 예에서는 `ExcelTable` 변수에 지정된 Excel 워크시트 또는 명명된 범위가 `ExcelFile` 변수에 지정된 Excel 통합 문서 파일에 있는지 여부를 확인한 다음 `ExcelTableExists` 변수의 부울 값을 이 결과로 설정합니다. 이 부울 값은 패키지의 워크플로에서 분기하는 데 사용할 수 있습니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가 하 고 해당 이름을 변경 **ExcelTableExists**합니다.  
  
2.  **스크립트 태스크 편집기**의 **스크립트** 탭을 클릭 **ReadOnlyVariables** 다음 방법 중 하나를 사용 하 여 속성 값을 입력 합니다.  
  
    -   형식 **ExcelTable** 및 **ExcelFile** 쉼표로 구분 하 여**합니다.**  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자를 선택은 **ExcelTable** 및 **ExcelFile** 변수입니다.  
  
3.  클릭 **ReadWriteVariables** 다음 방법 중 하나를 사용 하 여 속성 값을 입력 합니다.  
  
    -   형식 **ExcelTableExists**합니다.  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자를 선택은 **ExcelTableExists** 변수입니다.  
  
4.  클릭 **스크립트 편집** 스크립트 편집기를 엽니다.  
  
5.  에 대 한 참조 추가 **System.Xml** 스크립트 프로젝트의 어셈블리.  
  
6.  추가 **Imports** 에 대 한 문을 **System.IO** 및 **System.Data.OleDb** 스크립트 파일의 맨 위쪽에 네임 스페이스입니다.  
  
7.  다음 코드를 추가합니다.  
  
### <a name="example-2-code"></a>코드 예 2  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
    Dim tableToTest As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim excelTables As DataTable  
    Dim excelTable As DataRow  
    Dim currentTable As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    tableToTest = Dts.Variables("ExcelTable").Value.ToString  
  
    Dts.Variables("ExcelTableExists").Value = False  
    If File.Exists(fileToTest) Then  
      connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=" & fileToTest & _  
        ";Extended Properties=Excel 8.0"  
      excelConnection = New OleDbConnection(connectionString)  
      excelConnection.Open()  
      excelTables = excelConnection.GetSchema("Tables")  
      For Each excelTable In excelTables.Rows  
        currentTable = excelTable.Item("TABLE_NAME").ToString  
        If currentTable = tableToTest Then  
          Dts.Variables("ExcelTableExists").Value = True  
        End If  
      Next  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
    public void Main()  
        {  
            string fileToTest;  
            string tableToTest;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable excelTables;  
            string currentTable;  
  
            fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
            tableToTest = Dts.Variables["ExcelTable"].Value.ToString();  
  
            Dts.Variables["ExcelTableExists"].Value = false;  
            if (File.Exists(fileToTest))  
            {  
                connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" +  
                "Data Source=" + fileToTest + ";Extended Properties=Excel 8.0";  
                excelConnection = new OleDbConnection(connectionString);  
                excelConnection.Open();  
                excelTables = excelConnection.GetSchema("Tables");  
                foreach (DataRow excelTable in excelTables.Rows)  
                {  
                    currentTable = excelTable["TABLE_NAME"].ToString();  
                    if (currentTable == tableToTest)  
                    {  
                        Dts.Variables["ExcelTableExists"].Value = true;  
                    }  
                }  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
}  
```  
  
##  <a name="example3"></a>예 3 설명: 폴더의 Excel 파일 목록 가져오기  
 이 예에서는 `ExcelFolder` 변수 값에 지정된 폴더에 있는 Excel 파일의 목록으로 배열을 채운 다음 이 배열을 `ExcelFiles` 변수에 복사합니다. Foreach from Variable 열거자를 사용하여 배열의 파일을 반복할 수 있습니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가 하 고 해당 이름을 변경 **GetExcelFiles**합니다.  
  
2.  열기는 **스크립트 태스크 편집기**의 **스크립트** 탭을 클릭 **ReadOnlyVariables** 다음 방법 중 하나를 사용 하 여 속성 값을 입력 합니다.  
  
    -   형식 **ExcelFolder**  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자에서 ExcelFolder 변수를 선택 합니다.  
  
3.  클릭 **ReadWriteVariables** 다음 방법 중 하나를 사용 하 여 속성 값을 입력 합니다.  
  
    -   형식 **ExcelFiles**합니다.  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자에서 ExcelFiles 변수를 선택 합니다.  
  
4.  클릭 **스크립트 편집** 스크립트 편집기를 엽니다.  
  
5.  추가 **Imports** 문에 **System.IO** 스크립트 파일의 맨 위쪽에 네임 스페이스입니다.  
  
6.  다음 코드를 추가합니다.  
  
### <a name="example-3-code"></a>코드 예 3  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const FILE_PATTERN As String = "*.xls"  
  
    Dim excelFolder As String  
    Dim excelFiles As String()  
  
    excelFolder = Dts.Variables("ExcelFolder").Value.ToString  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN)  
  
    Dts.Variables("ExcelFiles").Value = excelFiles  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    const string FILE_PATTERN = "*.xls";  
  
    string excelFolder;  
    string[] excelFiles;  
  
    excelFolder = Dts.Variables["ExcelFolder"].Value.ToString();  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN);  
  
    Dts.Variables["ExcelFiles"].Value = excelFiles;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
### <a name="alternate-solution"></a>대체 솔루션  
 스크립트 태스크를 사용하여 Excel 파일의 목록을 배열로 수집하는 대신 ForEach File 열거자를 사용하여 폴더의 모든 Excel 파일을 반복할 수도 있습니다. 자세한 내용은 참조 [Excel 파일 및 Foreach 루프 컨테이너를 사용 하 여 테이블을 통해 루프](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)합니다.  
  
##  <a name="example4"></a>예 4 설명: Excel 파일의 테이블 목록 가져오기  
 이 예에서는 `ExcelFile` 변수 값으로 지정된 Excel 통합 문서 파일에 있는 워크시트 및 명명된 범위의 목록으로 배열을 채운 다음 이 배열을 `ExcelTables`에 복사합니다. Foreach from Variable 열거자를 사용하여 배열의 테이블을 반복할 수 있습니다.  
  
> [!NOTE]  
>  Excel 통합 문서의 테이블 목록에는 워크시트($ 접미사를 가짐)와 명명된 범위가 모두 포함됩니다. 워크시트만 포함하거나 명명된 범위 목록만 포함하도록 목록을 필터링해야 하는 경우에는 이를 위한 다른 코드를 추가해야 합니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가 하 고 해당 이름을 변경 **GetExcelTables**합니다.  
  
2.  열기는 **스크립트 태스크 편집기**의 **스크립트** 탭을 클릭 **ReadOnlyVariables** 다음 방법 중 하나를 사용 하 여 속성 값을 입력 합니다.  
  
    -   형식 **ExcelFile**합니다.  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자에서 ExcelFile 변수를 선택 합니다.  
  
3.  클릭 **ReadWriteVariables** 다음 방법 중 하나를 사용 하 여 속성 값을 입력 합니다.  
  
    -   형식 **ExcelTables**합니다.  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자는 ExcelTablesvariable를 선택 합니다.  
  
4.  클릭 **스크립트 편집** 스크립트 편집기를 엽니다.  
  
5.  에 대 한 참조 추가 **System.Xml** 스크립트 프로젝트의 네임 스페이스입니다.  
  
6.  추가 **Imports** 문에 **System.Data.OleDb** 스크립트 파일의 맨 위쪽에 네임 스페이스입니다.  
  
7.  다음 코드를 추가합니다.  
  
### <a name="example-4-code"></a>예 4 코드  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim excelFile As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim tablesInFile As DataTable  
    Dim tableCount As Integer = 0  
    Dim tableInFile As DataRow  
    Dim currentTable As String  
    Dim tableIndex As Integer = 0  
  
    Dim excelTables As String()  
  
    excelFile = Dts.Variables("ExcelFile").Value.ToString  
    connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=" & excelFile & _  
        ";Extended Properties=Excel 8.0"  
    excelConnection = New OleDbConnection(connectionString)  
    excelConnection.Open()  
    tablesInFile = excelConnection.GetSchema("Tables")  
    tableCount = tablesInFile.Rows.Count  
    ReDim excelTables(tableCount - 1)  
    For Each tableInFile In tablesInFile.Rows  
      currentTable = tableInFile.Item("TABLE_NAME").ToString  
      excelTables(tableIndex) = currentTable  
      tableIndex += 1  
    Next  
  
    Dts.Variables("ExcelTables").Value = excelTables  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            string excelFile;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable tablesInFile;  
            int tableCount = 0;  
            string currentTable;  
            int tableIndex = 0;  
  
            string[] excelTables = new string[5];  
  
            excelFile = Dts.Variables["ExcelFile"].Value.ToString();  
            connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" +  
                "Data Source=" + excelFile + ";Extended Properties=Excel 8.0";  
            excelConnection = new OleDbConnection(connectionString);  
            excelConnection.Open();  
            tablesInFile = excelConnection.GetSchema("Tables");  
            tableCount = tablesInFile.Rows.Count;  
  
            foreach (DataRow tableInFile in tablesInFile.Rows)  
            {  
                currentTable = tableInFile["TABLE_NAME"].ToString();  
                excelTables[tableIndex] = currentTable;  
                tableIndex += 1;  
            }  
  
            Dts.Variables["ExcelTables"].Value = excelTables;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
### <a name="alternate-solution"></a>대체 솔루션  
 스크립트 태스크를 사용하여 Excel 테이블의 목록을 배열로 수집하는 대신 ForEach ADO.NET 스키마 행 집합 열거자를 사용하여 Excel 통합 문서 파일의 모든 테이블, 즉 워크시트와 명명된 범위를 반복할 수도 있습니다. 자세한 내용은 참조 [Excel 파일 및 Foreach 루프 컨테이너를 사용 하 여 테이블을 통해 루프](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)합니다.  
  
##  <a name="testing"></a>예제 결과 표시합니다.  
 이 항목의 각 예를 동일한 패키지에서 구성한 경우 모든 스크립트 태스크를 모든 예의 출력을 표시하는 추가 스크립트 태스크에 연결할 수 있습니다.  
  
#### <a name="to-configure-a-script-task-to-display-the-output-of-the-examples-in-this-topic"></a>이 항목의 예 출력을 표시하도록 스크립트 태스크를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가 하 고 해당 이름을 변경 **DisplayResults**합니다.  
  
2.  각 태스크가 이전 태스크가 성공적으로 완료 된 후 실행 되도록 네 개의 예 스크립트 태스크를 서로 연결 하 고 네 번째 예 태스크를 연결 된 **DisplayResults** 작업 합니다.  
  
3.  열기는 **DisplayResults** 의 태스크는 **스크립트 태스크 편집기**합니다.  
  
4.  에 **스크립트** 탭을 클릭 **ReadOnlyVariables** 에 나열 된 모든 7 개의 변수를 추가 하려면 다음 방법 중 하나를 사용 하 고 [예제를 테스트 하기 위한 패키지 구성](#configuring):  
  
    -   각 변수의 이름을 쉼표로 구분하여 입력합니다.  
  
         -또는-  
  
    -   줄임표를 클릭 (**... **) 단추 옆 속성 필드는 **변수 선택** 대화 상자에서 변수를 선택 합니다.  
  
5.  클릭 **스크립트 편집** 스크립트 편집기를 엽니다.  
  
6.  추가 **Imports** 에 대 한 문을 **Microsoft.VisualBasic** 및 **System.Windows.Forms** 스크립트 파일의 맨 위쪽에 네임 스페이스입니다.  
  
7.  다음 코드를 추가합니다.  
  
8.  패키지를 실행하고 메시지 상자에 표시된 결과를 확인합니다.  
  
### <a name="code-to-display-the-results"></a>결과를 표시하는 코드  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const EOL As String = ControlChars.CrLf  
  
    Dim results As String  
    Dim filesInFolder As String()  
    Dim fileInFolder As String  
    Dim tablesInFile As String()  
    Dim tableInFile As String  
  
    results = _  
      "Final values of variables:" & EOL & _  
      "ExcelFile: " & Dts.Variables("ExcelFile").Value.ToString & EOL & _  
      "ExcelFileExists: " & Dts.Variables("ExcelFileExists").Value.ToString & EOL & _  
      "ExcelTable: " & Dts.Variables("ExcelTable").Value.ToString & EOL & _  
      "ExcelTableExists: " & Dts.Variables("ExcelTableExists").Value.ToString & EOL & _  
      "ExcelFolder: " & Dts.Variables("ExcelFolder").Value.ToString & EOL & _  
      EOL  
  
    results &= "Excel files in folder: " & EOL  
    filesInFolder = DirectCast(Dts.Variables("ExcelFiles").Value, String())  
    For Each fileInFolder In filesInFolder  
      results &= " " & fileInFolder & EOL  
    Next  
    results &= EOL  
  
    results &= "Excel tables in file: " & EOL  
    tablesInFile = DirectCast(Dts.Variables("ExcelTables").Value, String())  
    For Each tableInFile In tablesInFile  
      results &= " " & tableInFile & EOL  
    Next  
  
    MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information)  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            const string EOL = "\r";  
  
            string results;  
            string[] filesInFolder;  
            //string fileInFolder;  
            string[] tablesInFile;  
            //string tableInFile;  
  
            results = "Final values of variables:" + EOL + "ExcelFile: " + Dts.Variables["ExcelFile"].Value.ToString() + EOL + "ExcelFileExists: " + Dts.Variables["ExcelFileExists"].Value.ToString() + EOL + "ExcelTable: " + Dts.Variables["ExcelTable"].Value.ToString() + EOL + "ExcelTableExists: " + Dts.Variables["ExcelTableExists"].Value.ToString() + EOL + "ExcelFolder: " + Dts.Variables["ExcelFolder"].Value.ToString() + EOL + EOL;  
  
            results += "Excel files in folder: " + EOL;  
            filesInFolder = (string[])(Dts.Variables["ExcelFiles"].Value);  
            foreach (string fileInFolder in filesInFolder)  
            {  
                results += " " + fileInFolder + EOL;  
            }  
            results += EOL;  
  
            results += "Excel tables in file: " + EOL;  
            tablesInFile = (string[])(Dts.Variables["ExcelTables"].Value);  
            foreach (string tableInFile in tablesInFile)  
            {  
                results += " " + tableInFile + EOL;  
            }  
  
            MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Excel 연결 관리자](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
