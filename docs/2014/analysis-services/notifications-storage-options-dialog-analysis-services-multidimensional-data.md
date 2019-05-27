---
title: 알림 (Storage Options Dialog Box) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.notifications.f1
ms.assetid: 5675cdbf-bfaa-4b6e-b716-31b8e9da72b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23845118c4c202db781fe325c4afc2402ceee271
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072198"
---
# <a name="notifications-storage-options-dialog-box-analysis-services---multidimensional-data"></a>알림(스토리지 옵션 대화 상자)(Analysis Services - 다차원 데이터)
  **에서** 저장소 옵션 **대화 상자의** 알림 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 탭을 사용하여 차원, 큐브, 측정값 그룹 또는 파티션에 대한 알림 방법 및 관련 설정을 설정할 수 있습니다.  
  
> [!NOTE]  
>  이러한 설정을 수정하려면 스토리지 모드와 자동 관리 캐싱 기능에 대해 잘 알고 있어야 합니다. 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.  
  
## <a name="options"></a>변수  
  
|용어|정의|  
|----------|----------------|  
|**저장소 모드**|개체에 사용할 스토리지 모드를 선택합니다.<br /><br /> **MOLAP**<br /> 개체가 MOLAP(다차원 OLAP) 스토리지를 사용합니다.<br /><br /> **HOLAP**<br /> 개체가 HOLAP(하이브리드 OLAP) 스토리지를 사용합니다.<br /><br /> **ROLAP**<br /> 개체가 ROLAP(관계형 OLAP) 스토리지를 사용합니다.|  
|**자동 관리 캐싱 설정**|자동 관리 캐싱을 설정합니다.<br /><br /> 참고: 이 옵션을 선택 하지 않으면 모든 옵션을 제외한 **저장소 모드** 비활성화 됩니다.|  
|**SQL Server**|[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 위해 특별히 제공되는 추적 메커니즘을 사용하여 개체의 기본 테이블에 대한 변경 내용을 식별합니다.|  
|**추적 테이블 지정**|개체에 대해 추적할 기본 테이블을 지정한 다음 세미콜론(;)으로 구분된 테이블 목록을 입력하거나 줄임표 단추(**...**)를 클릭하여 **관계형 개체** 대화 상자를 열고 추적할 테이블을 선택합니다. 자세한 내용은 [관계형 개체 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.<br /><br /> 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 특정 요구 사항이 만족되면 개체에 대해 추적할 기본 테이블 목록 확인을 시도합니다. 이러한 요구 사항에 대한 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.|  
|**클라이언트 시작**|XMLA(XML for Analysis) 명령 `NotifyTableChange`를 사용하여 개체에 대한 기본 테이블의 변경 내용을 식별합니다. 일반적으로 이 옵션은 클라이언트 기반 알림 프로세스를 사용할 경우 선택됩니다.|  
|**추적 테이블 지정**|선택하여 개체에 대해 추적할 기본 테이블을 지정한 다음 세미콜론(;)으로 구분된 테이블 목록을 입력하거나 줄임표 단추(**...**)를 클릭하여 **관계형 개체** 대화 상자를 열고 추적할 테이블을 선택합니다. 자세한 내용은 [관계형 개체 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.<br /><br /> 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 특정 요구 사항이 만족되면 개체에 대해 추적할 기본 테이블 목록 확인을 시도합니다. 이러한 요구 사항에 대한 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.|  
|**예약 된 폴링**|폴링 메커니즘을 통해 개체에 대한 기본 테이블에 대해 일련의 쿼리를 실행하여 변경 내용을 식별합니다.|  
|**폴링 간격**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 가 폴링 표에 정의된 폴링 쿼리 및 처리 쿼리를 실행하기 전에 경과해야 하는 시간 간격 및 단위를 지정합니다.|  
|**증분 업데이트 설정**|추가 데이터만 식별하도록 디자인된 폴링 및 처리 쿼리 집합에 기초하여 개체에 대한 MOLAP 캐시를 증분 업데이트합니다. 이 옵션을 선택하면 폴링 쿼리가 데이터 원본 뷰의 테이블 식별자와 연결됩니다. 그런 다음 처리 쿼리를 사용하여 폴링 쿼리의 현재 값을 이전에 실행한 폴링 쿼리의 저장된 값과 비교하여 변경 내용을 식별합니다.<br /><br /> 이 옵션을 선택하지 않으면 MOLAP 캐시가 전체 업데이트됩니다. 폴링 쿼리를 사용하여 변경 내용 발생 여부를 식별합니다. 처리 쿼리 또는 테이블 식별자는 필요 없습니다.|  
|**폴링 표**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 데이터 원본을 폴링하고 개체에 대한 기본 테이블의 변경 내용을 식별하는 데 사용하는 폴링 쿼리, 처리 쿼리 및 테이블 식별자를 포함합니다. 표에는 다음 열이 있습니다.<br /><br /> **폴링 쿼리**: 폴링 간격으로 실행되는 단일 쿼리를 입력하여 개체에 대한 변경 내용을 식별하거나, 줄임표 단추(**...**)를 클릭하여 **폴링 쿼리 만들기** 대화 상자를 열고 단일 쿼리를 정의합니다. 자세한 내용은 [폴링 쿼리 만들기 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](create-polling-query-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요. **증분 업데이트 설정** 을 선택하면 폴링 쿼리가 **테이블**에서 식별된 테이블에 마지막으로 추가된 레코드를 식별하는 값을 반환해야 합니다. **증분 업데이트 설정** 을 선택하지 않으면 폴링 쿼리가 테이블의 현재 레코드 수를 식별하는 값을 반환해야 합니다.<br /><br /> **처리 쿼리**: 폴링 간격으로 실행되는 쿼리를 입력하여 **테이블**에서 식별된 테이블에서 새 레코드를 검색하거나 줄임표 단추(**...**)를 클릭하여 **처리 쿼리 만들기** 대화 상자를 열고 쿼리를 정의합니다. 자세한 내용은 [처리 쿼리 만들기 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](create-processing-query-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요. 쿼리에 의해 반환 된 두 개의 매개 변수는 이전 값을 허용 하도록 쿼리를 매개 변수화 할지 **폴링 쿼리** 의 쿼리에 의해 반환 된 현재 값 **폴링 쿼리**-하는 데 사용 될 수 있습니다 식별 하 고 폴링 기간 중 추가 된 레코드만 추출 합니다. 이 옵션은 **증분 업데이트 설정** 을 선택한 경우에만 사용할 수 있습니다.<br /><br /> **테이블**: **폴링 쿼리**의 쿼리가 마지막 레코드를 추적하는 테이블의 식별자를 입력하거나 줄임표 단추(**...**)를 클릭하여 **테이블 찾기** 대화 상자를 열고 테이블을 선택합니다. 자세한 내용은 [테이블 찾기 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](find-table-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.|  
  
## <a name="see-also"></a>관련 항목:  
 [저장소 옵션 대화 상자 &#40;Analysis Services-다차원 데이터&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)  
  
  
