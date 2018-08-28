---
title: 스크립트 태스크를 사용한 Excel 파일 작업 | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 9c2edfdfde4bf02097e9a4470e21cbefd68aa2f3
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40405722"
---
# <a name="working-with-excel-files-with-the-script-task"></a>스크립트 태스크를 사용한 Excel 파일 작업
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 파일 형식으로 스프레드시트에 저장된 데이터를 작업하기 위한 Excel 연결 관리자, Excel 원본 및 Excel 대상을 제공합니다. 이 항목에서는 스크립트 태스크를 사용하여 사용 가능한 Excel 데이터베이스(통합 문서 파일) 및 테이블(워크시트 및 명명된 범위)에 대한 정보를 가져오는 기술을 설명합니다.
  
> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.
 
> [!TIP]  
>  여러 패키지에서 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  

##  <a name="configuring"></a> 예제를 테스트하기 위한 패키지 구성  
 단일 패키지에서 이 항목의 모든 예제를 테스트할 수 있도록 구성할 수 있습니다. 이 항목의 예제에서는 대개 동일한 여러 패키지 변수와 동일한 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스를 사용합니다.  
  
### <a name="to-configure-a-package-for-use-with-the-examples-in-this-topic"></a>패키지를 이 항목의 예에 사용할 수 있도록 구성하려면  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 새 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 프로젝트를 만들고 편집을 위해 기본 패키지를 엽니다.  
  
2.  **변수**. **변수** 창을 열고 다음 변수를 정의합니다.  
  
    -   `ExcelFile`, **String** 형식. 기존 Excel 통합 문서의 전체 경로와 파일 이름을 입력합니다.  
  
    -   `ExcelTable`, **String** 형식. 기존 워크시트의 이름이나 `ExcelFile` 변수의 값에 명명된 통합 문서의 명명된 범위를 입력합니다. 이 값은 대/소문자를 구분합니다.  
  
    -   `ExcelFileExists`, **Boolean** 형식.  
  
    -   `ExcelTableExists`, **Boolean** 형식.  
  
    -   `ExcelFolder`, **String** 형식. 적어도 하나의 Excel 통합 문서가 들어 있는 폴더의 전체 경로를 입력합니다.  
  
    -   `ExcelFiles`, **Object** 형식.  
  
    -   `ExcelTables`, **Object** 형식.  
  
3.  **Imports 문**. 대부분의 코드 예제에서는 스크립트 파일의 맨 위에서 다음 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 네임스페이스 중 하나 또는 둘 모두를 가져와야 합니다.  
  
    -   **System.IO** - 파일 시스템 작업의 경우  
  
    -   **System.Data.OleDb** - Excel 파일을 데이터 원본으로 열려는 경우  
  
4.  **References**. Excel 파일에서 스키마 정보를 읽는 코드 예제에는 스크립트 프로젝트에는 **System.Xml** 네임스페이스에 대한 추가 참조가 필요합니다.  
  
5.  **옵션** 대화 상자의 **일반** 페이지에 있는 **스크립트 언어** 옵션을 사용하여 스크립트 구성 요소에 대한 기본 스크립트 언어를 설정합니다. 자세한 내용은 [General Page](../general-page-of-integration-services-designers-options.md)을 참조하세요.  
  
##  <a name="example1"></a> 예 1 설명: Excel 파일의 존재 여부 확인  
 이 예에서는 `ExcelFile` 변수에 지정된 Excel 통합 문서 파일이 존재하는지 확인한 다음 `ExcelFileExists` 변수의 부울 값을 이 결과로 설정합니다. 이 부울 값은 패키지의 워크플로에서 분기하는 데 사용할 수 있습니다.  
  
### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가하고 해당 이름을 **ExcelFileExists**로 바꿉니다.  
  
2.  **스크립트 태스크 편집기**의 **스크립트** 탭에서 **ReadOnlyVariables**를 클릭하고 다음 방법 중 하나를 사용하여 속성 값을 입력합니다.  
  
    -   **ExcelFile**을 입력합니다.  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 **ExcelFile** 변수를 선택합니다.  
  
3.  **ReadWriteVariables**를 클릭하고 다음 방법 중 하나를 사용하여 속성 값을 입력합니다.  
  
    -   **ExcelFileExists**를 입력합니다.  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 **ExcelFileExists** 변수를 선택합니다.  
  
4.  **스크립트 편집**을 클릭하여 스크립트 편집기를 엽니다.  
  
5.  **System.IO** 네임스페이스에 대한 **Imports** 문을 스크립트 파일의 맨 위에 추가합니다.  
  
6.  다음 코드를 추가합니다.  
  
### <a name="example-1-code"></a>예 1 코드  
  
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
  
##  <a name="example2"></a> 예 2 설명: Excel 테이블의 존재 여부 확인  
 이 예에서는 `ExcelTable` 변수에 지정된 Excel 워크시트 또는 명명된 범위가 `ExcelFile` 변수에 지정된 Excel 통합 문서 파일에 있는지 여부를 확인한 다음 `ExcelTableExists` 변수의 부울 값을 이 결과로 설정합니다. 이 부울 값은 패키지의 워크플로에서 분기하는 데 사용할 수 있습니다.  
  
### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가하고 해당 이름을 **ExcelTableExists**로 바꿉니다.  
  
2.  **스크립트 태스크 편집기**의 **스크립트** 탭에서 **ReadOnlyVariables**를 클릭하고 다음 방법 중 하나를 사용하여 속성 값을 입력합니다.  
  
    -   **ExcelTable** 및 **ExcelFile**을 쉼표로 구분하여 입력합니다 **.**  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 **ExcelTable** 및 **ExcelFile** 변수를 선택합니다.  
  
3.  **ReadWriteVariables**를 클릭하고 다음 방법 중 하나를 사용하여 속성 값을 입력합니다.  
  
    -   **ExcelTableExists**를 입력합니다.  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 **ExcelTableExists** 변수를 선택합니다.  
  
4.  **스크립트 편집**을 클릭하여 스크립트 편집기를 엽니다.  
  
5.  스크립트 프로젝트에 **System.Xml** 어셈블리에 대한 참조를 추가합니다.  
  
6.  **System.IO** 및 **System.Data.OleDb** 네임스페이스에 대한 **Imports** 문을 스크립트 파일 맨 위에 추가합니다.  
  
7.  다음 코드를 추가합니다.  
  
### <a name="example-2-code"></a>예 2 코드  
  
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
      connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" & _  
        "Data Source=" & fileToTest & _  
        ";Extended Properties=Excel 12.0"  
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
                connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" +  
                "Data Source=" + fileToTest + ";Extended Properties=Excel 12.0";  
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
  
##  <a name="example3"></a> 예 3 설명: 폴더의 Excel 파일 목록 가져오기  
 이 예에서는 `ExcelFolder` 변수 값에 지정된 폴더에 있는 Excel 파일의 목록으로 배열을 채운 다음 이 배열을 `ExcelFiles` 변수에 복사합니다. Foreach from Variable 열거자를 사용하여 배열의 파일을 반복할 수 있습니다.  
  
### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가하고 해당 이름을 **GetExcelFiles**로 바꿉니다.  
  
2.  **스크립트 태스크 편집기**를 열고 **스크립트** 탭에서 **ReadOnlyVariables**를 클릭한 후 다음 방법 중 하나를 사용하여 속성 값을 입력합니다.  
  
    -   **ExcelFolder**를 입력합니다.  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 ExcelFolder 변수를 선택합니다.  
  
3.  **ReadWriteVariables**를 클릭하고 다음 방법 중 하나를 사용하여 속성 값을 입력합니다.  
  
    -   **ExcelFiles**를 입력합니다.  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 ExcelFiles 변수를 선택합니다.  
  
4.  **스크립트 편집**을 클릭하여 스크립트 편집기를 엽니다.  
  
5.  **System.IO** 네임스페이스에 대한 **Imports** 문을 스크립트 파일의 맨 위에 추가합니다.  
  
6.  다음 코드를 추가합니다.  
  
### <a name="example-3-code"></a>예 3 코드  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const FILE_PATTERN As String = "*.xlsx"  
  
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
    const string FILE_PATTERN = "*.xlsx";  
  
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
 스크립트 태스크를 사용하여 Excel 파일의 목록을 배열로 수집하는 대신 ForEach File 열거자를 사용하여 폴더의 모든 Excel 파일을 반복할 수도 있습니다. 자세한 내용은 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)을 참조하세요.  
  
##  <a name="example4"></a> 예 4 설명: Excel 파일의 테이블 목록 가져오기  
 이 예에서는 `ExcelFile` 변수 값으로 지정된 Excel 통합 문서 파일에 있는 워크시트 및 명명된 범위의 목록으로 배열을 채운 다음 이 배열을 `ExcelTables`에 복사합니다. Foreach from Variable 열거자를 사용하여 배열의 테이블을 반복할 수 있습니다.  
  
> [!NOTE]  
>  Excel 통합 문서의 테이블 목록에는 워크시트($ 접미사를 가짐)와 명명된 범위가 모두 포함됩니다. 워크시트만 포함하거나 명명된 범위 목록만 포함하도록 목록을 필터링해야 하는 경우에는 이를 위한 다른 코드를 추가해야 합니다.  
  
### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가하고 해당 이름을 **GetExcelTables**로 바꿉니다.  
  
2.  **스크립트 태스크 편집기**를 열고 **스크립트** 탭에서 **ReadOnlyVariables**를 클릭한 후 다음 방법 중 하나를 사용하여 속성 값을 입력합니다.  
  
    -   **ExcelFile**을 입력합니다.  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 ExcelFile 변수를 선택합니다.  
  
3.  **ReadWriteVariables**를 클릭하고 다음 방법 중 하나를 사용하여 속성 값을 입력합니다.  
  
    -   **ExcelTables**를 입력합니다.  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 ExcelTablesvariable 변수를 선택합니다.  
  
4.  **스크립트 편집**을 클릭하여 스크립트 편집기를 엽니다.  
  
5.  스크립트 프로젝트에 **System.Xml** 네임스페이스에 대한 참조를 추가합니다.  
  
6.  **System.Data.OleDb** 네임스페이스에 대한 **Imports** 문을 스크립트 파일의 맨 위에 추가합니다.  
  
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
    connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" & _  
        "Data Source=" & excelFile & _  
        ";Extended Properties=Excel 12.0"  
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
            connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" +  
                "Data Source=" + excelFile + ";Extended Properties=Excel 12.0";  
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
 스크립트 태스크를 사용하여 Excel 테이블의 목록을 배열로 수집하는 대신 ForEach ADO.NET 스키마 행 집합 열거자를 사용하여 Excel 통합 문서 파일의 모든 테이블, 즉 워크시트와 명명된 범위를 반복할 수도 있습니다. 자세한 내용은 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)을 참조하세요.  
  
##  <a name="testing"></a> 예제 결과 표시  
 이 항목의 각 예를 동일한 패키지에서 구성한 경우 모든 스크립트 태스크를 모든 예의 출력을 표시하는 추가 스크립트 태스크에 연결할 수 있습니다.  
  
### <a name="to-configure-a-script-task-to-display-the-output-of-the-examples-in-this-topic"></a>이 항목의 예 출력을 표시하도록 스크립트 태스크를 구성하려면  
  
1.  패키지에 새 스크립트 태스크를 추가하고 해당 이름을 **DisplayResults**로 바꿉니다.  
  
2.  각 태스크가 이전 태스크가 성공적으로 완료된 후 실행되도록 네 개의 예 스크립트 태스크를 서로 연결하고, 네 번째 예 태스크를 **DisplayResults** 태스크에 연결합니다.  
  
3.  **스크립트 태스크 편집기**에서 **DisplayResults** 태스크를 엽니다.  
  
4.  **스크립트** 탭에서 **ReadOnlyVariables**를 클릭하고 다음 방법 중 하나를 사용하여 [예제를 테스트하기 위한 패키지 구성](#configuring)에 나열된 7개의 변수를 모두 추가합니다.  
  
    -   각 변수의 이름을 쉼표로 구분하여 입력합니다.  
  
         -또는-  
  
    -   속성 필드 옆의 줄임표(**…**) 단추를 클릭하고 **변수 선택** 대화 상자에서 해당 변수를 선택합니다.  
  
5.  **스크립트 편집**을 클릭하여 스크립트 편집기를 엽니다.  
  
6.  **Microsoft.VisualBasic** 및 **System.Windows.Forms** 네임스페이스에 대한 **Imports** 문을 스크립트 파일 맨 위에 추가합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](../load-data-to-from-excel-with-ssis.md)  
 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
