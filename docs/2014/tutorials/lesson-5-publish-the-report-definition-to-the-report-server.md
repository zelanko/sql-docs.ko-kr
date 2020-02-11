---
title: '5 단원: 보고서 서버에 보고서 정의 게시 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 57fab70f-4a72-4413-a0ad-d0525caca3f7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c9c561657767c1b1e593fa9dcd9702b72193004d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63272864"
---
# <a name="lesson-5-publish-the-report-definition-to-the-report-server"></a>5단원: 보고서 정의를 보고서 서버에 게시
  보고서 정의를 업데이트하는 마지막 단계는 해당 정의를 다시 보고서 서버에 게시하는 것입니다.  
  
### <a name="to-publish-the-report-to-the-report-catalog"></a>보고서를 보고서 카탈로그에 게시하려면  
  
1.  Program.cs 파일 (의 경우 `PublishReportDefinition()` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]module1.vb)의 메서드에 대 한 코드를 다음 코드로 바꿉니다.  
  
    ```csharp  
    private void PublishReportDefinition()  
    {  
        System.Console.WriteLine("Publishing Report Definition");  
  
        string reportPath =  
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012";  
  
        XmlSerializer serializer =  
            new XmlSerializer(typeof(Report));  
  
        using (MemoryStream stream = new MemoryStream())  
        {  
            // Serialize the report into the MemoryStream  
            serializer.Serialize(stream, _report);  
            stream.Position = 0;  
  
            byte[] bytes = stream.ToArray();  
  
            // Update the report on the report server  
            Warning[] warnings =   
                _reportService.SetItemDefinition(reportPath, bytes, null);  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub PublishReportDefinition()  
  
        System.Console.WriteLine("Publishing Report Definition")  
  
        Dim reportPath As String = _  
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012"  
        Dim serializer As XmlSerializer = _  
            New XmlSerializer(GetType(Report))  
  
        Using stream As MemoryStream = New MemoryStream  
  
            'Serialize the report into the MemoryStream  
            serializer.Serialize(stream, m_report)  
            stream.Position = 0  
  
            'Update the report on the report server  
            Dim bytes As Byte() = stream.ToArray  
            Dim warnings As Warning() = _  
                m_reportService.SetItemDefinition(reportPath, bytes, Nothing)  
  
        End Using  
  
    End Sub  
    ```  
  
## <a name="next-lesson"></a>다음 단원  
 다음 단원에서는 `SampleRDLSchema` 응용 프로그램을 컴파일하고 실행 합니다. [6 단원: RDL 스키마 응용 프로그램 실행 &#40;VB-C&#35;&#41;](../../2014/tutorials/lesson-6-run-the-rdl-schema-application-vb-csharp.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [RDL 스키마 &#40;생성 된 클래스를 사용 하 여 보고서 업데이트 (SSRS 자습서&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [SSRS&#41;&#40;보고서 정의 언어](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
