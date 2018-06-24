---
title: RDL 스키마 (SSRS 자습서)에서 생성 한 클래스를 사용 하 여 보고서 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- RDL [Reporting Services], generating
- RDL [Reporting Services], tutorials
- RDL [Reporting Services], serializing
ms.assetid: 8f81d48f-7ab9-4ef8-bce0-7d16d9a47fbd
caps.latest.revision: 26
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: a13d94965eebf99c401159c86e5fed065f5ec7ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079172"
---
# <a name="updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial"></a>RDL 스키마에서 생성한 클래스를 사용하여 보고서 업데이트(SSRS 자습서)
  이 자습서에서는 XML 스키마 정의 도구 (Xsd.exe) 클래스를 생성 하려면 serialize 하 고 보고서 정의 파일 (.rdl 및.rdlc)을 deserialize 할 수 있도록 사용 방법의 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] <xref:System.Xml.Serialization.XmlSerializer> 클래스입니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서를 통해 다음 작업을 완료합니다.  
  
-   사용 하 여 응용 프로그램 만들기는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 콘솔 응용 프로그램 프로젝트 템플릿을 합니다.  
  
-   **xsd** 도구를 사용하여 RDL(Report Definition Language) 스키마의 클래스를 생성합니다.  
  
-   보고서 서버에 연결하고 보고서 정의를 검색합니다.  
  
-   코드를 작성하여 보고서 정의 파일을 업데이트합니다.  
  
-   업데이트한 보고서 정의를 다시 보고서 서버에 저장합니다.  
  
-   RDL Schema 응용 프로그램을 실행합니다(VB/C#).  
  
> [!NOTE]  
>  이 자습서에 제공되는 코드 예제는 설명이 없는 보고서의 경우 실패할 수 있습니다. 설명이 지정되지 않은 보고서의 경우 설명 속성이 존재하지 않기 때문입니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서를 수행하려면 다음 항목이 필요합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]입니다.  
  
-   보고서 서버가 있는 컴퓨터의 보고서 서버 웹 서비스에 액세스하고 보고서를 게시할 수 있는 권한  
  
-   [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 인스턴스에 설치된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 예제 데이터베이스  
  
-   보고서 서버에 설치된 보고서. 이 자습서에서는 예제 보고서 Company Sales 2012를 사용합니다. 예제 보고서에 대한 자세한 내용은 [SQL Server Reporting Services 제품 예제(SQL Server Reporting Services Product Samples)](http://go.microsoft.com/fwlink/?LinkId=177889)를 참조하십시오.  
  
> [!NOTE]  
>  설치 시 예제가 자동으로 설치되지 않지만 예제는 언제든지 설치할 수 있습니다. 예제에 대한 정보는 [SQL Server 제품 예제](http://go.microsoft.com/fwlink/?LinkId=182887)를 참조하십시오.  
  
 **자습서에 소요되는 예상 시간:** 30분  
  
## <a name="tasks"></a>태스크  
 [1단원: RDL Schema Visual Studio 프로젝트 만들기](../../2014/tutorials/lesson-1-create-the-rdl-schema-visual-studio-project.md)  
  
 [2단원: xsd 도구를 사용하여 RDL 스키마에서 클래스 생성](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)  
  
 [3단원: 보고서 서버에서 보고서 정의 로드](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)  
  
 [4단원: 프로그래밍 방식으로 보고서 정의 업데이트](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)  
  
 [5단원: 보고서 정의를 보고서 서버에 게시](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)  
  
 [6 단원: RDL Schema 응용 프로그램을 실행 &#40;VB C&#35;&#41;](../../2014/tutorials/lesson-6-run-the-rdl-schema-application-vb-csharp.md)  
  
## <a name="see-also"></a>관련 항목  
 [RDL(Report Definition Language)&#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  