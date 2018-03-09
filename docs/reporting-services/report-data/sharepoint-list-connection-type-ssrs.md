---
title: "SharePoint 목록 연결 형식(SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2c4adf2f-e9c4-4fae-bd3c-97fe64436caf
caps.latest.revision: 
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ba9625e6d50c14ee47070b4980e6b376cc68e738
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="sharepoint-list-connection-type-ssrs"></a>SharePoint 목록 연결 형식(SSRS)

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)] [!INCLUDE [ssrs-appliesto-sharepoint-2013-2016](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Microsoft SharePoint 목록의 데이터를 보고서에 포함하려면 Microsoft SharePoint 목록 유형의 보고서 데이터 원본을 기반으로 하는 데이터 집합을 추가하거나 만들어야 합니다. 이는 Microsoft SQL Server Reporting Services SharePoint 목록 데이터 확장 프로그램을 기반으로 하는 기본 제공 데이터 원본 유형입니다. 이 데이터 원본 유형을 사용하여 SharePoint 2013 이상에 연결하여 목록 데이터를 검색합니다.

이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  

##  <a name="Connection"></a> 연결 문자열  
 SharePoint 목록에 대한 연결 문자열은 SharePoint 사이트 또는 하위 사이트에 대한 URL입니다(예: `http://MySharePointWeb/MySharePointSite` 또는 `http://MySharePointWeb/MySharePointSite/Subsite`).  
  
 쿼리 디자이너는 사용자가 액세스할 수 있는 권한이 있는 SharePoint 목록을 자동으로 표시합니다.  
  
 연결 문자열 예제는 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)을 참조하세요.  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다. 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다. 이 데이터 확장 프로그램과 함께 사용할 수 있는 자격 증명의 유형은 데이터 원본으로 사용 중인 SharePoint 목록에 대한 SharePoint 기술 구성에 따라 다릅니다.  
  
 다음 표에서는 로컬 팜 SharePoint 목록 및 원격 SharePoint 목록에 연결할 때 SharePoint 목록 확장에 대한 자격 증명 검색 동작을 보여 줍니다.  
  
 **표 1** 은 레거시 Windows SharePoint 사이트에 배포되는 보고서에 대한 것입니다. 레거시 Windows 사이트는 Kerberos, NTLM 및 FBA(Forms Based Authentication)만 지원합니다. **표 2** 는 클레임 기반 SharePoint 사이트에 배포되는 보고서에 대한 것입니다.  
  
 **표 1**  
  
||지원되는 자격 증명|클래식 모드 Windows 인증|*클레임 인증|  
|-|---------------------------|-----------------------------------------|-----------------------------|  
|로컬 팜 SharePoint 팜 목록|Windows 인증(통합) 또는 SharePoint 사용자 토큰|예|예|  
||저장됨, 프롬프트, 없음(Windows 자격 증명 사용)<br /><br /> Windows 자격 증명이 아닌 다른 자격 증명이 포함된 저장된 자격 증명 및 프롬프트 자격 증명은 지원되지 않습니다.|예|아니오|  
|원격 SharePoint 목록|Windows 인증(통합) 또는 SharePoint 사용자 토큰|예|아니오<br /><br /> 폼 기반 인증 및 클레임 인증은 원격 SharePoint 목록에 지원되지 않습니다.|  
||저장됨, 프롬프트, 없음(Windows 자격 증명 사용)<br /><br /> Windows 자격 증명이 아닌 다른 자격 증명이 포함된 저장된 자격 증명 및 프롬프트 자격 증명은 지원되지 않습니다.|예|아니오<br /><br /> 폼 기반 인증 및 클레임 인증은 원격 SharePoint 목록에 지원되지 않습니다.|  
  
 *Windows 인증, FBA(폼 기반 인증), SAML(Secure Application Markup Language) 토큰, 기타 ID 공급자 또는 위에 명시된 인증 공급자 중 둘 이상의 조합입니다.  
  
 **표 2**  
  
||지원되는 자격 증명|클래식 모드 Windows 인증|*클레임 인증|  
|-|---------------------------|-----------------------------------------|-----------------------------|  
|로컬 팜 SharePoint 팜 목록|Windows 인증(통합) 또는 SharePoint 사용자 토큰|예|예|  
||저장됨, 프롬프트, 없음(Windows 자격 증명 사용)<br /><br /> Windows 자격 증명이 아닌 다른 자격 증명이 포함된 저장된 자격 증명 및 프롬프트 자격 증명은 지원되지 않습니다.|아니오|아니오|  
|원격 SharePoint 목록|Windows 인증(통합) 또는 SharePoint 사용자 토큰|예|아니오<br /><br /> 폼 기반 인증 및 클레임 인증은 원격 SharePoint 목록에 지원되지 않습니다.|  
||저장됨, 프롬프트, 없음(Windows 자격 증명 사용)<br /><br /> Windows 자격 증명이 아닌 다른 자격 증명이 포함된 저장된 자격 증명 및 프롬프트 자격 증명은 지원되지 않습니다.|아니오|아니오<br /><br /> 폼 기반 인증 및 클레임 인증은 원격 SharePoint 목록에 지원되지 않습니다.|  
  
 *Windows 인증, FBA(폼 기반 인증), SAML(Secure Application Markup Language) 토큰, 기타 ID 공급자 또는 위에 명시된 인증 공급자 중 둘 이상의 조합입니다.  
  
 **Windows 인증**  
 트러스트된 계정 모드에서 보고서 서버와 함께 작동하도록 구성된 SharePoint 기술의 경우 이 옵션은 지원되지 않습니다. 이 옵션은 SQL Server 2012 Reporting Services 이전 릴리스에만 적용됩니다.

 Windows 통합 모드에서 보고서 서버와 함께 작동하도록 구성된 SharePoint 기술의 경우 이 옵션은 현재 Windows 사용자 및 현재 SharePoint 사용자 둘 다에 적용됩니다.
 
 보고서 서버(로컬 모드) 없이 작동하도록 구성된 SharePoint 기술의 경우 이 옵션은 지원되지 않습니다. 로컬 모드에 대한 자세한 내용은 [보고서 뷰어의 로컬 모드와 보고서 뷰어의 연결 모드 보고서&#40;SharePoint 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)를 참조하세요.  
  
 **자격 증명 필요 없음(자격 증명 사용 안 함):**  
 이 옵션을 사용하려면 보고서 서버에서 무인 실행 계정을 구성해야 합니다. 자세한 내용은 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.  
  
 Microsoft BI 스택 간 클레임 인증 지원에 대한 자세한 내용은 [Microsoft BI 스택 간 클레임 인증 사용](http://social.technet.microsoft.com/wiki/contents/articles/15274.using-claims-authentication-across-the-microsoft-bi-stack.aspx)을 참조하십시오.  
  
 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md), [보고서 작성기에 자격 증명 지정](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53) 또는 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)을 참조하세요.  
  
##  <a name="Query"></a> 쿼리  
 쿼리를 디자인하려면 데이터 원본을 기준으로 새 데이터 집합을 만든 다음 연결된 쿼리 디자이너를 엽니다. 자세한 내용은 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)을 참조하세요.  
  
 SharePoint 목록 그래픽 쿼리 디자이너에는 4개의 창이 표시됩니다.  
  
 **SharePoint 목록**  이 데이터 원본에 대해 사이트의 모든 SharePoint 목록이 포함된 목록을 표시합니다. 목록을 선택한 다음 쿼리에 포함할 필드를 선택합니다. 이 창의 필드 이름은 SharePoint 이름(표시 이름)입니다. 항목 위로 마우스를 이동하면 도구 설명에 다음 속성이 표시됩니다.  
  
-   **이름** 필드의 고유 이름입니다.  
  
-   **식별자** 필드의 고유 식별자입니다.  
  
-   **필드 형식** 필드의 데이터 형식입니다.  
  
-   **숨김** 필드가 SharePoint 목록 보기에 표시되는지 여부입니다.  
  
 여러 목록에서 필드를 선택할 수는 없습니다. 각 목록에 대해 데이터 집합을 만들고 각 데이터 집합에서 필드를 선택할 수 있습니다. 목록에 공용 필드가 있는 경우, 한 데이터 집합에 바인딩된 테이블릭스 데이터 영역에서 Lookup 함수를 사용하여 데이터 영역에 바인딩되지 않는 다른 데이터 집합의 값을 검색할 수 있습니다. 자세한 내용은 [조회 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md)를 참조하세요.  
  
-   **선택한 필드**  선택한 필드를 표시합니다. 이 창의 필드 이름은 SharePoint 사용자가 지정한 이름입니다. 쿼리 디자이너를 닫으면 이 이름이 보고서 데이터 창의 데이터 집합 필드 모음에 표시됩니다. 고유 이름과 이름 간의 관계는 [데이터 집합 속성 대화 상자, 필드&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42) 페이지에 나와 있습니다.  
  
-   **적용된 필터**  SharePoint 목록에서 반환되는 데이터를 보고서로 반환하기 전에 제한합니다. 사용할 필드 이름, 연산자 및 값을 선택하여 목록에서 검색되는 데이터를 제한합니다. 연산자는 선택한 값의 데이터 형식에 따라 달라집니다.  
  
     그래픽 쿼리 디자이너에서는 정렬 순서를 변경하거나 그룹을 지정할 수 없습니다. 이렇게 하려면 보고서 데이터 집합에 대해 정렬 식을 설정하고 보고서의 데이터 영역에서 식을 그룹화합니다. 쿼리 매개 변수는 지원되지 않습니다. 보고서의 데이터를 필터링하려면 보고서 필터 또는 보고서 매개 변수를 만들어서 사용하십시오. 자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) 및 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)을 참조하세요.  
  
-   **쿼리 결과**  쿼리 실행 시 반환되는 예제 행을 표시합니다. SharePoint 사이트에서 SharePoint 목록 값이 자주 변경되는 경우 쿼리 결과 창에 표시되는 값과 보고서에 표시되는 값이 다를 수 있습니다.  
  
-   **선택한 필드**  선택한 필드를 표시합니다. 이 창의 필드 이름은 SharePoint 사용자가 지정한 이름입니다. 쿼리 디자이너를 닫으면 이 이름이 보고서 데이터 창의 데이터 집합 필드 모음에 표시됩니다. 고유 이름과 이름 간의 관계는 [데이터 집합 속성 대화 상자, 필드&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42) 페이지에 나와 있습니다.  
  
-   **적용된 필터**  SharePoint 목록에서 반환되는 데이터를 보고서로 반환하기 전에 제한합니다. 사용할 필드 이름, 연산자 및 값을 선택하여 목록에서 검색되는 데이터를 제한합니다. 연산자는 선택한 값의 데이터 형식에 따라 달라집니다.  
  
     그래픽 쿼리 디자이너에서는 정렬 순서를 변경하거나 그룹을 지정할 수 없습니다. 이렇게 하려면 보고서 데이터 집합에 대해 정렬 식을 설정하고 보고서의 데이터 영역에서 식을 그룹화합니다. 쿼리 매개 변수는 지원되지 않습니다. 보고서의 데이터를 필터링하려면 보고서 필터 또는 보고서 매개 변수를 만들어서 사용하십시오. 자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) 및 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)을 참조하세요.  
  
-   **쿼리 결과**  쿼리 실행 시 반환되는 예제 행을 표시합니다. SharePoint 사이트에서 SharePoint 목록 값이 자주 변경되는 경우 쿼리 결과 창에 표시되는 값과 보고서에 표시되는 값이 다를 수 있습니다.  
  
 자세한 내용은 [SharePoint 목록 쿼리 디자이너&#40;보고서 작성기&#41;](../../reporting-services/report-data/sharepoint-list-query-designer-report-builder.md)를 참조하세요.  
  
### <a name="query-text"></a>쿼리 텍스트  
 그래픽 쿼리 디자이너에서 생성한 쿼리를 보려면 텍스트 기반 쿼리 디자이너로 전환합니다. 이 보기에서 그래픽 쿼리 디자이너가 만든 XML을 볼 수 있습니다. XML에는 목록 이름, 필드, 모음 및 필터 요소가 포함되어 있습니다.  
  
#### <a name="example-1-specified-fields-for-a-list"></a>예 1. 목록의 지정된 필드  
 다음 예제에서는 올바른 형식의 SharePoint 쿼리를 보여 줍니다.  
  
```  
<RSSharePointList>  
<listName>MyList</listName>  
<viewFields>  
  <FieldRef Name="Field1"/>  
  <FieldRef Name="Field4"/>  
</viewFields>  
<Query>  
  <Where>  
    <And>  
      <Gt>  
        <FieldRef Name="Field1"/>  
        <Value Type="Integer">1</Value>  
      </Gt>  
      <IsNotNull>  
        <FieldRef Name="Field2"/>  
        <Value Type="string"/>  
      </IsNotNull>   
    </And>  
  </Where>  
</Query>  
</RSSharePointList>  
```  
  
 올바른 형식의 XML 텍스트를 유지하면서 이 쿼리 보기를 편집할 수 있습니다.  
  
#### <a name="example-2-all-fields-for-a-list"></a>예 2. 목록의 모든 필드  
 목록의 이름만 지정할 수도 있습니다. 그러면 숨겨진 필드를 비롯해 모든 필드가 반환됩니다. 다음 예에서는 Tasks라는 목록의 모든 필드를 검색합니다.  
  
```  
<RSSharePointList>  
<listName>Tasks</listName>  
</RSSharePointList>  
```  
  
 Tasks 목록의 모든 필드가 쿼리 결과에 반환됩니다.  
  
##  <a name="Parameters"></a> 매개 변수  
 이 데이터 확장 프로그램은 매개 변수를 지원하지 않습니다.  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 집합을 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 집합에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
##  <a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 집합 및 공유 데이터 집합에 대한 정보를 제공합니다.  
  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 쿼리에 의해 생성되는 데이터 집합 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)에 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서의 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  

## <a name="see-also"></a>참고 항목

[보고서 매개 변수](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
[데이터 필터링, 그룹화 및 정렬](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
[식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
