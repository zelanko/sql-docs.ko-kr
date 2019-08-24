---
title: 보고서 서버 애플리케이션을 위한 사용 가능한 메모리 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- memory [Reporting Services]
- memory thresholds [Reporting Services]
ms.assetid: ac7ab037-300c-499d-89d4-756f8d8e99f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 80215f23b2544a442600a97112f3d0e2650f55e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103964"
---
# <a name="configure-available-memory-for-report-server-applications"></a>보고서 서버 애플리케이션을 위한 사용 가능한 메모리 구성
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 가 모든 사용 가능한 메모리를 사용할 수 있지만 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 서버 응용 프로그램에 할당되는 총 메모리 리소스 양에 대한 상한값을 구성하여 기본 동작을 재정의할 수 있습니다. 메모리 가중 정도가 낮은지, 보통인지, 높은지에 따라 보고서 서버가 요청의 우선 순위를 정하고 해당 요청을 처리하는 방법을 변경하도록 하는 임계값을 설정할 수도 있습니다. 메모리 가중 정도가 낮은 수준에서 보고서 서버는 대화형 또는 요청 시 실행 보고서 처리에 약간 더 높은 우선 순위를 부여하여 응답합니다. 메모리 가중 정도가 높은 수준에서 보고서 서버는 사용 가능한 제한된 리소스를 통해 여러 기술을 사용하여 작동 상태를 유지합니다.  
  
 이 항목에서는 메모리 가중 상태가 요청 처리의 요인이 될 때 지정할 수 있는 구성 설정과 서버의 응답 방식을 설명합니다.  
  
## <a name="memory-management-policies"></a>메모리 관리 정책  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 특정 응용 프로그램에 할당된 메모리 양과 처리 요청의 유형을 조정하여 시스템 리소스 제약 조건에 응답합니다. 보고서 서버 서비스에서 실행되고 메모리 관리의 대상이 되는 애플리케이션은 다음과 같습니다.  
  
-   보고서 관리자 - 보고서 서버용 웹 프런트 엔드 애플리케이션입니다.  
  
-   보고서 서버 웹 서비스 - 대화형 보고서 처리 및 요청 시 실행 요청에 사용됩니다.  
  
-   백그라운드 처리 애플리케이션 - 예약된 보고서 처리, 구독 배달 및 데이터베이스 유지 관리에 사용됩니다.  
  
 메모리 관리 정책은 프로세스 내에서 실행되는 개별 애플리케이션이 아닌 보고서 서버 서비스 전체에 적용됩니다.  
  
 시스템에 메모리 가중 상태가 없는 경우 각 서버 애플리케이션은 실제로 요청을 받을 때 최적의 성능을 제공할 수 있도록 요청을 받기 전에 시작 시 약간의 메모리를 요청합니다. 메모리 가중 정도가 심해지면 보고서 서버가 다음 표에 설명된 대로 해당 프로세스 모델을 조정합니다.  
  
|메모리 가중|서버 응답|  
|---------------------|---------------------|  
|낮음|현재 요청이 계속 처리됩니다. 새 요청은 대부분 받아들여집니다. 백그라운드 처리 애플리케이션으로 전송된 요청에는 보고서 서버 웹 서비스로 전송된 요청보다 낮은 우선 순위가 부여됩니다.|  
|보통|현재 요청이 계속 처리됩니다. 새 요청은 받아들여질 수 있습니다. 백그라운드 처리 애플리케이션으로 전송된 요청에는 보고서 서버 웹 서비스로 전송된 요청보다 낮은 우선 순위가 부여됩니다. 웹 서비스 요청에 더 많은 메모리를 사용할 수 있도록 백그라운드 처리의 메모리를 상대적으로 더 많이 줄여 세 개의 서버 애플리케이션 모두에 대한 메모리 할당이 줄어듭니다.|  
|높음|메모리 할당이 더 줄어듭니다. 더 많은 메모리를 요청하는 서버 애플리케이션은 거부됩니다. 현재 요청은 느려져 완료되는 데 더 많은 시간이 소요됩니다. 새 요청은 받아들여지지 않습니다. 보고서 서버가 메모리 내 데이터 파일을 디스크로 스왑합니다.<br /><br /> 메모리 제약 조건이 심해지고 새 요청을 처리하는 데 사용할 수 있는 메모리가 없는 경우 보고서 서버는 현재 요청이 완료되는 동안 HTTP 503 서버 사용할 수 없음 오류를 반환합니다. 경우에 따라 메모리 가중 정도를 즉시 낮추기 위해 애플리케이션 도메인이 재활용될 수 있습니다.|  
  
 다양한 메모리 가중 시나리오에 대한 보고서 서버 응답을 사용자 지정할 수는 없지만 메모리 가중 응답을 높음, 보통, 낮음으로 구분하는 경계를 정의하는 구성 설정을 지정할 수 있습니다.  
  
## <a name="when-to-customize-memory-management-settings"></a>메모리 관리 설정을 사용자 지정해야 하는 경우  
 기본 설정은 낮은 메모리 가중, 보통 메모리 가중 및 높은 메모리 가중에 대해 서로 다른 범위를 지정합니다. 기본적으로 낮은 메모리 가중 영역은 보통 및 높은 메모리 가중 영역에 비해 더 큽니다. 이 구성은 고르게 분산되어 있거나 증분식으로 증가/감소하는 처리 부하에 가장 적합합니다. 이 시나리오에서 영역은 점진적으로 전환되므로 보고서 서버에 응답을 조정할 시간이 제공됩니다.  
  
 부하 패턴이 급격하게 변동되는 경우 기본 설정을 수정하면 유용합니다. 처리 부하가 급격하게 변동되는 경우 보고서 서버는 메모리 가중 없음 상태에서 메모리 할당 실패 상태로 매우 빠르게 이동할 수 있습니다. 이러한 상황은 동시에 시작하며 메모리를 많이 사용하는 보고서의 동시 인스턴스가 여러 개인 경우 발생할 수 있습니다. 이러한 처리 부하 유형을 처리하기 위해서는 처리가 느려질 수 있도록 가능한 한 빨리 보고서 서버를 보통 또는 높은 메모리 가중 응답으로 이동해야 합니다. 이렇게 하면 더 많은 요청이 완료될 수 있습니다. 이렇게 하려면 낮은 메모리 가중 영역이 다른 영역에 비해 상대적으로 더 작아지도록 `MemorySafetyMargin`의 값을 줄여야 합니다. 그러면 보통 및 높은 메모리 가중에 대한 응답이 더 일찍 발생하게 됩니다.  
  
## <a name="configuration-settings-for-memory-management"></a>메모리 관리에 대한 구성 설정  
 보고서 서버에 대한 메모리 할당을 제어하는 구성 설정에는 `WorkingSetMaximum`, `WorkingSetMinimum`, `MemorySafetyMargin` 및 `MemoryThreshold`가 포함됩니다.  
  
-   `WorkingSetMaximum` 및 `WorkingSetMinimum`은 사용 가능한 메모리의 범위를 정의합니다. 이러한 설정을 구성하여 보고서 서버 애플리케이션에 대해 사용 가능한 메모리의 범위를 설정할 수 있습니다. 이는 같은 컴퓨터에서 여러 애플리케이션을 호스팅하며 보고서 서버가 같은 컴퓨터에 있는 다른 애플리케이션에 비해 상대적으로 시스템 리소스를 과다하게 사용하고 있다고 판단되는 경우 유용할 수 있습니다.  
  
-   `MemorySafetyMargin` 및 `MemoryThreshold`는 메모리 가중의 낮음, 보통 및 높음 수준에 대한 경계를 설정합니다. 각 상태에 대해 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 는 보고서 처리 및 기타 요청이 컴퓨터에서 사용할 수 있는 메모리 양에 상대적으로 적절하게 처리되도록 수정 동작을 수행합니다. 낮음, 높음 및 보통 가중 수준 간 경계를 지정하는 구성 설정을 지정할 수 있습니다.  
  
     구성 설정을 변경할 수 있지만 이렇게 해도 보고서 처리 성능은 향상되지 않습니다. 요청이 완료되기 전에 삭제되는 경우에만 구성 설정을 변경하는 것이 유용합니다. 서버 성능을 향상시키는 가장 좋은 방법은 전용 컴퓨터에 보고서 서버 또는 개별 보고서 서버 애플리케이션을 배포하는 것입니다.  
  
 다음 그림에서는 낮음, 보통 및 높음 수준의 메모리 가중 상태를 구분하기 위해 설정을 함께 사용하는 방법을 보여 줍니다.  
  
 ![메모리 상태에 대한 구성 설정](../media/rs-memoryconfigurationzones.gif "메모리 상태에 대한 구성 설정")  
  
 다음 표에서는 `WorkingSetMaximum`, `WorkingSetMinimum`, `MemorySafetyMargin` 및 `MemoryThreshold` 설정을 설명합니다. 구성 설정은 [RSReportServer 구성 파일](rsreportserver-config-configuration-file.md)에 지정되어 있습니다.  
  
|요소|Description|  
|-------------|-----------------|  
|`WorkingSetMaximum`|값 초과 시 보고서 서버 애플리케이션에 대한 새 메모리 할당 요청이 더 이상 허가되지 않는 메모리 임계값을 지정합니다.<br /><br /> 기본적으로 보고서 서버는 `WorkingSetMaximum`을 컴퓨터에서 사용 가능한 메모리 양으로 설정합니다. 이 값은 서비스가 시작될 때 검색됩니다.<br /><br /> 이 설정을 직접 추가하지 않으면 RSReportServer.config 파일에 나타나지 않습니다. 보고서 서버가 메모리를 더 적게 사용하도록 하려면 RSReportServer.config 파일을 수정하고 요소와 값을 추가합니다. 유효한 값은 0에서 최대 정수 사이입니다. 이 값은 KB로 표시됩니다.<br /><br /> `WorkingSetMaximum`의 값에 도달하면 보고서 서버가 새 요청을 받아들이지 않습니다. 현재 진행 중인 요청은 완료되도록 허용됩니다. 새 요청은 메모리 사용이 `WorkingSetMaximum`을 통해 지정된 값 아래로 떨어질 때만 받아들여집니다.<br /><br /> `WorkingSetMaximum` 값에 도달한 후에도 기존 요청이 추가 메모리를 계속 사용하는 경우 모든 보고서 서버 애플리케이션 도메인이 재활용됩니다. 자세한 내용은 [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md)을 참조하세요.|  
|`WorkingSetMinimum`|리소스 소비량에 대한 하한값을 지정합니다. 보고서 서버는 전체 메모리 사용이 이 값 미만인 경우 메모리를 해제하지 않습니다.<br /><br /> 기본적으로 이 값은 서비스 시작 시 계산됩니다. 계산 시 초기 메모리 할당 요청은 `WorkingSetMaximum`의 60%입니다.<br /><br /> 이 설정을 직접 추가하지 않으면 RSReportServer.config 파일에 나타나지 않습니다. 이 값을 사용자 지정하려는 경우 RSReportServer.config 파일에 `WorkingSetMinimum` 요소를 추가해야 합니다. 유효한 값은 0에서 최대 정수 사이입니다. 이 값은 KB로 표시됩니다.|  
|`MemoryThreshold`|높음 및 보통 가중 시나리오 간 경계를 정의하는 `WorkingSetMaximum`의 비율을 지정합니다. 보고서 서버 메모리 사용이 이 값에 도달하는 경우 보고서 서버는 요청 처리 속도를 낮추고 다른 서버 애플리케이션에 할당된 메모리 양을 변경합니다. 기본값은 90입니다. 이 값은 `MemorySafetyMargin`에 설정된 값보다 커야 합니다.|  
|`MemorySafetyMargin`|보통 및 낮음 가중 시나리오 간 경계를 정의하는 `WorkingSetMaximum`의 비율을 지정합니다. 이 값은 시스템용으로 예약된 사용 가능한 메모리 비율이며 보고서 서버 작업에 사용할 수 없습니다. 기본값은 80입니다.|  
  
> [!NOTE]  
>  `MemoryLimit` 및 `MaximumMemoryLimit` 설정은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 및 이후 버전에서 사용되지 않습니다. 기존 설치를 업그레이드했거나 해당 설정을 포함하는 RSReportServer.config 파일을 사용하는 경우 보고서 서버는 해당 값을 더 이상 읽지 않습니다.  
  
#### <a name="example-of-memory-configuration-settings"></a>메모리 구성 설정 예  
 다음 예에서는 사용자 지정 메모리 구성 값을 사용하는 보고서 서버 컴퓨터에 대한 구성 설정을 보여 줍니다. `WorkingSetMaximum` 또는 `WorkingSetMinimum`을 추가하려는 경우 RSReportServer.config 파일에 요소와 값을 입력해야 합니다. 두 값 모두 서버 애플리케이션에 할당하는 RAM을 KB로 표시하는 정수입니다. 다음 예에서는 보고서 서버 애플리케이션에 대한 총 메모리 할당이 4GB를 초과할 수 없음을 지정합니다. `WorkingSetMinimum`의 기본값(`WorkingSetMaximum`의 60%)이 허용 가능한 수준인 경우 RSReportServer.config 파일에서 이 값을 생략하고 `WorkingSetMaximum`만 지정할 수 있습니다. 이 예에서는 추가하는 경우 해당 값이 나타나는 방법을 보여 주기 위해 `WorkingSetMinimum`을 포함합니다.  
  
```  
      <MemorySafetyMargin>80</MemorySafetyMargin>  
      <MemoryThreshold>90</MemoryThreshold>  
      <WorkingSetMaximum>4000000</WorkingSetMaximum>  
      <WorkingSetMinimum>2400000</WorkingSetMinimum>  
```  
  
#### <a name="about-aspnet-memory-configuration-settings"></a>ASP.NET 메모리 구성 설정 정보  
 보고서 서버 웹 서비스와 보고서 관리자는 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 애플리케이션이지만 이 중 어떤 애플리케이션도 IIS 5.0 호환성 모드에서 실행되는 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 애플리케이션에 대한 machine.config의 `processModel` 섹션에 지정하는 메모리 구성 설정에 응답하지 않습니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 는 RSReportServer.config 파일에서만 메모리 구성 설정을 읽습니다.  
  
## <a name="see-also"></a>관련 항목  
 [RSReportServer 구성 파일](rsreportserver-config-configuration-file.md)   
 [RSReportServer 구성 파일](rsreportserver-config-configuration-file.md)   
 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [보고서 서버 응용 프로그램을 위한 응용 프로그램 도메인](application-domains-for-report-server-applications.md)  
  
  
