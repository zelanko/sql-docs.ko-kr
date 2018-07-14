---
title: XML 연결 형식(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5b55fff2-1b15-4156-83ef-15ad9cf9f509
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 17b03e4ca74b5aa8d9e59d6bcc32eafe4ef1139e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191803"
---
# <a name="xml-connection-type-ssrs"></a>XML 연결 형식(SSRS)
  보고서에 XML 데이터 원본의 데이터를 포함하려면 XML 유형의 보고서 데이터 원본에 기초하는 데이터 집합이 있어야 합니다. 이 기본 제공 데이터 원본 유형은 XML 데이터 확장 프로그램을 기반으로 합니다. 이 데이터 원본 유형을 사용하여 쿼리에 포함된 XML 문서, 웹 서비스 또는 XML에서 데이터에 연결하여 검색합니다.  
  
 이 데이터 확장 프로그램은 연결 문자열과 별개로 관리되는 자격 증명 및 매개 변수를 지원합니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결이 나 데이터 원본 추가 및 확인 &#40;보고서 작성기 및 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)합니다.  
  
##  <a name="Connection"></a> 연결 문자열  
 연결 문자열은 HTTP를 통해 사용할 수 있는 웹 서비스, 웹 기반 응용 프로그램 또는 XML 문서를 가리키는 URL이어야 합니다. XML 문서에는 XML 확장명을 사용해야 합니다. 데이터 집합 쿼리에 포함된 XML 데이터의 경우 빈 연결 문자열을 사용할 수도 있습니다.  
  
 다음 예에서는 웹 서비스 및 XML 문서에 대한 각각의 연결 문자열 구문을 보여 줍니다. `file://` 프로토콜은 지원되지 않습니다.  
  
|XML 문서 유형|연결 문자열 예|  
|-----------------------|-------------------------------|  
|웹 서비스|`http://adventure-works.com/results.aspx`|  
|XML 문서|`http://localhost/XML/Customers.xml`|  
|포함 XML 문서|*비어 있음*|  
  
 연결 문자열 예제는 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md)을 참조하세요.  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 보고서 작성 클라이언트에서는 다음 옵션을 사용하여 자격 증명을 지정할 수 있습니다.  
  
-   현재 Windows 사용자(통합 보안).  
  
-   자격 증명 필요 없음. 자격 증명을 사용하지 않도록 선택하는 경우 익명 액세스가 사용됩니다. 보고서 서버에서 외부 데이터 원본에 연결할 수 있도록 무인 실행 계정을 정의했는지 확인합니다. XML 데이터 처리 확장 프로그램에서는 자격 증명을 대상 URL이나 웹 서비스로 전달하지 않으므로 무인 실행 계정을 정의하지 않은 경우에는 연결이 실패합니다. 자세한 내용은 msdn.microsoft.com의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서의 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.  
  
 저장된 자격 증명 및 입력 정보를 요청하는 자격 증명은 지원되지 않습니다. Windows 통합 보안을 사용하지 않도록 설정한 경우 이를 사용하여 데이터를 검색할 수 없습니다. 저장된 자격 증명 및 입력 정보를 요청하는 자격 증명을 지정할 경우 런타임에 오류가 발생합니다.  
  
 자세한 내용은 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) 하거나 [보고서 작성기에 자격 증명 지정](../specify-credentials-in-report-builder.md)합니다.  
  
##  <a name="Query"></a> 쿼리  
 쿼리는 보고서 데이터 집합에 대해 검색할 데이터를 지정합니다. 쿼리 결과 집합의 열은 데이터 집합의 필드 컬렉션을 채웁니다. 보고서는 쿼리에서 검색된 첫 번째 결과 집합만 처리합니다.  
  
 쿼리를 만들려면 텍스트 기반 쿼리 디자이너를 사용해야 합니다. 쿼리는 XML 데이터를 반환해야 합니다.  
  
 텍스트 기반 쿼리 디자이너에 대한 자세한 내용은 [텍스트 기반 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](text-based-query-designer-user-interface-report-builder.md)를 참조하세요.  
  
 XML 형식의 데이터 원본에 대한 데이터 집합 쿼리에서 사용할 수 있는 값이 아래에 나와 있습니다.  
  
-   *빈*: 기본 결과 집합을 만들려면 빈 쿼리를 사용 합니다. 기본 쿼리는 데이터 원본을 읽고 XML 노드 계층에서 첫 번째 리프 컬렉션까지 탐색하도록 만들어집니다. 결과 집합에는 텍스트 값이 있는 모든 노드와 해당 경로의 모든 노드 특성이 포함됩니다. 결과 집합의 열은 데이터 집합의 필드에 매핑됩니다.  
  
-   요소 경로: 데이터 원본의 XML 데이터를 검색할 때 사용할 노드 시퀀스를 지정 합니다.  
  
-   XML 쿼리 요소가: 다음과 같은 선택적 요소를 사용 하 여 XML 쿼리 사양:  
  
    -   **웹 서비스:**  
  
         필요한 XML 요소:  
  
         `<Method Namespace=` *"namespace"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *soap action* `</SoapAction>`  
  
         선택적 XML 요소:  
  
         `<ElementPath>`  *element path*  `</ElementPath>`  
  
         `<Method Namespace=` *"namespace"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *soap action* `</SoapAction>`  
  
    -   **XML 문서:**  
  
         선택적 XML 요소:  
  
         `<ElementPath>`  *element path*  `</ElementPath>`  
  
    -   **포함 XML 문서의:**  
  
         필요한 XML 요소:  
  
         `<XmlData>` inner XML `</XmlData>`  
  
         선택적 XML 요소:  
  
         `<ElementPath>`  *element path*  `</ElementPath>`  
  
         `-- or --`  
  
         `<ElementPath IgnoreNamespaces="true">`  *element path*  `</ElementPath>`  
  
 쿼리 구문에 대한 자세한 내용은 msdn.microsoft.com의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서의 [XML 보고서 데이터를 위한 XML 쿼리 구문&#40;SSRS&#41;](report-data-ssrs.md)을 참조하세요.  
  
 예를 보려면 [Reporting Services: XML 및 웹 서비스 데이터 원본 사용(Reporting Services: Using XML and Web Service Data Sources)](http://go.microsoft.com/fwlink/?LinkId=81654)을 참조하십시오.  
  
### <a name="requirements-for-retrieving-xml-web-service-data"></a>XML 웹 서비스 데이터 검색을 위한 요구 사항  
 XML 데이터 처리 확장 프로그램은 스키마를 검색하지 않습니다. 따라서 다른 방법으로 원하는 데이터를 검색할 SOAP 메서드를 찾아야 합니다. 또한 웹 서비스에서 해당 데이터에 사용하는 주소 지정 스키마나 네임스페이스에 대해 이해하고 있어야 합니다.  
  
 웹 서비스의 경우 호출할 메서드나 SOAP 동작을 지정하는 <`Query`> 요소를 지정할 수 있습니다. XML 데이터 원본에 보고서에 사용할 데이터를 생성하는 계층 구조가 있는 경우 쿼리를 비워 두고 기본 쿼리를 사용할 수 있습니다. 쿼리가 실행될 때 검색되는 XML 요소 노드 값 및 특성은 보고서에서 사용하는 데이터 집합 필드에 매핑됩니다.  
  
### <a name="requirements-for-retrieving-xml-document-data"></a>XML 문서 데이터 검색을 위한 요구 사항  
 http 프로토콜을 사용할 경우 서버에서 XML 데이터를 반환하거나 XML 데이터가 XML `Query` 요소에 포함되어 있어야 합니다. http 프로토콜을 사용하여 XML 문서를 직접 참조하려면 해당 문서의 확장명이 .xml이어야 합니다.  
  
 필요한 모든 데이터를 검색하는 XML 쿼리를 만드는 방법을 알고 있어야 합니다. 요소 경로를 지정하지 않으면 XML 문서를 구문 분석하는 기본 동작에 따라 XML 문서의 리프 노드 컬렉션에 대한 첫 번째 사용 가능 경로가 선택됩니다. XML 문서에 다른 형제 리프 노드 컬렉션에 대한 추가 경로가 포함되어 있는 경우 쿼리에 경로를 지정하지 않으면 해당 노드는 무시됩니다.  
  
 XQuery와 유사한 XML 구문을 사용하여 요소 경로를 지정할 수 있습니다.  
  
 자세한 내용은 msdn.microsoft.com의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서의 [XML 보고서 데이터를 위한 요소 경로 구문&#40;SSRS&#41;](element-path-syntax-for-xml-report-data-ssrs.md)을 참조하세요.  
  
##  <a name="Parameters"></a> 매개 변수  
 쿼리는 매개 변수 식별을 위해 분석되지 않습니다.  
  
 매개 변수를 추가하려면 **데이터 집합 속성** 대화 상자의 [매개 변수](../dataset-properties-dialog-box-parameters-report-builder.md) 페이지를 통해 직접 만들어야 합니다.  
  
##  <a name="Remarks"></a> 주의  
 XML 데이터 확장 프로그램은 계층 구조가 아닌 테이블 형식 XML 데이터의 보고를 지원합니다. 자세한 내용은 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 XML 문서를 검색하는 작업은 기본적으로 지원되지 않습니다.  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 집합을 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결이 나 데이터 원본 추가 및 확인 &#40;보고서 작성기 및 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 집합에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
##  <a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 집합 및 공유 데이터 집합에 대한 정보를 제공합니다.  
  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 쿼리에 의해 생성되는 데이터 집합 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)에 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서의 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
