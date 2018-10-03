---
title: 보고서 및 구독 처리 일시 중지 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4c15666aecbbdde8ca95eaf684bf9909454d3d42
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129314"
---
# <a name="pause-report-and-subscription-processing"></a>보고서 및 구독 처리 일시 중지
  보고서나 구독을 직접 일시 중지할 수 없습니다. 그러나 프로세스가 시작되거나 데이터 원본 연결이 만들어지기 전에 보고서 및 구독 처리를 중단할 수 있습니다. 사용자가 보고서나 구독에 액세스하지 못하도록 하여 보고서나 구독 처리를 중단할 수도 있습니다.  
  
 다음 방법으로 프로세스를 일시적으로 중단할 수 있습니다.  
  
## <a name="modify-role-assignments-to-prevent-access"></a>역할 할당을 수정하여 액세스 금지  
 보고서를 사용할 수 없도록 하는 최선의 방법은 보고서에 액세스할 수 있는 권한을 제공하는 역할 할당을 일시적으로 제거하는 것입니다. 이 방법은 데이터 원본 연결이 생성되는 방법에 관계없이 모든 보고서에 사용될 수 있습니다. 이 방법은 다른 보고서나 항목의 작업에 영향을 주지 않고 해당 보고서에만 영향을 줍니다.  
  
 역할 할당을 제거하려면 보고서 관리자에서 보고서의 보안 속성 페이지를 여십시오. 보고서가 부모 보고서에서 보안 설정을 상속받은 경우 **항목 보안 편집** 을 클릭하여 광범위한 액세스를 제공하는 역할 할당은 포함하지 않는 제한적인 보안 정책을 만들 수 있습니다. 예를 들어 Everyone에게 액세스를 제공하는 역할 할당은 제거하고 Administrators와 같은 일부 사용자에게만 액세스를 제공하는 역할 할당은 유지할 수 있습니다.  
  
## <a name="disable-a-shared-data-source"></a>공유 데이터 원본 해제  
 공유 데이터 원본 사용 시 이점은 보고서나 데이터 기반 구독이 실행되지 않도록 공유 데이터 원본을 해제할 수 있다는 점입니다. 공유 데이터 원본을 해제하면 보고서와 외부 원본의 연결이 끊어집니다. 해제되어 있는 동안에는 데이터 원본을 사용하는 모든 보고서와 구독에서 해당 데이터 원본을 사용할 수 없습니다. 공유 데이터 원본을 해제하려면 보고서 관리자에서 데이터 원본을 열고 **이 데이터 원본 사용** 확인란의 선택을 취소합니다.  
  
 데이터 원본을 사용할 수 없는 경우에도 보고서는 로드됩니다. 보고서에는 데이터가 포함되지 않지만 적절한 권한이 있는 사용자는 보고서에 연결된 속성 페이지, 보안 설정, 보고서 기록 및 구독 정보에 액세스할 수 있습니다.  
  
## <a name="pause-a-shared-schedule"></a>공유 일정 일시 중지  
 보고서나 구독을 공유 일정에 따라 실행하는 경우 일정을 일시 중지하여 처리를 중단할 수 있습니다. 일정에 따라 진행되는 모든 보고서와 구독 처리는 일정을 다시 시작할 때까지 중단됩니다. 자세한 내용은 [일시 중지 및 다시 시작 공유 일정](schedules.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)   
 [보안 속성 페이지, 항목&#40;보고서 관리자&#41;](../security-properties-page-items-report-manager.md)  
  
  
