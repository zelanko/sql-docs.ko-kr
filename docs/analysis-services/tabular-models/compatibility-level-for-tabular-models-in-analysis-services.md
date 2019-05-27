---
title: Analysis Services 테이블 형식 모델에 호환성 수준 | Microsoft Docs
ms.date: 05/23/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d2176b88f01808e1b84f409cb1f1c117774a220c
ms.sourcegitcommit: 982a1dad0b58315cff7b54445f998499ef80e68d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66175127"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Analysis Services 테이블 형식 모델에 대 한 호환성 수준
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  합니다 *호환성 수준* Analysis Services 엔진의 릴리스 관련 동작을 가리킵니다. 예를 들어 DirectQuery 및 테이블 형식 개체 메타 데이터는 호환성 수준에 따라 서로 다른 구현을 갖습니다. 일반에 서버에서 지 원하는 최신 호환성 수준을 선택 해야 합니다.

  **최신 지원 되는 호환성 수준은 1400입니다.** 
  
1400 호환성 수준에서 주요 기능은 다음과 같습니다.

*  TOM Api 및 TMSL 스크립트에 대 한 지원 사용 하 여 데이터 연결 및 테이블 형식 모델로 가져오기에 대 한 새로운 인프라. 이 통해 Azure Blob 저장소와 같은 추가 데이터 원본에 대 한 지원. 추가 데이터 원본을 사용할 수는 향후 업데이트를 포함 합니다.
*  데이터 변환 및 SSDT에서 데이터 가져오기 및 M 식을 사용 하 여 데이터 매시업 기능.
*  이제 측정값을 상세 데이터로 드릴 다운 하는 Microsoft Excel과 같은 BI 도구를 사용 하도록 설정 집계 된 보고서에서 DAX 식 사용 하 여 정보 행 속성을 지원 합니다. 예를 들어 최종 사용자가 지역 및 월에 대 한 총 판매액을 볼 때 관련 된 주문 세부 정보를 볼 수 있습니다. 
*  그 안의 데이터 외에도 테이블 및 열 이름에 대 한 개체 수준 보안입니다.
*  비정형된 계층 구조에 대 한 향상 된 지원입니다.
*  성능 및 향상 된 기능을 모니터링 합니다.

  
## <a name="supported-compatibility-levels-by-version"></a>버전에서 지원 되는 호환성 수준
  
|||  
|-|-|- 
|**호환성 수준**|**서버 버전**| 
|1470|SQL Server 2019 (CTP 2.3 이상) | 
|1400|Azure Analysis Services, SQL Server 2019, SQL Server 2017 |  
|1200|Azure Analysis Services, SQL Server 2019, SQL Server 2017, SQL Server 2016| 
|1103|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1, SQL Server 2012| 

\* 호환성 수준 1100 및 1103은 SQL Server 2017에서 사용 되지 않습니다.
  
## <a name="set-compatibility-level"></a>호환성 수준 설정 
 새 테이블 형식 모델 프로젝트를 SQL Server 데이터 도구 (SSDT)를 만들 때의 호환성 수준을 지정할 수 있습니다 합니다 **테이블 형식 모델 디자이너** 대화 합니다. 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 선택 하는 경우는 **이 메시지를 다시 표시 안 함** 옵션을 모든 후속 프로젝트는 기본적으로 지정한 호환성 수준을 사용 됩니다. SSDT의 **도구** > **옵션**에서 기본 호환성 수준을 변경할 수 있습니다.  
  
 SSDT에서 테이블 형식 모델 프로젝트를 업그레이드 하려면 설정 합니다 **호환성 수준** 모델의 속성 **속성** 창입니다. 에 유의 해야, 호환성 수준 업그레이드는 되돌릴 수 없습니다.
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>SSMS에서 데이터베이스에 대한 호환성 수준 확인  
 SSMS에서 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 > **속성** > **호환성 수준**합니다.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>SSMS의 서버에 대해 지원되는 호환성 수준 확인  
 SSMS에서 서버 이름을 마우스 오른쪽 단추로 클릭 > **속성** > **지원 되는 호환성 수준**합니다.  

 이 속성에는 서버에서 실행 되는 데이터베이스의 가장 높은 호환성 수준을 지정 합니다. 지원되는 호환성 수준은 읽기 전용이며 변경할 수 없습니다.
 
> [!NOTE]  
>  SSMS는 SQL Server Analysis Services 서버, Azure Analysis Services 서버 또는 Power BI 프리미엄 작업 영역에 연결 하는 경우 지원 되는 호환성 수준 속성 1200를 표시 됩니다. 알려진된 문제 이며 향후 SSMS에서 해결 될 것이 업데이트 합니다. 해결 하는 경우이 속성에는 가장 높은 지원 되는 호환성 수준을 표시 됩니다. 
  
## <a name="see-also"></a>참고자료  
 [다차원 데이터베이스의 호환성 수준](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [What's new in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [새 테이블 형식 모델 프로젝트 만들기](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
