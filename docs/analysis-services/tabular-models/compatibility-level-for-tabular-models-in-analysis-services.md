---
title: "Analysis Services 테이블 형식 모델에 호환성 수준이 | Microsoft Docs"
ms.custom: 
ms.date: 07/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 58710676e09a49ecc1b49ad37c656e3589ee1257
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Analysis Services 테이블 형식 모델에 대 한 호환성 수준
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  *호환성 수준이* Analysis Services 엔진의 릴리스 관련 동작을 가리킵니다. 예를 들어 DirectQuery 및 테이블 형식 개체 메타 데이터는 서로 다른 구현이 호환성 수준에 따라 합니다. 일반에 서버에서 지 원하는 최신 호환성 수준을 선택 해야 합니다.

  **최신 호환성 수준은 1400** 
  
1400 호환성 수준에서 주요 기능은 다음과 같습니다.

*  TOM Api 및 TMSL 스크립트를 지 원하는 데이터 연결 및 테이블 형식 모델에 가져오기에 대 한 새로운 인프라입니다. 이 통해 Azure Blob 저장소와 같은 추가 데이터 원본에 대 한 지원. 추가 데이터 원본을 사용할 수는 향후 업데이트를 포함 합니다.
*  데이터 변환 및 데이터 가져오기 및 M 식을 사용 하 여 데이터 매시업 기능입니다.
*  측정값 집계 된 보고서에서 자세한 데이터를 드릴 다운 하는 Microsoft Excel과 같은 BI 도구를 사용 하도록 설정 하는 DAX 식 사용 하 여 정보 행 속성을 지원 합니다. 예를 들어 최종 사용자가 보는 지역 및 월에 대 한 총 판매액을 관련된 주문 세부 정보를 볼 수 있습니다. 
*  내 데이터 외에도 테이블 및 열 이름에 대 한 개체 수준 보안 합니다.
*  비정형된 계층 구조에 대 한 향상 된 지원 합니다.
*  성능 및 향상 된 기능을 모니터링 합니다.

  
## <a name="supported-compatibility-levels-by-version"></a>버전에서 지원 되는 호환성 수준
  
|||  
|-|-|- 
|**호환성 수준**|**서버 버전**| 
|1400|SQL Server 2017 azure Analysis Services (미리 보기) |  
|1200|Azure Analysis Services, SQL Server 2017 년 1 SQL Server 2016| 
|1103|SQL Server 2017 *, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017 *, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1, SQL Server 2012| 

\*1100 및 1103 호환성 수준은 SQL Server 2017에서는 사용 되지 않습니다.
  
## <a name="set-compatibility-level"></a>호환성 수준을 설정 
 새 테이블 형식 모델 프로젝트를 SQL Server Data Tools (SSDT)를 만들 때에 호환성 수준을 지정할 수 있습니다는 **테이블 형식 모델 디자이너** 대화 상자. 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 선택 하는 경우는 **이 메시지를 다시 표시 안 함** 옵션을 모든 후속 프로젝트는 기본적으로 지정 된 호환성 수준을 사용 합니다. SSDT의 **도구** > **옵션**에서 기본 호환성 수준을 변경할 수 있습니다.  
  
 SSDT에서 테이블 형식 모델 프로젝트를 업그레이드 하려면 설정는 **호환성 수준이** 모델의 속성 **속성** 창. 에 유의 해야, 호환성 수준이 업그레이드은 취소할 수 없습니다.
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>SSMS에서 데이터베이스에 대한 호환성 수준 확인  
 SSMS에서 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 > **속성** > **호환성 수준이**합니다.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>SSMS의 서버에 대해 지원되는 호환성 수준 확인  
 SSMS에서 서버 이름을 마우스 오른쪽 단추로 클릭 > **속성** > **호환성 수준을 지원**합니다.  
  
 이 속성에는 서버에서 실행 되는 데이터베이스의 가장 높은 호환성 수준을 지정 합니다. 지원되는 호환성 수준은 읽기 전용이며 변경할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [다차원 데이터베이스의 호환성 수준](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Analysis Services의 새로운 기능](../../analysis-services/what-s-new-in-analysis-services.md)   
 [새 테이블 형식 모델 프로젝트 만들기](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  

