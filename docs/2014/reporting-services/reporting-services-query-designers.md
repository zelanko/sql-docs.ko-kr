---
title: Reporting Services 쿼리 디자이너 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- query designers [Reporting Services]
ms.assetid: 07efd3f1-804f-45f7-b62a-3e727a3d9835
caps.latest.revision: 16
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ca805856f4cd09d6d1172b5602a7a9e54b4cc16c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080819"
---
# <a name="reporting-services-query-designers"></a>Reporting Services 쿼리 디자이너
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서에서 각 데이터 원본 유형에 대 한 쿼리를 작성할 수 있도록 그래픽 및 텍스트 기반 쿼리 디자이너를 제공 합니다.  
  
 일부 데이터 원본은 쿼리를 대화형으로 작성하는 데 도움이 되는 그래픽 디자이너를 지원하고 다른 데이터 원본은 텍스트 기반 쿼리 디자이너를 사용합니다. 그래픽 쿼리 디자이너를 사용하면 데이터 원본에서 기본 데이터를 나타내는 메타데이터 항목을 쿼리 디자인 화면으로 끌 수 있습니다. 텍스트 기반 쿼리 디자이너를 사용하면 쿼리 창에 명령 텍스트를 입력할 수 있습니다. 도구 모음의 텍스트 기반 쿼리 디자이너 아이콘을 클릭하여 그래픽 쿼리 디자이너에서 텍스트 기반 쿼리 디자이너로 변경할 수 있습니다.  
  
 보고서에 사용할 수 있는 데이터 원본 유형은 클라이언트 또는 보고서 서버에 설치된 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 확장 프로그램에 따라 다릅니다. 자세한 내용은 참조 [RSReportDesigner 구성 파일](report-server/rsreportdesigner-configuration-file.md) 및 [RSReportServer 구성 파일](report-server/rsreportserver-config-configuration-file.md)합니다.  
  
 데이터 처리 확장 프로그램 및 연결된 쿼리 디자이너는 데이터 원본에 대한 지원이 다음과 같이 서로 다를 수 있습니다.  
  
-   **쿼리 디자이너 유형별.** 예를 들어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 원본은 그래픽 기반 쿼리 디자이너와 텍스트 기반 쿼리 디자이너를 모두 지원합니다.  
  
-   **쿼리 언어 변형별.** 예를 들어 [!INCLUDE[tsql](../includes/tsql-md.md)] 과 같은 쿼리 언어는 데이터 원본 유형에 따라 구문이 달라질 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] 언어 및 Oracle SQL 언어의 경우 쿼리 명령에 대해 구문이 약간 달라질 수 있습니다.  
  
-   **데이터베이스 개체 이름의 스키마 부분 지원별.** 데이터 원본에서 스키마를 데이터베이스 개체 식별자의 일부로 사용하는 경우 기본 스키마를 사용하지 않는 모든 이름에 대해 스키마 이름을 쿼리의 일부로 제공해야 합니다. `SELECT FirstName, LastName FROM [Person].[Person]`)을 입력합니다.  
  
-   **쿼리 매개 변수 지원별.** 데이터 공급자에 따라 매개 변수 지원이 다릅니다. 일부 데이터 공급자는 명명된 매개 변수(예: `SELECT Col1, Col2 FROM Table WHERE <parameter identifier><parameter name> = <value>`)를 지원합니다. 다른 데이터 공급자는 명명되지 않은 매개 변수(예: `SELECT Col1, Col2 FROM Table WHERE <column name> = ?`)를 지원합니다. 매개 변수 식별자는 데이터 공급자; 따라 달라질 수 있음 예를 들어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용 하는 "at" (@) 기호를 Oracle은 콜론 (:)를 사용 하 합니다. 매개 변수를 지원하지 않는 데이터 공급자도 있습니다.  
  
-   **쿼리 가져오기 기능별.** 예를 들어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 원본의 경우 보고서 정의 파일(.rdl) 또는 .sql 파일에서 쿼리를 가져올 수 있습니다.  
  
## <a name="query-designers"></a>쿼리 디자이너  
 다음 항목에서는 각 쿼리 디자이너의 사용자 인터페이스에 대해 설명합니다.  
  
-   [Analysis Services MDX 쿼리 디자이너 사용자 인터페이스](report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
-   [Analysis Services DMX 쿼리 디자이너 사용자 인터페이스](report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
-   [그래픽 쿼리 디자이너 사용자 인터페이스](report-data/graphical-query-designer-user-interface.md)  
  
-   [관계형 쿼리 디자이너 사용자 인터페이스](../../2014/reporting-services/relational-query-designer-user-interface.md)  
  
-   [Hyperion Essbase 쿼리 디자이너 사용자 인터페이스](report-data/hyperion-essbase-query-designer-user-interface.md)  
  
-   [보고서 모델 쿼리 디자이너 사용자 인터페이스](report-data/report-model-query-designer-user-interface.md)  
  
-   [SAP NetWeaver BI 쿼리 디자이너 사용자 인터페이스](report-data/sap-netweaver-bi-query-designer-user-interface.md)  
  
-   [SharePoint 목록 쿼리 디자이너](../../2014/reporting-services/sharepoint-list-query-designer.md)  
  
-   [텍스트 기반 쿼리 디자이너 사용자 인터페이스](../../2014/reporting-services/text-based-query-designer-user-interface.md)  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services에서 지 원하는 데이터 원본 &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md)   
 [데이터 처리 확장 프로그램과.NET Framework 데이터 공급자 &#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)   
 [확장 &#40;SSRS&#41;](extensions-ssrs.md)  
  
  