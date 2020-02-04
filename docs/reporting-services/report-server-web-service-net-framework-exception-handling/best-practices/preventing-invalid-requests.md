---
title: 잘못된 요청 방지 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 219fc1883f395e56f1fd73af32e95ea066df28b7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62992214"
---
# <a name="preventing-invalid-requests"></a>잘못된 요청 방지
  애플리케이션 흐름을 분석하고 보고서 서버로 전송되는 요청이 유효한지 확인하여 일부 유형의 예외가 throw되지 않도록 할 수 있습니다. 예를 들어 사용자가 보고서의 이름, 데이터 원본 또는 기타 보고서 서버 항목을 추가하거나 갱신할 수 있는 애플리케이션의 경우 사용자가 입력하는 텍스트의 유효성을 검사해야 합니다. 또한 요청을 보고서 서버로 보내기 전에 항상 예약 문자를 확인해야 합니다. 코드에서 **if**문 또는 기타 논리 구문을 사용하여 보고서 서버에 요청을 보내는 데 필요한 조건이 충족되지 않았음을 사용자에게 알립니다.  
  
 다음의 간단한 C# 예에서는 사용자가 이름에 슬래시(/) 문자가 포함된 보고서를 만들려고 시도할 때 오류 메시지를 표시합니다.  
  
```  
// C#  
private void PublishReport()  
{  
   int index;  
   string reservedChar;  
   string message;  
  
   // Check the text value of the name text box for "/",  
   // a reserved character  
   index = nameTextBox.Text.IndexOf(@"/");  
  
   if ( index != -1) // The text contains the character  
   {  
      reservedChar = nameTextBox.Text.Substring(index, 1);  
      // Build a user-friendly error message  
      message = "The name of the report cannot contain the reserved character " +  
         "\"" + reservedChar + "\". " +  
         "Please enter a valid name for the report. " +  
         "For more information about reserved characters, " +  
         "see the help documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      FileStream stream = File.OpenRead("MyReport.rdl");  
      definition = new Byte[stream.Length];  
      stream.Read(definition, 0, (int) stream.Length);  
      stream.Close();  
      // Create report with user-defined name  
      rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
      MessageBox.Show("Report: {0} created successfully", name);  
   }  
}  
```  
  
 요청이 보고서 서버로 전송되기 전에 방지할 수 있는 오류 유형에 대한 자세한 내용은 [SoapException 오류 테이블](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)을 참조하세요. try/catch 블록을 사용하여 위의 예를 개선하는 방법은 [Try 및 Catch 블록 사용](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
