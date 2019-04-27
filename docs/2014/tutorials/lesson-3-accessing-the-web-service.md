---
title: '3단원: 웹 서비스에 액세스 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c3e4c198-ab35-4548-9471-1b4e6b6e5dfd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 09671f8880f9f7745359961d9c6c126a893d26a7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653786"
---
# <a name="lesson-3-accessing-the-web-service"></a>3단원: 웹 서비스 액세스
  보고서 서버 웹 서비스에 대한 참조를 프로젝트에 추가한 후에는 웹 서비스의 프록시 클래스 인스턴스를 만듭니다. 그런 다음 프록시 클래스에서 메서드를 호출하여 웹 서비스의 메서드에 액세스할 수 있습니다. 애플리케이션에서 이러한 메서드를 호출하면 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 에 의해 생성된 프록시 클래스 코드가 사용자 애플리케이션과 웹 서비스간의 통신을 처리합니다.  
  
 먼저 웹 서비스의 프록시 클래스 인스턴스인 <xref:ReportService2010.ReportingService2010>를 만듭니다. 그런 다음 프록시 클래스를 사용하여 웹 서비스의 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 메서드를 호출합니다. 이 호출로 예제 보고서인 Company Sales에 대한 이름 및 설명을 검색할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services에서 실행되고 있는 웹 서비스에 액세스할 경우 "ReportServer" 경로에 "$SQLExpress"를 추가해야 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
>   
>  `http://<Server Name>/reportserver$sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-access-the-web-service"></a>웹 서비스에 액세스하려면  
  
1.  먼저 코드 파일에 `using`([!INCLUDE[vbprvb](../includes/vbprvb-md.md)]의 경우 `Imports`) 지시문을 추가하여 Program.cs 파일([!INCLUDE[vbprvb](../includes/vbprvb-md.md)]의 경우 Module1.vb)에 네임스페이스를 추가해야 합니다. 이 지시문을 사용할 경우에는 네임스페이스에서 형식을 정규화하지 않아도 됩니다.  
  
2.  이를 위해 코드 파일 시작 위치에 다음 코드를 추가합니다.  
  
    ```vb  
    Imports System  
    Imports GetPropertiesSample.ReportService2010  
    ```  
  
    ```csharp  
    using System;  
    using GetPropertiesSample.ReportService2010;  
    ```  
  
3.  코드 파일에 네임스페이스 지시문을 입력한 다음에는 콘솔 애플리케이션의 Main 메서드에 다음 코드를 입력합니다. 웹 서비스 인스턴스의 **Url** 속성을 설정할 때 반드시 서버 이름을 변경합니다.  
  
    ```vb  
    Sub Main()  
       Dim rs As New ReportingService2010  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx"  
  
       Dim name As New [Property]  
       name.Name = "Name"  
  
       Dim description As New [Property]  
       description.Name = "Description"  
  
       Dim properties(1) As [Property]  
       properties(0) = name  
       properties(1) = description  
  
       Try  
          Dim returnProperties As [Property]() = rs.GetProperties( _  
             "/AdventureWorks 2012 Sample Reports/Company Sales 2012", properties)  
  
          Dim p As [Property]  
          For Each p In returnProperties  
              Console.WriteLine((p.Name + ": " + p.Value))  
          Next p  
  
       Catch e As Exception  
          Console.WriteLine(e.Message)  
       End Try  
    End Sub  
    ```  
  
    ```csharp  
    static void Main(string[] args)  
    {  
       ReportingService2010 rs = new ReportingService2010();  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx";  
  
       Property name = new Property();  
       name.Name = "Name";  
  
       Property description = new Property();  
       description.Name = "Description";  
  
       Property[] properties = new Property[2];  
       properties[0] = name;  
       properties[1] = description;  
  
       try  
       {  
          Property[] returnProperties = rs.GetProperties(  
          "/AdventureWorks 2012 Sample Reports/Company Sales 2012",properties);  
  
          foreach (Property p in returnProperties)  
          {  
             Console.WriteLine(p.Name + ": " + p.Value);  
          }  
       }  
  
       catch (Exception e)  
       {  
          Console.WriteLine(e.Message);  
       }  
    }  
    ```  
  
4.  솔루션을 저장합니다.  
  
 연습 예제 코드에서는 웹 서비스의 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 메서드를 사용하여 예제 보고서 Company Sales 2012의 속성을 검색합니다. 합니다 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 메서드는 두 개의 인수: 배열 및 속성 정보를 검색 하려는 보고서의 이름을 **Property** 검색 하려는 값의 속성 이름을 포함 하는 개체입니다. 이 메서드는 또한 속성 인수에 지정된 속성의 이름과 값이 들어 있는 **Property[]** 개체의 배열을 반환합니다.  
  
> [!NOTE]  
>  속성 인수에 빈 **Property[]** 배열을 지정하면 사용 가능한 모든 속성이 반환됩니다.  
  
 이전 예제 코드에서는 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 메서드를 사용하여 예제 보고서 Company Sales 2012의 이름과 설명을 반환합니다. 그런 다음 `foreach` 루프를 사용하여 속성과 값을 콘솔에 기록합니다.  
  
 보고서 서버 웹 서비스용 프록시 클래스를 만들고 사용하는 방법은 [Creating the Web Service Proxy](../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [4단원: 응용 프로그램을 실행 &#40;VB VC&#35;&#41;](../../2014/tutorials/lesson-4-running-the-application-vb-vcsharp.md)   
 [Visual Basic 또는 Visual C를 사용 하 여 보고서 서버 웹 서비스에 액세스&#35; &#40;SSRS 자습서&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
