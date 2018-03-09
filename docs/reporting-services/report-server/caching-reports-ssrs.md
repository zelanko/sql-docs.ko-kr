---
title: "보고서 캐시(SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- report processing [Reporting Services], caching
- cached instances [Reporting Services]
- refreshing cache
- cached reports [Reporting Services]
- preloading cache
- invalid cached reports [Reporting Services]
- performance [Reporting Services]
- expiration [Reporting Services]
- snapshots [Reporting Services], caching
ms.assetid: 146542c3-8efd-4b89-a8d8-77d22896630e
caps.latest.revision: "44"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: be5dfff54e54b9e5fd768f3b438f9e378bf34c9a
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="caching-reports-ssrs"></a>보고서 캐시(SSRS)
  보고서 서버는 처리된 보고서의 복사본을 캐시했다가 사용자가 보고서를 열면 해당 복사본을 반환할 수 있습니다. 사용자는 보고서가 실행된 날짜와 시간을 통해서만 보고서가 캐시된 복사본인지 여부를 알 수 있습니다. 보고서의 날짜 또는 시간이 현재가 아니고 보고서가 스냅숏이 아니라면 캐시에서 가져온 보고서입니다.  
  
 캐싱은 보고서가 크거나 자주 액세스되는 경우 보고서를 검색하는 데 필요한 시간을 단축시킬 수 있습니다. 서버를 다시 부팅한 경우 보고서 서버 웹 서비스가 온라인 상태로 돌아오면 캐시된 모든 인스턴스가 복원됩니다.  
  
 캐싱은 성능을 향상시키는 기술입니다. 캐시의 내용은 휘발성이며 보고서가 추가, 대체 또는 제거되면 그에 따라 변경될 수 있습니다. 좀 더 예측 가능한 캐싱을 위해서는 보고서 스냅숏을 만들어야 합니다. 자세한 내용은 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 사용자 세션 및 보고서 처리를 지원하기 위해 데이터베이스에 임시 파일을 저장합니다. 이러한 파일은 단일 브라우저 세션 중에 일관된 뷰를 제공하며 내부용으로 사용하기 위해 캐시됩니다. 내부용 임시 파일을 캐시하는 방법에 대한 자세한 내용은 [보고서 서버 데이터베이스&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)를 참조하세요.  
  
## <a name="cached-instances"></a>캐시된 인스턴스  
 보고서의 캐시된 인스턴스는 보고서의 중간 형식을 기반으로 합니다. 보고서 서버는 일반적으로 보고서 이름에 따라 하나의 보고서 인스턴스를 캐시합니다. 그러나 보고서에 쿼리 매개 변수를 기반으로 하는 다른 데이터가 포함될 수 있는 경우 여러 버전의 보고서가 캐시됩니다. 예를 들어 지역 번호를 매개 변수 값으로 사용하는 매개 변수가 있는 보고서가 있다고 가정해 봅시다. 4명의 사용자가 고유한 지역 번호 4개를 지정하면 캐시된 복사본 4개가 만들어집니다.  
  
 고유한 지역 번호가 있는 보고서를 실행하는 첫 번째 사용자는 해당 지역에 대한 데이터를 포함하는 캐시된 보고서를 만듭니다. 같은 지역 번호를 사용하는 보고서를 요청하는 다음 사용자는 캐시된 복사본을 얻습니다.  
  
 모든 보고서가 캐시되는 것은 아닙니다. 보고서가 사용자 종속 데이터를 포함하거나 사용자에게 자격 증명을 요청하거나 Windows 인증을 사용하면 캐시될 수 없습니다.  
  
## <a name="refreshing-the-cache"></a>캐시 새로 고침  
 이전에 캐시된 복사본이 만료된 이후에 사용자가 해당 보고서를 선택하면 캐시된 보고서가 최신 버전으로 대체됩니다. 캐시된 인스턴스로 실행되도록 구성된 보고서는 만료 설정에 따라 정기적인 간격으로 캐시에서 제거됩니다. 데이터의 즉시 필요 여부에 따라 보고서 만료를 분 단위로 설정하거나 예약된 시간에 보고서가 만료되도록 설정할 수 있습니다. SOAP API를 사용하지 않는 한 캐시에서 직접 보고서를 삭제할 수 없습니다.  
  
 캐시 만료를 구성하려면 공유 일정이나 보고서별 일정을 사용할 수 있습니다. 공유 일정을 사용하다가 이후에 일시 중지된 경우 일정이 작동하지 않는 동안에는 캐시가 만료되지 않습니다. 이후에 공유 일정을 삭제하면 일정 설정 복사본이 보고서별 일정으로 저장됩니다.  
  
 일정이 만료되거나 캐시 만료 날짜에 일정 예약 엔진을 사용할 수 없는 경우 보고서 서버는 일정을 확장하거나 일정 서비스를 시작하여 예약된 작업이 다시 시작될 때까지 실제 보고서를 실행합니다.  
  
## <a name="preloading-the-cache"></a>캐시 미리 로드  
 서버 성능을 향상시키기 위해 캐시를 미리 로드할 수 있습니다. 다음과 같은 두 가지 방법으로 매개 변수가 있는 보고서 인스턴스의 모음과 함께 캐시를 미리 로드할 수 있습니다.  
  
1.  캐시 새로 고침 계획을 만듭니다. 새로 고침 계획을 만들 경우 단일 보고서에 대한 일정을 지정하거나 공유 일정을 지정할 수 있습니다.  
  
2.  Null 배달 공급자를 사용하는 데이터 기반 구독을 만듭니다. 구독에서 Null 배달 공급자를 배달 방법으로 지정하면 보고서 서버는 보고서 서버 데이터베이스를 배달 대상으로 지정하고 Null 렌더링 확장 프로그램이라고 하는 특수한 렌더링 확장 프로그램을 사용합니다. 다른 배달 확장 프로그램과는 달리 Null 배달 공급자에는 구독 정의를 통해 구성할 수 있는 배달 설정이 없습니다.  
  
 보고서를 캐시하는 기능은 매개 변수가 있는 여러 보고서 인스턴스를 캐시할 때 특히 유용하며, 다양한 매개 변수 값을 사용하여 서로 다른 보고서 인스턴스가 생성됩니다. 보고서에는 쿼리 기반 매개 변수만 지정할 수 있습니다.  
  
 일정을 지정하거나 데이터 기반 구독을 만들 때는 보고서를 캐시로 배달하는 빈도를 예약해야 합니다. 새 복사본을 캐시로 배달하려면 이전 복사본이 만료되어야 합니다. 따라서 캐시 만료 설정을 포함하도록 보고서의 실행 속성을 구성해야 합니다. 만료 설정은 사용자가 정의한 구독 일정과 일치해야 합니다. 예를 들어 매일 밤에 실행되는 구독을 만드는 경우 캐시는 매일 밤 구독 실행 시간 전에 만료되어야 합니다. 실행 속성에 만료 시간이 포함되지 않으면 새 배달은 무시됩니다. 캐시 새로 고침 계획에 대한 자세한 내용은 [일정](../../reporting-services/subscriptions/schedules.md)을 참조하세요. 속성을 설정하는 방법에 대한 자세한 내용은 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)을 참조하세요. 데이터 기반 구독을 사용하는 방법에 대한 자세한 내용은 [데이터 기반 구독](../../reporting-services/subscriptions/data-driven-subscriptions.md)을 참조하세요.  
  
## <a name="conditions-that-cause-cache-expiration"></a>캐시 만료 조건  
 캐시된 보고서는 보고서 정의가 수정되거나 보고서 매개 변수가 수정되거나 데이터 원본 자격 증명이 변경되거나 보고서 실행 옵션이 변경될 때 무효화됩니다. 캐시에 저장된 보고서가 삭제되면 캐시된 버전도 삭제됩니다.  
  
 사용자가 지정한 매개 변수 값이 캐시된 보고서를 만드는 데 사용된 값과 다른 경우 등 어떤 이유에서든 캐시된 인스턴스에서 보고서를 렌더링할 수 없으면 보고서 서버에서 보고서를 다시 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Reporting Services 개념&#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [캐시 사전 로드&#40;보고서 관리자&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md)   
 [일정](../../reporting-services/subscriptions/schedules.md)   
 [공유 데이터 집합 캐시&#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)   
 [캐시 새로 고침 옵션&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6)  
  
  
