---
title: 공유 데이터 세트 관리 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 2cbb1fa3-959e-4df6-9887-ebc93cc1b686
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 04591d5c1d44f0655d0f8dac0743a0e3d0cf6c55
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51814216"
---
# <a name="manage-shared-datasets"></a>공유 데이터 세트 관리
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 공유 데이터 집합은 외부 데이터 원본에 연결되는 공유 데이터 원본에서 데이터를 검색합니다. 공유 데이터 세트를 사용하면 쿼리를 공유하여 여러 보고서에서 일관성 있는 데이터 세트를 제공할 수 있습니다. 데이터 세트 쿼리에는 데이터 세트 매개 변수를 포함할 수 있습니다. 처음 사용할 때 또는 일정을 지정하여 특정 매개 변수 조합에 대해 쿼리 결과를 캐시하도록 공유 데이터 세트를 구성할 수 있습니다. 공유 데이터 세트 캐싱을 보고서 캐싱 및 보고서 데이터 피드와 함께 사용하면 데이터 원본에 대한 액세스를 쉽게 관리할 수 있습니다.  
  
 공유 데이터 세트는 포함된 데이터 원본이 아닌 공유 데이터 원본만을 사용합니다. 공유 데이터 세트는 지원되는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 확장 프로그램 또는 보고서 모델에서 모든 데이터 원본을 기반으로 할 수 있습니다.  
  
## <a name="creating-and-using-shared-datasets"></a>공유 데이터 세트 만들기 및 사용  
 공유 데이터 집합을 만들려면 공유 데이터 집합 정의 파일(.rsd)을 만드는 애플리케이션을 사용해야 합니다. 다음 애플리케이션 중 하나를 사용하여 공유 데이터 집합을 만들 수 있습니다.  
  
-   보고서 작성기   공유 데이터 세트 디자인 모드를 사용하여 공유 데이터 세트를 보고서 서버나 SharePoint 사이트에 저장합니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 보고서 디자이너   솔루션 탐색기의 공유 데이터 집합 폴더에 공유 데이터 집합을 만듭니다. 공유 데이터 세트를 게시하려면 보고서 서버 또는 SharePoint 사이트에 배포합니다.  
  
-   공유 데이터 세트 정의 파일(.rsd) 업로드   파일을 보고서 서버 또는 SharePoint 사이트로 업로드할 수 있습니다. SharePoint 사이트에 업로드된 파일은 공유 데이터 세트가 캐시되거나 보고서에서 사용되기 전까지는 스키마에 대해 유효성이 검사되지 않습니다.  
  
 공유 데이터 세트 정의에는 쿼리, 기본값을 포함하는 데이터 세트 매개 변수, 대/소문자 구분과 같은 데이터 옵션 및 데이터 세트 필터가 포함됩니다. 정의에서 설정하는 값은 공유 데이터 세트가 보고서에 포함될 때마다 사용됩니다.  
  
 보고서에서 공유 데이터 집합을 사용하려면 보고서 작성기와 같은 애플리케이션을 열고 보고서 서버 또는 SharePoint 사이트로 이동하여 공유 데이터 집합을 선택합니다. 이렇게 하면 보고서에 공유 데이터 세트의 인스턴스가 추가됩니다. 보고서에서 공유 데이터 세트에 대한 쿼리 또는 공유 데이터 원본을 보거나 변경할 수 없습니다. 보고서의 인스턴스에 적용할 일련의 데이터 세트 속성 값을 추가로 지정할 수 있습니다. 예를 들어 필터를 추가하거나 대/소문자 구분과 같은 데이터 옵션을 변경할 수 있습니다. 자세한 내용은 msdn.microsoft.com의 [보고서 작성기 설명서](https://go.microsoft.com/fwlink/?LinkId=154494)에서 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="managing-shared-datasets"></a>공유 데이터 세트 관리  
 게시된 공유 데이터 집합의 속성을 관리하려면 기본 모드 보고서 서버에 대한 보고서 관리자를 사용하거나 보고서 서버를 SharePoint 통합 모드로 배포한 경우 SharePoint 사이트의 애플리케이션 페이지를 사용할 수 있습니다. 공유 데이터 세트에서 수행할 수 있는 태스크는 역할 할당, 사이트 수준 및 항목 수준 사용 권한(사용 권한 상속이 적용되는 경우에는 폴더에 대한 사용 권한 포함)에 따라 달라집니다. 공유 데이터 세트에 대한 항목 수준 보안은 보고서에 대한 항목 수준 보안과 동일한 모델을 사용합니다. 자세한 내용은 [공유 데이터 세트 항목 보안 설정](../../reporting-services/security/secure-shared-dataset-items.md)을 참조하세요.  
  
 공유 데이터 세트를 사용하는 보고서나 공유 데이터 세트가 종속되는 공유 데이터 원본과는 별도로 사용할 공유 데이터 원본을 포함하여 공유 데이터 세트 항목의 속성을 관리할 수 있습니다. 공유 데이터 세트 정의의 일부인 기타 데이터 세트 속성이나 쿼리를 변경하려면 정의를 편집해야 합니다.  
  
### <a name="manage-shared-dataset-item-properties"></a>공유 데이터 세트 항목 속성 관리  
 다음 표에서는 공유 데이터 세트 항목에 대해 변경할 수 있는 항목 속성을 나열합니다.  
  
|||  
|-|-|  
|이름 편집|공유 데이터 세트의 이름을 변경합니다. 종속 항목에서의 참조는 계속 작동합니다.|  
|설명 편집|공유 데이터 세트에 대한 설명을 변경합니다.|  
|쿼리 실행 제한 시간 편집|쿼리 실행 제한 시간(초)을 설정합니다. 0초는 시간 제한이 없음을 의미합니다. 데이터 세트 쿼리 시간이 초과되기 전까지의 시간(초)을 결정합니다. 제한 시간 값을 지정하지 않으려면 0을 사용합니다. 자세한 내용은 [보고서 및 공유 데이터 집합 처리에 대한 제한 시간 값 설정&#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)를 참조하세요.|  
|종속 항목 보기|게시된 보고서 파트, 공유 데이터 원본 및 보고서와 같은 공유 데이터 세트를 사용하는 항목을 볼 수 있습니다.|  
  
 다음과 같은 추가 공유 데이터 세트 속성이 자동으로 구성됩니다.  
  
|속성|설명|  
|--------------|-----------------|  
|HasDataSourceCredentials|보고서 서버에 연결된 공유 데이터 원본에 대한 자격 증명이 저장되는지 여부를 지정합니다.|  
|HasUserProfileDependencies|보고서의 쿼리 또는 필터 식에 User 전역 컬렉션에 대한 참조가 있는지 여부를 지정합니다.|  
  
## <a name="viewing-or-changing-the-shared-dataset-definition"></a>공유 데이터 세트 정의 보기 또는 변경  
 쿼리, 데이터 세트 매개 변수, 기본값, 데이터 세트 필터, 데이터 정렬 및 대/소문자 구분 등의 데이터 옵션을 포함하여 공유 데이터 세트 속성이 공유 데이터 세트 정의에 저장됩니다. 충분한 사용 권한이 있는 경우 정의를 보고 변경할 수 있습니다.  
  
 공유 데이터 집합 정의를 보거나 변경하려면 공유 데이터 집합 디자인 모드에서 보고서 작성기와 같은 애플리케이션을 사용하여 공유 데이터 집합을 편집합니다. 공유 데이터 세트 정의를 변경한 후에는 서버나 사이트에 정의를 다시 저장합니다.  
  
 XML에서 공유 데이터 세트 정의를 보는 또 다른 방법은 보고서 관리자에서 URL 액세스 구문을 사용하는 것입니다. 예를 들어 각 데이터 세트 매개 변수에 대한 기본값을 보려면 다음 URL 액세스 명령을 사용하여 보고서 서버에서 DataSet1이라는 공유 데이터 세트 정의를 표시할 수 있습니다.  
  
```  
https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
```  
  
## <a name="controlling-access-to-the-shared-dataset-definition"></a>공유 데이터 세트 정의에 대한 액세스 제어  
 기본적으로 다음 태스크는 공유 데이터 세트에 대한 작업에 적용됩니다.  
  
-   **보고서 보기** 공유 데이터 집합 항목 및 항목 속성을 봅니다.  
  
-   **보고서 사용** 공유 데이터 집합의 정의를 읽습니다.  
  
-   **보고서 관리** 공유 데이터 집합을 만들고 삭제하며 공유 데이터 집합의 속성을 편집합니다.  
  
-   **항목의 보안 설정** 공유 데이터 집합에 대한 보안 설정을 보고 수정합니다.  
  
 기본 모드 보고서 서버의 데이터 원본 속성에 대한 액세스를 제어하는 태스크 및 사용 권한에 대한 자세한 내용은 [공유 데이터 세트 항목 보안 설정](../../reporting-services/security/secure-shared-dataset-items.md)을 참조하세요.  
  
 SharePoint 라이브러리의 항목에 대한 속성을 보고 편집할 수 있는 권한은 사이트 관리자에 의해 결정됩니다. 자세한 내용은 [보고서 서버 항목에 대한 SharePoint 사이트 및 목록 사용 권한 참조](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)를 참조하세요.  
  
## <a name="how-to-work-with-shared-dataset-properties-on-a-report-server"></a>보고서 서버에서 공유 데이터 세트 속성을 사용하는 방법  
 다양한 도구를 사용하여 공유 데이터 세트 작업을 할 수 있습니다. 다음 표에서는 접근 방법과 도구를 요약하여 설명하고 추가 지침에 대한 링크를 제공합니다.  
  
|태스크|도구|링크|  
|----------|----------|----------|  
|공유 데이터 세트를 추가하거나 공유 데이터 세트 정의 속성을 변경합니다.|보고서 작성기에서 저장<br /><br /> 보고서 디자이너에서 배포<br /><br /> 보고서 관리자에서 .rsd 파일 업로드|msdn.microsoft.com의 [보고서 작성기 설명서](https://go.microsoft.com/fwlink/?LinkId=154494)에서 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)<br /><br /> [파일 업로드 페이지&#40;보고서 관리자&#41;](https://msdn.microsoft.com/library/7bb3166f-9374-4449-b66a-ffb77298507d)<br /><br /> 공유 데이터 세트를 공유 데이터 세트가 종속되어 있는 공유 데이터 원본보다 먼저 업로드하는 경우 공유 데이터 세트를 공유 데이터 원본에 수동으로 바인딩해야 합니다. 자세한 내용은 msdn.microsoft.com의 [일반 속성 페이지, 공유 데이터 집합&#40;보고서 관리자&#41;](https://msdn.microsoft.com/library/10798e41-24c3-4e69-893b-7ee6af7fc958)을 참조하세요.|  
|공유 데이터 세트 항목 속성을 변경합니다.|보고서 관리자|[일반 속성 페이지, 공유 데이터 집합&#40;보고서 관리자&#41;](https://msdn.microsoft.com/library/10798e41-24c3-4e69-893b-7ee6af7fc958)|  
|보고서의 공유 데이터 세트 인스턴스에 대한 추가 공유 데이터 세트 속성을 지정합니다.|보고서 작성기 보고서 디자이너|[데이터 집합 속성 대화 상자, 쿼리](https://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f)|  
|공유 데이터 세트의 다른 공유 데이터 원본에 바인딩합니다.|보고서 관리자|[데이터 원본 선택 페이지&#40;보고서 관리자&#41;](https://msdn.microsoft.com/library/7f7e8b19-0c0b-4b1f-9cc1-057099aa07eb)|  
|데이터 세트 매개 변수의 기본값을 확인합니다.|보고서 작성기에서 열기 또는 URL 액세스 구문 사용|예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> `https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition`|  
|캐싱 설정|보고서 관리자|[공유 데이터 집합 캐시&#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)<br /><br /> [캐싱 페이지, 공유 데이터 집합&#40;보고서 관리자&#41;](https://msdn.microsoft.com/library/eac372e9-d2a1-48a8-bbe5-09d101df16ea)|  
|캐시 새로 고침 계획 만들기 또는 편집|보고서 관리자|[캐시 새로 고침 옵션&#40;보고서 관리자&#41;](https://msdn.microsoft.com/library/227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6)|  
|공유 데이터 세트 정의 스키마를 봅니다.|보고서 관리자|`https://<reportserver>/shareddatasetdefinition.xsd`|  
|SharePoint 통합 모드에서 보고서 서버와 SharePoint 사이트 간의 공유 데이터 세트 정의 동기화|SharePoint 애플리케이션 페이지|공유 데이터 세트 항목 속성 변경<br /><br /> 캐시 옵션 변경<br /><br /> 공유 데이터 원본 변경|  
  
## <a name="comparing-shared-datasets-with-other-report-server-items"></a>공유 데이터 세트와 다른 보고서 서버 항목 비교  
 보고서 서버에서 여러 유형의 항목을 관리할 때 항목과 다른 보고서 서버 항목의 유사성 및 차이점을 이해하는 것이 도움이 됩니다.  
  
 공유 데이터 세트는 다음과 같은 면에서 공유 데이터 원본 및 보고서와 유사합니다.  
  
-   공유 데이터 원본과 마찬가지로 공유 데이터 세트는 공유 데이터 세트가 사용되는 보고서와는 별도로 관리됩니다. 보고서 서버에서의 공유 데이터 세트 관리에는 공유 데이터 세트 정의를 편집하지 않고 공유 데이터 세트가 종속되는 공유 데이터 원본을 변경할 수 있는 기능이 포함됩니다.  
  
-   보고서와 마찬가지로 공유 데이터 세트도 캐시할 수 있습니다. 데이터 원본에서 필요로 하는 자격 증명은 캐싱 제한 사항을 충족해야 하며 모든 매개 변수에 대해 기본값이 지정되어야 합니다. 자세한 내용은 msdn.microsoft.com의 [공유 데이터 집합 캐시&#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)을 참조하세요.  
  
-   보고서와 마찬가지로 처리가 발생할 때마다 보고서 서버 항목의 현재 정의가 사용됩니다. 공유 데이터 세트를 변경하는 경우 해당 항목을 사용하는 각 보고서는 보고서가 처리될 때 보고서 서버에 있는 현재 정의를 사용합니다. 공유 데이터 세트에 대해 캐싱이 설정되어 있는 경우 공유 데이터 세트 정의를 변경하면 이러한 변경 사항은 캐시에 있는 데이터가 만료될 때까지 적용되지 않습니다. 캐시 새로 고침 계획을 사용하여 여러 보고서에 대해 일관성 있는 데이터 집합을 제공할 수 있습니다.  
  
 공유 데이터 세트는 다음과 같은 면에서 게시된 보고서 파트와 차이가 있습니다.  
  
-   게시된 보고서 파트와 달리 보고서 서버의 공유 데이터 세트 정의에 대한 변경 사항은 보고서 제작 클라이언트에서 보고서가 열릴 때 업데이트 알림을 트리거하지 않습니다. 보고서를 실행하면 보고서 서버의 현재 공유 데이터 세트 정의에서 데이터가 사용됩니다.  
  
 공유 데이터 세트는 다음과 같은 면에서 구독과 유사합니다.  
  
-   공유 데이터 세트는 캐싱에 항목별 일정 및 공유 일정을 사용할 수 있습니다.  
  
-   공유 데이터 세트는 매개 변수 값 지정에 구독과 동일한 규칙을 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
