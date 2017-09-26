---
title: "스크립트 태스크를 사용 하 여 ForEach 루프에 대 한 목록을 수집 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], Foreach loops
- Script task [Integration Services], examples
- SSIS Script task, Foreach loops
ms.assetid: 694f0462-d0c5-4191-b64e-821b1bdef055
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1bd133c2fdc8c500db9c07df9c54e954db327bf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="gathering-a-list-for-the-foreach-loop-with-the-script-task"></a>스크립트 태스크를 사용하여 ForEach 루프에 사용할 목록 수집
  Foreach from Variable 열거자는 변수에서 해당 열거자에 전달된 목록의 항목을 열거하고 각 항목에 대해 동일한 태스크를 수행합니다. 스크립트 태스크에서 사용자 지정 코드를 사용하여 이러한 용도로 사용할 목록을 채울 수 있습니다. 열거자에 대 한 자세한 내용은 참조 [Foreach 루프 컨테이너](../../integration-services/control-flow/foreach-loop-container.md)합니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="description"></a>Description  
 다음 예제에서는 메서드를 사용 하 여는 **System.IO** 인지 관계 없이 최신 변수에서 사용자가 지정한 일 수보다 오래 된 컴퓨터에는 Excel 통합 문서의 목록을 수집 하는 네임 스페이스입니다. 이 예에서는 C 드라이브의 디렉터리에서 확장명이 .xls인 파일을 재귀적으로 검색하고 각 파일을 마지막으로 수정한 날짜를 검사하여 목록에 포함할 파일인지 확인합니다. 조건에 맞는 파일을 추가 **ArrayList** 저장는 **ArrayList** Foreach 루프 컨테이너에서 나중에 사용할 변수를 합니다. Foreach 루프 컨테이너는 Foreach from Variable 열거자를 사용하도록 구성됩니다.  
  
> [!NOTE]  
>  Foreach from Variable 열거자와 함께 사용 하는 변수 형식 이어야 합니다 **개체**합니다. 변수에 추가 하는 개체는 다음 인터페이스 중 하나를 구현 해야: **System.Collections.IEnumerable**, **System.Runtime.InteropServices.ComTypes.IEnumVARIANT**, **System.ComponentModel IListSource**, 또는 **Microsoft.SqlServer.Dts.Runtime.Wrapper.ForEachEnumeratorHost**합니다. **배열** 또는 **ArrayList** 는 일반적으로 사용 합니다. **ArrayList** 대 한 참조가 및 **Imports** 문을 **System.Collections** 네임 스페이스입니다.  
  
 `FileAge` 패키지 변수에 각기 다른 양수 및 음수 값을 사용하여 이 태스크를 시험해 볼 수 있습니다. 예를 들어 만든 지 5일이 지나지 않은 파일을 검색하려면 5를 입력하고, 만든 지 3일이 지난 파일을 검색하려면 -3을 입력합니다. 드라이브에 검색할 폴더가 많은 경우 이 태스크를 수행하는 데 1~2분 정도 소요될 수 있습니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  `FileAge`라는 정수 형식의 패키지 변수를 만들고 양의 정수나 음의 정수 값을 입력합니다. 값이 양수이면 코드는 만든 날짜 또는 수정한 날짜가 지정된 일 수를 경과하지 않은 파일을 검색하고, 값이 음수이면 지정된 일 수를 경과한 파일을 검색합니다.  
  
2.  패키지 변수를 만들고 `FileList` 형식의 **개체** from Variable 열거자에서 Foreach 나중에 사용할 스크립트 태스크에 의해 수집 된 파일 목록을 받을 수 있습니다.  
  
3.  추가 `FileAge` 스크립트 태스크의 변수 **ReadOnlyVariables** 속성을 추가 하 고는 `FileList` 변수를 **ReadWriteVariables** 속성입니다.  
  
4.  코드를 가져옵니다는 **System.Collections** 및 **System.IO** 네임 스페이스입니다.  
  
### <a name="code"></a>코드  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Collections  
Imports System.IO  
  
Public Class ScriptMain  
  
  Private Const FILE_AGE As Integer = -50  
  
  Private Const FILE_ROOT As String = "C:\"  
  Private Const FILE_FILTER As String = "*.xls"  
  
  Private isCheckForNewer As Boolean = True  
  Dim fileAgeLimit As Integer  
  Private listForEnumerator As ArrayList  
  
  Public Sub Main()  
  
    fileAgeLimit = DirectCast(Dts.Variables("FileAge").Value, Integer)  
  
    ' If value provided is positive, we want files NEWER THAN n days.  
    '  If negative, we want files OLDER THAN n days.  
    If fileAgeLimit < 0 Then  
      isCheckForNewer = False  
    End If  
    ' Extract number of days as positive integer.  
    fileAgeLimit = Math.Abs(fileAgeLimit)  
  
    listForEnumerator = New ArrayList  
  
    GetFilesInFolder(FILE_ROOT)  
  
    ' Return the list of files to the variable  
    '  for later use by the Foreach from Variable enumerator.  
    System.Windows.Forms.MessageBox.Show("Matching files: " & listForEnumerator.Count.ToString, "Results", Windows.Forms.MessageBoxButtons.OK, Windows.Forms.MessageBoxIcon.Information)  
    Dts.Variables("FileList").Value = listForEnumerator  
  
    Dts.TaskResult = ScriptResults.Success  
  
  End Sub  
  
  Private Sub GetFilesInFolder(ByVal folderPath As String)  
  
    Dim localFiles() As String  
    Dim localFile As String  
    Dim fileChangeDate As Date  
    Dim fileAge As TimeSpan  
    Dim fileAgeInDays As Integer  
    Dim childFolder As String  
  
    Try  
      localFiles = Directory.GetFiles(folderPath, FILE_FILTER)  
      For Each localFile In localFiles  
        fileChangeDate = File.GetLastWriteTime(localFile)  
        fileAge = DateTime.Now.Subtract(fileChangeDate)  
        fileAgeInDays = fileAge.Days  
        CheckAgeOfFile(localFile, fileAgeInDays)  
      Next  
  
      If Directory.GetDirectories(folderPath).Length > 0 Then  
        For Each childFolder In Directory.GetDirectories(folderPath)  
          GetFilesInFolder(childFolder)  
        Next  
      End If  
  
    Catch  
      ' Ignore exceptions on special folders such as System Volume Information.  
    End Try  
  
  End Sub  
  
  Private Sub CheckAgeOfFile(ByVal localFile As String, ByVal fileAgeInDays As Integer)  
  
    If isCheckForNewer Then  
      If fileAgeInDays <= fileAgeLimit Then  
        listForEnumerator.Add(localFile)  
      End If  
    Else  
      If fileAgeInDays > fileAgeLimit Then  
        listForEnumerator.Add(localFile)  
      End If  
    End If  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Math;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Collections;  
using System.IO;  
  
public partial class ScriptMain : Microsoft.SqlServer.Dts.Tasks.ScriptTask.VSTARTScriptObjectModelBase  
    {  
  
        private const int FILE_AGE = -50;  
  
        private const string FILE_ROOT = "C:\\";  
        private const string FILE_FILTER = "*.xls";  
  
        private bool isCheckForNewer = true;  
        int fileAgeLimit;  
        private ArrayList listForEnumerator;  
  
        public void Main()  
  {  
  
    fileAgeLimit = (int)(Dts.Variables["FileAge"].Value);  
  
    // If value provided is positive, we want files NEWER THAN n days.  
    // If negative, we want files OLDER THAN n days.  
    if (fileAgeLimit<0)  
    {  
      isCheckForNewer = false;  
    }  
    // Extract number of days as positive integer.  
    fileAgeLimit = Math.Abs(fileAgeLimit);  
  
    ArrayList listForEnumerator = new ArrayList();  
  
    GetFilesInFolder(FILE_ROOT);  
  
    // Return the list of files to the variable  
    // for later use by the Foreach from Variable enumerator.  
    System.Windows.Forms.MessageBox.Show("Matching files: "+ listForEnumerator.Count, "Results",   
MessageBoxButtons.OK, MessageBoxIcon.Information);  
    Dts.Variables["FileList"].Value = listForEnumerator;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  
  }  
  
        private void GetFilesInFolder(string folderPath)  
        {  
  
            string[] localFiles;  
            DateTime fileChangeDate;  
            TimeSpan fileAge;  
            int fileAgeInDays;  
  
            try  
            {  
                localFiles = Directory.GetFiles(folderPath, FILE_FILTER);  
                foreach (string localFile in localFiles)  
                {  
                    fileChangeDate = File.GetLastWriteTime(localFile);  
                    fileAge = DateTime.Now.Subtract(fileChangeDate);  
                    fileAgeInDays = fileAge.Days;  
                    CheckAgeOfFile(localFile, fileAgeInDays);  
                }  
  
                if (Directory.GetDirectories(folderPath).Length > 0)  
                {  
                    foreach (string childFolder in Directory.GetDirectories(folderPath))  
                    {  
                        GetFilesInFolder(childFolder);  
                    }  
                }  
  
            }  
            catch  
            {  
                // Ignore exceptions on special folders, such as System Volume Information.  
            }  
  
        }  
  
        private void CheckAgeOfFile(string localFile, int fileAgeInDays)  
        {  
  
            if (isCheckForNewer)  
            {  
                if (fileAgeInDays <= fileAgeLimit)  
                {  
                    listForEnumerator.Add(localFile);  
                }  
            }  
            else  
            {  
                if (fileAgeInDays > fileAgeLimit)  
                {  
                    listForEnumerator.Add(localFile);  
                }  
            }  
  
        }  
  
    }  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Foreach 루프 컨테이너](../../integration-services/control-flow/foreach-loop-container.md)   
 [Foreach 루프 컨테이너 구성](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
  
  
