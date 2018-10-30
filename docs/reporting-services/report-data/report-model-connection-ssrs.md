---
title: 보고서 모델 연결(SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: da880fb8-13cc-4d5f-b992-91ed0ec3ca7d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0f948086d974be8eaf03b048d36327bfed0de215
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50029272"
---
# <a name="report-model-connection-ssrs"></a>보고서 모델 연결(SSRS)
  보고서 모델의 데이터를 포함하려면 데이터 원본으로 보고서 모델을 기반으로 하는 데이터 집합이 있어야 합니다. 다른 보고서 데이터 원본과는 달리 보고서 모델용 데이터 확장 프로그램은 없습니다. 보고서 작성기에서는 보고서 서버에서 모델을 찾아 직접 선택하면 됩니다. 보고서 디자이너에서는 보고서 모델 URL을 지정합니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Connection"></a> 연결 문자열  
 보고서 모델을 데이터 원본으로 사용하는 데 연결 문자열은 필요하지 않습니다. 보고서 모델에 연결하려면 보고서 서버 또는 SharePoint 사이트로 이동하고 게시된 모델을 선택합니다. SharePoint 사이트에서 보고서 모델 파일 이름의 확장명은 .smdl입니다.  
  
 연결 문자열 예제는 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)을 참조하세요.  
  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 자세한 내용은 [보고서 작성기에 자격 증명 지정](https://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)을 참조하세요.  
  
  
##  <a name="Query"></a> 쿼리  
 보고서 모델 쿼리 디자이너를 사용하여 대화형으로 엔터티와 필드 및 쿼리에 대한 필터를 지정할 수 있습니다. 모델의 엔터티와 필드는 보고서 데이터 창에 표시되는 데이터 집합 필드 컬렉션이 됩니다.  
  
  
##  <a name="Parameters"></a> 매개 변수  
 보고서 매개 변수를 추가하려면 보고서 모델 쿼리 디자이너에서 프롬프트를 사용하여 필터를 만듭니다.  
  
 보고서 매개 변수는 수정해야 할 수도 있는 기본 속성 값을 사용하여 만들어집니다. 기본적으로 각 보고서 매개 변수의 데이터 형식은 **Text**입니다. 기본 데이터의 데이터 형식이 다르면 매개 변수 데이터 형식을 변경해야 합니다.  
  
 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  
  
  
##  <a name="Remarks"></a> 주의  
 이 데이터 공급자는 일부 보고서 배달 모드만 지원합니다. 이 데이터 처리 확장 프로그램에서는 데이터 기반 구독을 통한 보고서 배달이 지원되지 않습니다. 자세한 내용은 [구독자 데이터에 외부 데이터 원본 사용&#40;데이터 기반 구독&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)을 참조하세요.  
  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 집합을 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 집합에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 집합 및 공유 데이터 집합에 대한 정보를 제공합니다.  
  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 쿼리에 의해 생성되는 데이터 집합 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](https://go.microsoft.com/fwlink/?linkid=121312)에 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서의 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
