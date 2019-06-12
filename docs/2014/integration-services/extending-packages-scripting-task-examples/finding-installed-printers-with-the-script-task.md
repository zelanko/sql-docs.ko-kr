---
title: 스크립트 태스크를 사용하여 설치된 프린터 찾기 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- System.Drawing.Printing namespace
- printers [Integration Services]
- SSIS Script task, printers
- locating printers
- Printing namespace
- Script task [Integration Services], examples
- finding printers [SQL Server]
- Script task [Integration Services], printers
ms.assetid: 50a55014-e2c3-4ecd-84e1-3e877c55a260
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: abc0228063e62447c34b0236009977a33bddb176
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768499"
---
# <a name="finding-installed-printers-with-the-script-task"></a>스크립트 태스크를 사용하여 설치된 프린터 찾기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 변환된 데이터의 최종 대상은 인쇄된 보고서인 경우가 종종 있습니다. 합니다 `System.Drawing.Printing` 네임 스페이스에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 프린터 작업을 위한 클래스를 제공 합니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="description"></a>Description  
 다음 예에서는 서버에 설치된 프린터 중 미국에서 사용하는 Legal 크기 용지를 지원하는 프린터를 찾습니다. 지원되는 용지 크기를 확인하는 코드는 프라이빗 함수에 캡슐화되어 있습니다. 각 프린터에 대한 설정을 확인할 때 스크립트의 진행률을 추적할 수 있도록 스크립트에서는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 메서드를 사용하여 Legal 크기 용지를 사용하는 프린터에 대한 정보 메시지를 발생시키거나 Legal 크기 용지를 사용하지 않는 프린터에 대해 경고를 발생시킵니다. 이러한 메시지는 디자이너에서 패키지를 실행할 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA(Tools for Applications) IDE의 **출력** 창에 나타납니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  `Object` 유형의 `PrinterList`라는 변수를 만듭니다.  
  
2.  **스크립트 태스크 편집기**의 **스크립트** 페이지에서 ReadWriteVariables 속성에 이 변수를 추가합니다.  
  
3.  스크립트 프로젝트에서 **System.Drawing** 네임스페이스에 대한 참조를 추가합니다.  
  
4.  코드에서 사용 하 여 `Imports` 문을 합니다 **System.Collections** 고 `System.Drawing.Printing` 네임 스페이스입니다.  
  
### <a name="code"></a>코드  
  
```vb  
Public Sub Main()  
  
    Dim printerName As String  
    Dim currentPrinter As New PrinterSettings  
    Dim size As PaperSize  
  
    Dim printerList As New ArrayList  
    For Each printerName In PrinterSettings.InstalledPrinters  
        currentPrinter.PrinterName = printerName  
        If PrinterHasLegalPaper(currentPrinter) Then  
            printerList.Add(printerName)  
            Dts.Events.FireInformation(0, "Example", _  
                "Printer " & printerName & " has legal paper.", _  
                String.Empty, 0, False)  
        Else  
            Dts.Events.FireWarning(0, "Example", _  
                "Printer " & printerName & " DOES NOT have legal paper.", _  
                String.Empty, 0)  
        End If  
    Next  
  
    Dts.Variables("PrinterList").Value = printerList  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Function PrinterHasLegalPaper( _  
    ByVal thisPrinter As PrinterSettings) As Boolean  
  
    Dim size As PaperSize  
    Dim hasLegal As Boolean = False  
  
    For Each size In thisPrinter.PaperSizes  
        If size.Kind = PaperKind.Legal Then  
            hasLegal = True  
        End If  
    Next  
  
    Return hasLegal  
  
End Function  
```  
  
```csharp  
public void Main()  
        {  
  
            PrinterSettings currentPrinter = new PrinterSettings();  
            PaperSize size;  
            Boolean Flag = false;  
  
            ArrayList printerList = new ArrayList();  
            foreach (string printerName in PrinterSettings.InstalledPrinters)  
            {  
                currentPrinter.PrinterName = printerName;  
                if (PrinterHasLegalPaper(currentPrinter))  
                {  
                    printerList.Add(printerName);  
                    Dts.Events.FireInformation(0, "Example", "Printer " + printerName + " has legal paper.", String.Empty, 0, ref Flag);  
                }  
                else  
                {  
                    Dts.Events.FireWarning(0, "Example", "Printer " + printerName + " DOES NOT have legal paper.", String.Empty, 0);  
                }  
            }  
  
            Dts.Variables["PrinterList"].Value = printerList;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private bool PrinterHasLegalPaper(PrinterSettings thisPrinter)  
        {  
  
            bool hasLegal = false;  
  
            foreach (PaperSize size in thisPrinter.PaperSizes)  
            {  
                if (size.Kind == PaperKind.Legal)  
                {  
                    hasLegal = true;  
                }  
            }  
  
            return hasLegal;  
  
        }  
```  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [스크립트 태스크 예제](../extending-packages-scripting-task-examples/script-task-examples.md)  
  
  
