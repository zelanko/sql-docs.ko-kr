---
title: '2 단원: xsd 도구를 사용 하 여 RDL 스키마에서 클래스 생성 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a81c87f1-7977-4b30-b6ac-b38b3e2b6398
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f5f74c6621d329885e9149fce9a37c7418d9c37b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62653758"
---
# <a name="lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool"></a>2단원: xsd 도구를 사용하여 RDL 스키마에서 클래스 생성
  
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 프로젝트를 만든 후 다음 단계는 보고서 정의 스키마의 로컬 복사본을 검색하고 XML 스키마 정의 도구(Xsd.exe)를 실행하는 것입니다.  
  
### <a name="to-generate-the-rdl-classes"></a>RDL 클래스를 생성하려면  
  
1.  
  [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 또는 이에 상당하는 웹 브라우저 인스턴스를 열고 다음 URL로 이동합니다.  
  
    ```  
    https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition/ReportDefinition.xsd  
    ```  
  
2.  RDL 스키마가 브라우저에서 열렸으면 **파일** 메뉴에서 **다른 이름으로 저장**을 선택합니다.  
  
3.  
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 프로젝트를 만든 위치를 찾아 스키마를 ReportDefinition.xsd라는 이름으로 저장합니다.  
  
4.  파일이 저장되었으면 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 명령 프롬프트의 인스턴스를 엽니다. 명령 프롬프트의 인스턴스를 열려면 시작 메뉴를 클릭하고 **모든 프로그램**, **Microsoft Visual Studio 2010**, **Visual Studio Tools** 를 차례로 가리킨 다음 **Visual Studio 명령 프롬프트(2010)** 를 클릭합니다.  
  
5.  현재 경로를 ReportDefinition.xsd 파일을 저장한 위치로 변경합니다.  
  
     `CD\<ReportDefinition.xsd Path>`  
  
6.  다음 명령을 사용하여 RDL 스키마에 대한 클래스가 있는 ReportDefinition.cs 파일을 생성합니다.  
  
     `xsd /c /n:SampleRDLSchema ReportDefinition.xsd`  
  
     ReportDefinition.vb 파일을 생성하려면 다음 명령을 사용합니다.  
  
     `xsd /c /l:VB /n:SampleRDLSchema ReportDefinition.xsd`  
  
7.  프로젝트에 ReportDefinition.xsd를 추가합니다. 
  **프로젝트** 메뉴에서 **기존 항목 추가**를 클릭합니다. ReportDefinition.xsd 파일의 위치로 이동하여 ReportDefinition.xsd를 선택한 다음 **추가**를 클릭합니다.  
  
    > [!NOTE]  
    >  프로젝트에 ReportDefinition.xsd 파일을 추가한 후에도 **솔루션 탐색기** 에 ReportDefinition.cs(.vb) 파일이 표시되지 않습니다. 파일을 표시하려면 ReportDefinition.xsd 파일 옆에 있는 확장/축소 단추를 클릭합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 다음 단원에서는 RDL 스키마에서 생성한 클래스를 사용하여 보고서 서버에서 보고서 정의를 로드하는 코드를 작성합니다. 
  [Lesson 3: Load a Report Definition from the Report Server](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [RDL 스키마 &#40;생성 된 클래스를 사용 하 여 보고서 업데이트 (SSRS 자습서&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [SSRS&#41;&#40;보고서 정의 언어](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
