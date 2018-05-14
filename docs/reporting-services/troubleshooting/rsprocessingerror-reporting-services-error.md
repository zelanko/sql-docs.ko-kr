---
title: rsProcessingError - Reporting Services 오류 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: troubleshooting
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- rsProcessingError
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d00747808949e7814ecd87c640d10ca3b8e54e97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="rsprocessingerror---reporting-services-error"></a>rsProcessingError - Reporting Services 오류
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|rsProcessingError|  
|이벤트 원본|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|구성 요소|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|메시지 텍스트|보고서를 처리하는 동안 오류가 발생했습니다.|  
  
## <a name="explanation"></a>설명  
 보고서 게시, 보고서 처리, 로컬에서 보고서 미리 보기, 보고서 서버에서 보고서 보기 또는 보고서에 대한 구독 만들기를 수행하는 동안 하나 이상의 오류가 발생했습니다. 이 오류 메시지는 하나 이상의 오류가 발견되었음을 나타냅니다.  
  
### <a name="possible-causes"></a>가능한 원인  
 가능한 원인은 다음과 같습니다.  
  
-   보고서 서버에서 처리 오류가 발생했습니다.  
  
-   보고서를 미리 볼 때 로컬 보고서 처리 중에 처리 오류가 발생했습니다.  
  
-   그룹 식이 잘못된 데이터 형식으로 반환되었습니다.  
  
-   필터 정의에서 비교할 수 없는 데이터 형식으로 계산되는 두 식을 지정했습니다.  
  
-   식이 Fields 컬렉션에 존재하지 않는 필드를 참조했습니다.  
  
-   식에 범위가 잘못되었거나 충돌하는 집계 함수 호출이 있습니다.  
  
-   식이 보고서 매개 변수 컬렉션에 존재하지 않는 매개 변수를 참조했습니다.  
  
-   잘못 배포된 사용자 지정 어셈블리나 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 어셈블리를 로드하지 못했습니다.  
  
-   Nullable 속성이 **False** 로 설정된 매개 변수가 해당 매개 변수에서 Null 값을 검색했습니다.  
  
-   데이터 영역의 Hidden 속성에 대한 식에 다음 오류가 있습니다. 개체의 인스턴스에 개체 참조가 설정되지 않았습니다.  
  
-   식에 잘못된 함수 호출 또는 구문 오류가 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
  
### <a name="finding-more-information"></a>추가 정보 찾기  
 다음 동작 중 하나 이상을 수행합니다.  
  
-   보고서 서버의 보고서를 검토하거나 보고서를 구독으로 보고 있는 경우 오류 메시지의 전체 텍스트를 확인합니다. 추가 정보가 확장된 텍스트에서 제공됩니다.  
  
-   보고서 디자이너에서 보고서를 제작하는 중에 보고서를 미리 보거나 게시할 때 이 오류가 발생하는 경우 오류 목록 창에 추가 정보가 제공됩니다.  
  
-   보고서 디자이너 미리 보기에서 보고서를 제작하는 중인 경우 오류 메시지의 전체 텍스트를 확인합니다. 추가 정보가 확장된 텍스트에서 제공됩니다.  
  
-   보고서 서버에서 보고서를 보고 있으며 보고서 서버에서 로컬 관리자로 실행 중인 경우 페이지를 마우스 오른쪽 단추로 클릭하고 **소스 보기**를 선택하면 호출 스택을 볼 수 있습니다. 호출 스택에 세부 정보가 제공됩니다.  
  
-   보고서 서버의 로컬 관리자로 실행 중인 경우 로그 파일에서 `ReportProcessingException`을 검색합니다. 로그 항목에 자세한 정보가 있습니다. 보고서 서버 로그 파일은 일반적으로 \<*drive*>:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__*datetimestamp*.log에 있습니다. 자세한 내용은 [Reporting Services 로그 파일 및 소스](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)를 참조하세요.  
  
### <a name="failed-to-load-expression-host-assembly"></a>식 호스트 어셈블리 로드 실패  
 사용자 지정 어셈블리에는 강력한 이름 서명 및 AllowPartiallyTrustedCallers 특성 집합이 있어야 합니다. 자세한 내용은 [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md) 및 [Understanding Security Policies](../../reporting-services/extensions/secure-development/understanding-security-policies.md)를 참조하세요.  
  
### <a name="a-built-in-global-name-does-not-exist"></a>기본 제공 전역 이름이 없음  
 식의 철자를 확인하세요. 기본 제공 전역 변수, 매개 변수 이름 및 필드 이름은 대/소문자를 구분합니다. 오류를 일으킨 식에서 이름이 보고서에 실제로 있는지, 그리고 철자가 정확한지 확인하세요. 자세한 내용은 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)을 참조하세요.  
  
### <a name="parameter-properties-and-null"></a>Properties 매개 변수와 Null 매개 변수  
 다중값 매개 변수는 Null이 될 수 없습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  
  
### <a name="main-report-with-subreport-could-not-be-processed"></a>하위 보고서가 있는 주 보고서를 처리할 수 없음  
 하위 보고서가 있는 보고서는 동일한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 프로세서 버전으로 처리해야 합니다. 보고서를 현재 버전의 보고서 정의 스키마로 업그레이드할 때 주 보고서와 하위 보고서는 동시에 업데이트될 수도 있고 업데이트되지 않을 수도 있습니다. 보고서와 하위 보고서 간에 버전이 호환되지 않는 경우 "하위 보고서를 처리할 수 없습니다." 메시지가 나타납니다.  
  
 주 보고서 또는 하위 보고서 중 하나를 변경하여 동일한 보고서 프로세서 버전으로 두 보고서를 처리할 수 있도록 해야 합니다. 보고서 업그레이드가 실패하는 이유에 대한 자세한 내용은 [보고서 업그레이드](../../reporting-services/install-windows/upgrade-reports.md)를 참조하세요.  
  
### <a name="verify-function-calls-are-visual-basic-and-not-sql"></a>함수 호출이 Visual Basic이며 SQL이 아닌지 확인  
 관계형 데이터베이스에서는 쿼리 텍스트에 SQL 함수를 사용할 수 있지만 쿼리 텍스트에 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 함수를 사용할 수 없습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 식은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 함수, System.Math 또는 System.String 함수, 정규화된 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 함수를 사용할 수 있으며 사용자 지정 코드나 사용자 지정 어셈블리에 제공한 사용자 지정 함수를 사용할 수 있습니다. 식에서 SQL 함수는 사용할 수 없습니다.  
  
 쿼리와 식에서 만든 함수 호출이 유효한지 확인합니다.  
  
### <a name="cannot-compare-data-types-for-a-filter"></a>필터에 대한 데이터 형식을 비교할 수 없음  
 필터 수식에서 필터링 대상을 정의하는 필터 식과 필터 값은 데이터 형식이 같아야 비교할 수 있습니다. 다음 오류가 발생할 경우 데이터 형식이 일치하도록 필드 식 또는 필터 값을 수정하세요.  
  
-   *\<report item name>* 에 대한 *\<report item type>* 처리를 수행할 수 없습니다. 형식이 *\<type>* 인 데이터와 *\<type>* 인 데이터를 비교할 수 없습니다. *\<report item name>* 에서 반환되는 데이터 형식을 확인하세요.  
  
-   *\<property name>* 을 계산하지 못했습니다.  
  
-   *\<property name>* 을 계산하지 못했습니다. *\<error string>* 오류가 있는 데이터 집합 필드를 참조합니다.  
  
 자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="invalid-or-conflicting-scope-specification-in-an-aggregate-function-call"></a>집계 함수 호출에 잘못된 또는 충돌하는 범위 사양이 있음  
 테이블릭스 셀에 식에 대한 집계 함수 호출을 포함하면 보고서 프로세서는 셀이 속한 가장 안쪽 그룹의 범위에서 식을 계산합니다.  
  
 집계 함수에 특정 범위의 이름을 전달할 수도 있습니다. 범위는 데이터 영역, 데이터 집합의 이름 또는 데이터 계층에서 높은 범위의 이름을 참조할 수 있습니다. 다음과 같은 메시지가 이에 해당합니다.  
  
-   *\<report item type>* '*\<report item name>*'에 잘못된 범위 "*\<scope name>*"이 있습니다. 범위는 현재 범위이거나 현재 범위 내에 포함되어야 합니다.  
  
-   *\<report item type>* '*\<report item name>*'에 대한 *\<property name>* 식에 집계 함수에 유효하지 않은 범위 매개 변수가 있습니다. 범위 매개 변수는 포함 그룹의 이름, 포함 데이터 영역의 이름 또는 데이터 집합의 이름 중 하나와 동일한 문자열 상수로 설정되어야 합니다.  
  
 누계를 계산하는 집계 함수의 경우(**Previous**, **RunningValue**또는 **RowNumber**) 행 그룹 이름 또는 열 그룹 이름 중 하나인 범위 매개 변수를 지정할 수 있습니다. 다음과 같은 오류 메시지가 이에 해당합니다.  
  
-   *\<report item type>* '*\<report item name>*'의 데이터 셀에 사용된 **Previous**, **RunningValue** 또는 **RowNumber** 집계 함수가 *\<report item type>* 의 열과 행 모두에 있는 그룹화 범위를 참조합니다. *\<report item type>* 내의 모든 **Previous**, **RunningValue** 및 **RowNumber** 집계 함수의 범위 매개 변수는 행 그룹화나 데이터 열 그룹화 중 하나만 참조할 수 있습니다.  
  
 자세한 내용은 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) 및 [기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)을 참조하세요.  
  
### <a name="default-dataset-scope-for-a-top-level-text-box"></a>최상위 입력란에 대한 기본 데이터 집합 범위  
 보고서에 데이터 집합이 두 개 이상인 경우 보고서 디자인 화면에 추가된 입력란에 기본 범위를 사용하지 마세요. 범위로 데이터 집합의 이름을 포함하는 식과 집계 함수를 사용하세요. `=First(Fields!FieldName.Value, "DataSet2")`)을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [일반적으로 사용되는 필터&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조&#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
