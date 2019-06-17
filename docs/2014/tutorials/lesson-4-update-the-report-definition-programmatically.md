---
title: '4단원: 보고서 정의 프로그래밍 방식으로 업데이트할 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1f0a1d46-6d6d-4f67-b51e-06dbbbffacf9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 703643f2c51ec86090cb03ba7089080dfe416620
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63137461"
---
# <a name="lesson-4-update-the-report-definition-programmatically"></a>4단원: 프로그래밍 방식으로 보고서 정의 업데이트
  이제 보고서 서버에서 보고서 정의가 로드되었고 보고서 필드를 사용하여 해당 정의를 참조했으므로 보고서 정의를 업데이트해야 합니다. 이 예에서는 보고서의 `Description` 속성을 업데이트합니다.  
  
### <a name="to-update-the-report-definition"></a>보고서 정의를 업데이트하려면  
  
1.  Program.cs 파일에서 UpdateReportDefinition() 메서드의 코드를 바꿉니다 (의 경우 module1.vb) 라는 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 다음 코드를 사용 하 여:  
  
    ```csharp  
    private void UpdateReportDefinition()  
    {  
        System.Console.WriteLine("Updating Report Definition");  
  
        // Create a list of the Items Choices for the Report. The   
        // ItemsChoiceType118 enum represents all the properties  
        // available in the report and the ItemsElementName   
        // represents the properties that exist in the current   
        // instance of the report.  
        List<ItemsChoiceType118> _reportItems =   
            new List<ItemsChoiceType118>(_report.ItemsElementName);  
  
        // Locate the index for the Description property  
        int index = _reportItems.IndexOf(  
            ItemsChoiceType118.Description);  
  
        // The Description item is of type StringLocIDType, so   
        // cast the item type first and then assign new value.  
        System.Console.WriteLine("- Old Description: " +   
            ((StringLocIDType)_report.Items[index]).Value );  
  
        // Update the Description for the Report  
        ((StringLocIDType)_report.Items[index]).Value =   
            "New Report Description";  
  
        System.Console.WriteLine("- New Description: " +   
            ((StringLocIDType)_report.Items[index]).Value );  
    }  
    ```  
  
    ```vb  
    Private Sub UpdateReportDefinition()  
  
        System.Console.WriteLine("Updating Report Definition")  
  
        'Create a list of the Items Choices for the Report. The   
        'ItemsChoiceType118 enum represents all the properties  
        'available in the report and the ItemsElementName   
        'represents the properties that exist in the current   
        'instance of the report.  
        Dim reportItems As List(Of ItemsChoiceType118) = _  
            New List(Of ItemsChoiceType118)(m_report.ItemsElementName)  
  
        'Locate the index for the Description property  
        Dim index As Integer = _  
            reportItems.IndexOf(ItemsChoiceType118.Description)  
  
        'The Description item is of type StringLocIDType, so   
        'cast the item type first and then assign new value.  
        System.Console.WriteLine("- Old Description: " & _  
            DirectCast(m_report.Items(index), StringLocIDType).Value)  
  
        'Update the Description for the Report  
        DirectCast(m_report.Items(index), StringLocIDType).Value = _  
            "New Report Description"  
  
        System.Console.WriteLine("- New Description: " & _  
            DirectCast(m_report.Items(index), StringLocIDType).Value)  
  
    End Sub  
    ```  
  
## <a name="next-lesson"></a>다음 단원  
 다음 단원에서는 업데이트된 보고서 정의를 다시 보고서 서버에 저장합니다. [5단원: 보고서 서버에 보고서 정의 게시](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDL 스키마에서 생성 된 클래스를 사용 하 여 보고서를 업데이트 하는 중 &#40;SSRS 자습서&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)  
  
  
