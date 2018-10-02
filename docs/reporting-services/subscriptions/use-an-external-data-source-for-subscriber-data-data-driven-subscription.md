---
title: 구독자 데이터에 외부 데이터 원본 사용(데이터 기반 구독) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriber data sources [Reporting Services]
- subscriptions [Reporting Services], external data sources
- query-based subscriptions [Reporting Services]
- external data sources [Reporting Services]
- data-driven subscriptions
- data sources [Reporting Services], subscriptions
ms.assetid: 1cade8ec-729c-4df8-a428-e75c9ad86369
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 98c58da0ba018bc65d8459350f3f8e664587cdc9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657831"
---
# <a name="use-an-external-data-source-for-subscriber-data-data-driven-subscription"></a>구독자 데이터에 외부 데이터 원본 사용(데이터 기반 구독)
  데이터 기반 구독에서는 외부 데이터 원본에서 데이터를 검색하는 쿼리 또는 명령에 의해 동적 구독 데이터가 제공됩니다. 데이터 기반 구독 처리 요구 사항을 만족하는 지원되는 모든 데이터 원본에서 구독 데이터를 검색할 수 있습니다. 쿼리 또는 명령 구문은 보고서 서버와 함께 설치되는 데이터 처리 확장 프로그램에 유효해야 합니다.  
  
## <a name="data-processing-requirements"></a>데이터 처리 요구 사항  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 데이터 처리 확장 프로그램을 사용하여 구독 데이터를 검색합니다. 권장되는 데이터 원본 유형은 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스  
  
-   Oracle 데이터베이스  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다차원 및 데이터 마이닝 데이터 원본  
  
-   XML 데이터 원본  
  
     구독자 데이터에 XML 데이터 처리 확장 프로그램을 사용할 때는 구독에서 쿼리 제한 시간 설정을 늘려야 합니다. XML 데이터 처리 확장 프로그램은 쿼리 제한 시간 값에 초가 아닌 밀리초를 사용합니다. 제한 시간 값을 늘리지 않으면 처리 시간 부족으로 인해 구독이 실패할 수 있습니다.  
  
     구독자 데이터 원본에 대한 연결을 구성할 때 **자격 증명 필요 없음** 옵션을 사용하지 마십시오. XML 데이터 처리 확장 프로그램을 사용하여 런타임에 구독 데이터를 검색하는 경우에는 저장된 자격 증명을 사용하는 것이 좋습니다.  
  
 지원되는 다른 데이터 원본 유형을 사용할 수 있지만 이 중 일부는 작동하지 않을 수 있습니다. 예를 들어 다음 데이터 원본 유형은 구독자 데이터에 사용할 수 없습니다.  
  
-   SAP Netweaver BI 데이터베이스  
  
-   보고서 모델  
  
 데이터 기반 구독에 사용할 사용자 지정 데이터 처리 확장 프로그램이 있을 경우 해당 프로그램에서는 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> 및 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 인터페이스를 구현해야 합니다. 데이터 처리 확장 프로그램에서는 스키마 전용 쿼리 실행을 지원해야 합니다. 이 쿼리는 사용자가 열을 구독 정의에 있는 배달 옵션 및 보고서 매개 변수에 매핑할 수 있도록 디자인 타임에 열 메타데이터를 검색하는 데 사용됩니다. 사용자가 구독을 정의할 때는 초기 단계에서 스키마 전용 쿼리가 실행됩니다.  
  
## <a name="query-requirements"></a>쿼리 요구 사항  
 구독 데이터를 검색하는 쿼리를 만들 때 다음 사항을 유의하십시오.  
  
-   구독에 대해 하나의 쿼리만 만들 수 있습니다.  
  
-   쿼리에서 배달 옵션 및 보고서 매개 변수 지정에 사용할 값을 모두 반환해야 합니다.  
  
-   보고서 서버에서는 결과 집합의 모든 행에 대한 보고서 배달을 만듭니다. 결과 집합이 300개의 행으로 구성된 경우에는 보고서 서버에서 300개의 보고서 배달을 시도합니다.  
  
## <a name="setting-delivery-options-using-variable-data-from-a-subscriber-database"></a>구독자 데이터베이스에서 변수 데이터를 사용하여 배달 옵션 설정  
 구독자 데이터베이스에 있는 데이터를 사용하여 각 받는 사람에 대한 배달 옵션을 사용자 지정할 수 있습니다. 사용하는 배달 확장 프로그램 종류에 따라 사용 가능한 옵션이 결정됩니다. 보고서 서버 전자 메일 배달 확장 프로그램을 사용하는 경우 쿼리에는 각 구독자에 대한 전자 메일 별칭이 포함되어야 합니다. 파일 공유 배달을 사용하고 있는 경우 구독자 데이터에는 구독자별 보고서 파일을 만들거나 배달 대상을 제공하는 데 사용할 수 있는 값이 포함되어야 합니다. 자세한 내용은 [Reporting Services의 전자 메일 배달](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)을 참조하세요.  
  
## <a name="passing-parameter-values-from-the-subscriber-database-to-the-report"></a>구독자 데이터베이스에서 보고서로 매개 변수 값 전달  
 매개 변수가 있는 보고서에 대해 데이터 기반 구독을 만드는 경우 변수 매개 변수 값을 사용하여 각 보고서의 출력을 사용자 지정할 수 있습니다. 예를 들어 구독자 데이터베이스에는 보고서 데이터를 필터링하는 데 사용할 수 있는 직원 ID 번호, 채용일, 직함, 사무실 위치 정보 등이 포함될 수 있습니다. 보고서에서 이러한 열 데이터나 기타 사용 가능한 열 데이터를 기반으로 하는 매개 변수를 사용하면 매개 변수를 해당 열로 매핑할 수 있습니다.  
  
 구독자 필드를 보고서 매개 변수에 매핑할 때 데이터 형식과 열 길이는 호환 가능해야 합니다. 데이터 형식이 일치하지 않으면 구독을 처리하는 동안 오류가 발생합니다. 매개 변수가 있는 보고서에서 구독자 데이터를 사용하는 방법에 대한 자세한 내용은 [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)를 참조하세요.  
  
## <a name="modifying-the-subscriber-data-source"></a>구독자 데이터 원본 수정  
 구독자 데이터 원본을 다음과 같이 수정하면 구독이 실행되지 않을 수 있습니다.  
  
-   구독에 참조된 열 제거  
  
-   데이터 원본의 테이블 구조 수정  
  
-   데이터 형식 및 기타 열 속성 변경  
  
 이렇게 변경하는 경우에는 구독을 업데이트해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 기반 구독 만들기, 수정 및 삭제](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [데이터 기반 구독](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  
