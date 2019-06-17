---
title: '3단원: 보고서 서버에서 보고서 정의 로드 합니다. | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ad8b31c-43b0-4481-a31b-090cbed4a438
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d4c51002c8c829417c63a0dd6c59a3538604fd81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042519"
---
# <a name="lesson-3-load-a-report-definition-from-the-report-server"></a>3단원: 보고서 서버에서 보고서 정의 로드
  프로젝트를 만들고 RDL 스키마에서 클래스를 생성하면 보고서 서버에서 보고서 정의를 로드할 준비가 됩니다.  
  
### <a name="to-load-a-report-definition"></a>보고서 정의를 로드하려면  
  
1.  맨 위에 있는 private 필드를 추가 합니다 `ReportUpdater` 클래스 (사용 하는 경우 모듈 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)])에 대 한는 `Report` 클래스입니다. 이 필드는 응용 프로그램의 수명이 지속되는 동안 보고서 서버에서 로드된 보고서에 대한 참조를 유지 관리하는 데 사용됩니다.  
  
    ```csharp  
    private Report _report;  
    ```  
  
    ```vb  
    Private m_report As Report  
    ```  
  
2.  Program.cs 파일([!INCLUDE[vbprvb](../includes/vbprvb-md.md)]의 경우 Module1.vb)에서 `LoadReportDefinition()` 메서드의 코드를 다음 코드로 바꿉니다.  
  
    ```csharp  
    private void LoadReportDefinition()  
    {  
        System.Console.WriteLine("Loading Report Definition");  
  
        string reportPath =   
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012";  
  
        // Retrieve the report definition   
        // from the report server  
        byte[] bytes =   
            _reportService.GetItemDefinition(reportPath);  
  
        if (bytes != null)  
        {  
            XmlSerializer serializer =   
                new XmlSerializer(typeof(Report));  
  
            // Load the report bytes into a memory stream  
            using (MemoryStream stream = new MemoryStream(bytes))  
            {  
                // Deserialize the report stream to an   
                // instance of the Report class  
                _report = (Report)serializer.Deserialize(stream);  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub LoadReportDefinition()  
  
        System.Console.WriteLine("Loading Report Definition")  
  
        Dim reportPath As String = _  
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012"  
  
        'Retrieve the report definition   
        'from the report server  
        Dim bytes As Byte() = _  
            m_reportService.GetItemDefinition(reportPath)  
  
        If Not (bytes Is Nothing) Then  
  
            Dim serializer As XmlSerializer = _  
                New XmlSerializer(GetType(Report))  
  
            'Load the report bytes into a memory stream  
            Using stream As MemoryStream = New MemoryStream(bytes)  
  
                'Deserialize the report stream to an   
                'instance of the Report class  
                m_report = CType(serializer.Deserialize(stream), _  
                                 Report)  
  
            End Using  
  
        End If  
  
    End Sub  
    ```  
  
## <a name="next-lesson"></a>다음 단원  
 다음 단원에서는 코드를 작성하여 보고서 서버에서 로드된 보고서 정의를 업데이트합니다. [4단원: 보고서 정의 프로그래밍 방식으로 업데이트할](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDL 스키마에서 생성 된 클래스를 사용 하 여 보고서를 업데이트 하는 중 &#40;SSRS 자습서&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [RDL(Report Definition Language)&#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
