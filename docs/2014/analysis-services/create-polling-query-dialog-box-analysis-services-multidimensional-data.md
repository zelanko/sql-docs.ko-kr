---
title: 폴링 쿼리 대화 상자 (Analysis Services-다차원 데이터) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.createpollingquerydialog.f1
ms.assetid: 0f2902b5-796a-4eb0-be03-01514dc01b9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b58e73b7757e8288ff90f462be1868cb60e3af5b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679731"
---
# <a name="create-polling-query-dialog-box-analysis-services---multidimensional-data"></a>폴링 쿼리 작성 대화 상자(Analysis Services - 다차원 데이터)
  **의** 폴링 쿼리 만들기 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 사용하여 **저장소 옵션** 대화 상자의 **알림** 탭에서 폴링 쿼리를 만들 수 있습니다. 폴링 쿼리는 일반적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 테이블 또는 기타 관계형 개체가 변경되었는지 확인하는 데 사용할 수 있는 값을 반환하는 단일 쿼리입니다. **저장소 옵션** 대화 상자 **알림** 탭의 **예약된 폴링** 옵션에 대한 표의 **폴링 쿼리** 열에서 줄임표 단추(**...**)를 클릭하면 **폴링 쿼리 만들기** 대화 상자를 표시할 수 있습니다. **저장소 옵션** 대화 상자의 **알림** 탭에 대한 자세한 내용은 [알림&#40;저장소 옵션 대화 상자&#41;&#40;Analysis Services - 다차원 데이터&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 쿼리 중인 테이블을 기반으로 개체의 MOLAP(다차원 OLAP) 캐시에 대해 계획된 업데이트 유형에 따라 폴링 쿼리에서 반환하는 값 유형이 달라집니다.  
  
-   **저장소 옵션** 대화 상자의 **알림** 탭에서 **증분 업데이트 설정** 을 선택하지 않은 경우 예약된 폴링 중에 변경 내용이 검색되면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 개체의 MOLAP 캐시를 전체 업데이트합니다. 사용된 폴링 쿼리에서 마지막 폴링 기간 후 레코드가 테이블에 추가되었는지 확인해야 합니다.  
  
-   **저장소 옵션** 대화 상자의 **알림** 탭에서 **증분 업데이트 설정** 을 선택한 경우 예약된 폴링 중에 변경 내용이 검색되면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 개체의 MOLAP 캐시를 증분 업데이트합니다. 사용된 폴링 쿼리에서 테이블의 마지막 레코드를 확인해야 합니다.  
  
 예를 들어 다음 폴링 쿼리를 사용하여 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 예제 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 고객 차원에 대해 전체 또는 증분 업데이트를 제공할 수 있습니다.  
  
|업데이트 유형|예약된 폴링|  
|-----------------|-------------------|  
|전체 업데이트|`SELECT`<br /><br /> `COUNT(*) AS TotalCount`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|증분 업데이트|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
  
 예약된 폴링 알림을 위한 전체 및 증분 업데이트에 대한 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.  
  
 기본 공급자에 유효한 쿼리 명령을 입력해야 합니다. 쿼리는 유효성 검사에 사용할 기본 공급자와 함께 준비되며 반환된 열을 식별하게 됩니다. 대화 상자는 다음 두 가지 뷰를 제공합니다.  
  
-   VDT(Visual Database Tools) 쿼리 작성기  
  
     VDT 쿼리 작성기 뷰에서는 모든 사용자를 위해 SQL 쿼리를 시각적으로 생성하고 테스트할 수 있는 사용자 인터페이스 도구 집합을 제공합니다.  
  
-   일반 쿼리 작성기  
  
     일반 쿼리 작성기 뷰에서는 고급 사용자를 위해 SQL 쿼리를 생성하고 테스트할 수 있는 보다 단순하고 직접적인 사용자 인터페이스를 제공합니다.  
  
## <a name="options"></a>변수  
 **데이터 원본**  
 쿼리의 데이터 원본을 지정합니다.  
  
 **쿼리 정의**  
 쿼리 정의에서는 선택한 뷰에 따라 쿼리를 정의하고 테스트할 수 있는 도구 모음 및 창을 제공합니다.  
  
 **도구 모음**  
 도구 모음을 사용하여 데이터 세트를 관리하고, 표시할 창을 선택하고, 다양한 쿼리 함수를 제어할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**일반 쿼리 작성기로 전환**|일반 쿼리 작성기 뷰에 사용할 수 있는 옵션만 표시하려면 선택합니다. 다음 옵션만 표시됩니다.<br /><br /> **SQL 창**<br /><br /> **결과 창**<br /><br /> **도구 모음**( **VDT 쿼리 작성기로 전환** 및 **실행**<br /><br /> <br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**VDT 쿼리 작성기로 전환**|이 옵션을 선택하면 VDT(Visual Database Tools) 쿼리 작성기 뷰에 사용할 수 있는 모든 옵션이 표시됩니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **일반 쿼리 작성기로 전환** 을 선택 합니다.|  
|**다이어그램 창 표시/숨기기**|**다이어그램 창**을 표시하거나 숨깁니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**표 형태 창 표시/숨기기**|**표 형태 창**을 표시하거나 숨깁니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**SQL 창 표시/숨기기**|**SQL 창**을 표시하거나 숨깁니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**결과 창 표시/숨기기**|**결과 창**을 표시하거나 숨깁니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**실행**|쿼리를 실행합니다. 결과는 **결과 창**에 표시됩니다.|  
|**SQL 검증**|쿼리에서 SQL 문을 검증합니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**오름차순 정렬**|**표 형태 창**에서 선택한 열의 출력 행을 오름차순으로 정렬합니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**내림차순 정렬**|**표 형태 창**에서 선택한 열의 출력 행을 내림차순으로 정렬합니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**필터 제거**|해당 사항이 있을 경우 **표 형태 창**에서 선택한 행의 정렬 조건을 제거합니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**Group By 사용**|쿼리에 그룹화 기능을 추가합니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
|**테이블 추가**|새 테이블 또는 뷰를 쿼리에 추가할 수 있는 **테이블 추가** 대화 상자를 표시합니다. **테이블 추가** 대화 상자에 대한 자세한 내용은 [테이블 추가 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **VDT 쿼리 작성기로 전환** 을 선택 합니다.|  
  
 **다이어그램 창**  
 쿼리에서 참조하는 개체를 다이어그램으로 표시합니다. 다이어그램은 쿼리에 포함된 테이블과 이러한 테이블의 조인 방법을 보여 줍니다. 쿼리 출력에 열을 추가하거나 제거하려면 테이블에서 해당 열의 옆에 있는 확인란을 선택하거나 선택을 취소합니다.  
  
 쿼리에 테이블을 추가하면 대화 상자에서 테이블의 키를 기반으로 테이블 간의 조인을 만듭니다. 조인을 추가하려면 한 테이블의 필드를 다른 테이블의 필드로 끌어 놓습니다. 조인을 관리하려면 해당 연결을 마우스 오른쪽 단추로 클릭합니다.  
  
 **다이어그램 창** 을 마우스 오른쪽 단추로 클릭하여 테이블을 추가 또는 제거하고, 모든 테이블을 선택하고, 창을 표시하거나 숨길 수 있습니다.  
  
> [!NOTE]  
>  **다이어그램 창**, **표 형태 창**및 **SQL 창** 의 내용이 동기화되므로 하나의 창에서 변경된 내용은 나머지 두 창에도 적용됩니다.  
  
> [!IMPORTANT]  
>  대화 상자에서는 쿼리 유형을 변경할 수 없습니다.  
  
 **표 형태 창**  
 쿼리에서 참조하는 개체를 표에 표시합니다. 이 창을 사용하여 쿼리에 열을 추가하거나 제거하고 각 열의 설정을 변경할 수 있습니다.  
  
> [!NOTE]  
>  **다이어그램 창**, **표 형태 창**및 **SQL 창** 의 내용이 동기화되므로 하나의 창에서 변경된 내용은 나머지 두 창에도 적용됩니다.  
  
 **SQL 창**  
 쿼리를 SQL 문으로 표시합니다. 쿼리용 SQL 문을 변경하려면 입력합니다.  
  
> [!NOTE]  
>  **다이어그램 창**, **표 형태 창**및 **SQL 창** 의 내용이 동기화되므로 하나의 창에서 변경된 내용은 나머지 두 창에도 적용됩니다.  
  
 **결과 창**  
 **도구 모음** 창에서 **실행** 을 클릭하면 쿼리 결과를 표시합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
