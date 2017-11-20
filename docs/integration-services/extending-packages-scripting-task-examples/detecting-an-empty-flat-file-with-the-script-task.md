---
title: "스크립트 태스크와 빈 플랫 파일 검색 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-task-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 40deae6a08a597114fbc721271a789895e1d8fa2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>스크립트 태스크를 사용하여 빈 플랫 파일 검색
  플랫 파일 원본에서는 플랫 파일의 처리를 시도하기 전에 플랫 파일에 데이터 행이 들어 있는지 여부를 확인하지 않습니다. 그러나 데이터 행이 들어 있지 않은 파일을 건너뛰면 특히 수많은 플랫 파일을 반복하는 패키지 등에서 패키지 효율성을 높일 수 있습니다. 스크립트 태스크는 패키지에서 데이터 흐름의 처리를 시작하기 전에 빈 플랫 파일을 찾을 수 있습니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="description"></a>Description  
 다음 예제에서는 메서드를 사용 하 여는 **System.IO** 파일이 비어 있거나 필요 합니다. 열과 같은 비 데이터 행만 들어 있는지 여부를 결정 하는 플랫 파일 연결 관리자에 지정 된 플랫 파일을 테스트 하려면 네임 스페이스 머리글이 나 빈 줄. 이 스크립트에서는 먼저 파일 크기를 확인합니다. 크기가 0바이트이면 해당 파일은 비어 있는 것입니다. 파일 크기가 0보다 크면 스크립트에서는 줄이 더 이상 없거나 줄 수가 비데이터 행의 예상 개수를 초과할 때까지 파일의 줄을 읽습니다. 파일의 줄 수가 비데이터 행의 예상 개수보다 작거나 같으면 해당 파일은 비어 있는 것으로 간주됩니다. 결과는 패키지의 제어 흐름에서 분기하는 데 사용할 수 있는 값을 갖는 사용자 변수에 부울 값으로 반환됩니다. **FireInformation** 메서드에 결과 표시 합니다는 **출력** 의 창 고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA Tools for Applications ().  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  만들기 및 구성 이라는 플랫 파일 연결 관리자 **EmptyFlatFileTest**합니다.  
  
2.  `FFNonDataRows`라는 정수 변수를 만들고 해당 값을 플랫 파일에 필요한 비데이터 행의 개수로 설정합니다.  
  
3.  `FFIsEmpty`라는 부울 변수를 만듭니다.  
  
4.  추가 `FFNonDataRows` 스크립트 태스크의 변수 **ReadOnlyVariables** 속성입니다.  
  
5.  추가 `FFIsEmpty` 스크립트 태스크의 변수 **ReadWriteVariables** 속성입니다.  
  
6.  코드를 가져옵니다는 **System.IO** 네임 스페이스입니다.  
  
 단일 플랫 파일 연결 관리자를 사용하는 대신 Foreach File 열거자를 사용하여 파일을 반복하는 경우에는 아래의 예제 코드를 수정하여 연결 관리자 대신 열거된 값이 저장된 변수에서 파일 이름과 경로를 가져와야 합니다.  
  
### <a name="code"></a>코드  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
## <a name="see-also"></a>관련 항목:  
 [스크립트 태스크 예제](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
  
  

