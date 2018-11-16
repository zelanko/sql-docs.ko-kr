---
title: SSMS에서 DirectQuery 모드를 사용 하도록 설정 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c0a6ddb7b06cf325235f3d3998b0f57d640667a9
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700591"
---
# <a name="enable-directquery-mode-in-ssms"></a>SSMS에서 DirectQuery 모드를 사용하도록 설정
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  이미 배포된 테이블 형식 모델의 데이터 액세스 속성을 변경하여 메모리 내 상주하는 캐시된 데이터가 아닌 백 엔드 관계형 데이터 원본에 대해 쿼리가 실행되는 DirectQuery 모드를 사용하도록 설정합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 DirectQuery 구성 단계는 모델의 호환성 수준에 따라 다릅니다. 아래에서 모든 호환성 수준에 대해 해당하는 단계를 찾을 수 있습니다.  
  
 이 문서 작성 했으며 DirectQuery 액세스를 설정 하 고 연결 문자열 업데이트에 필요 하 고 호환성 수준 1200 이상에서 메모리 내 테이블 형식 모델을 유효성 검사를 가정 합니다. 낮은 호환성 수준에서 시작하는 경우 먼저 수동으로 업그레이드해야 합니다. 단계는 [Analysis Services 업그레이드](../../database-engine/install-windows/upgrade-analysis-services.md) 를 참조하세요.  
  
> [!IMPORTANT]  
>  데이터 저장소 모드를 전환하기 위해 Management Studio 대신 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 를 사용하는 것이 좋습니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 를 사용하여 모델을 변경한 다음 서버 배포로 후속 작업을 할 경우 해당 모델과 데이터베이스는 동기화를 유지합니다. 또한 모델의 저장소 모드를 변경하면 발생하는 유효성 검사 오류를 검토할 수 있습니다. 이 문서의 설명대로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용할 경우 유효성 검사 오류는 보고되지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 테이블 형식 모델에서 DirectQuery 모드를 사용하도록 설정하는 작업은 다단계 프로세스입니다.  
  
-   모델에 DirectQuery 모드에서 유효성 검사 오류를 일으킬 수 있는 기능이 없는지 확인한 다음, 모델에 대한 데이터 저장소 모드를 메모리 내에서 DirectQuery로 변경합니다.  
  
     기능 제한 사항 목록은 된다 [DirectQuery 모드](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)합니다.  
  
-   백엔드 외부 데이터베이스에서 데이터를 검색하려면 배포된 데이터베이스에서 사용하는 연결 문자열 및 자격 증명을 검토합니다. 단 하나의 연결만 있고, 해당 설정이 쿼리 실행에 적합한지 확인합니다.  
  
     DirectQuery용으로 특별히 설계되지 않은 테이블 형식 데이터베이스에는 여러 개의 연결이 있을 수 있으며, 이제 DirectQuery 모드의 요구 사항대로 하나로 줄여야 합니다.  
  
     원래 데이터 처리에 사용되는 자격 증명은 이제 데이터 쿼리에 사용됩니다. DirectQuery 구성의 일부로, 전용 작업에 다른 작업을 사용하는 경우 계정을 검토하고 변경합니다.  
  
     DirectQuery 모드는 Analysis Services가 신뢰할 수 있는 위임을 수행하는 유일한 시나리오입니다. 솔루션이 위임이 사용자 특정 쿼리 결과를 얻도록 요청할 경우 백엔드 데이터베이스에 연결하기 위해 사용한 계정은 요청하는 사용자의 ID를 위임하도록 허용해야 하며 해당 사용자 ID는 백엔드 데이터베이스에서 읽기 권한이 있어야 합니다.  
  
-   마지막 단계로, DirectQuery 모드가 쿼리 실행을 통해 작동 중인지 확인합니다.  
  
## <a name="step-1-check-the-compatibility-level"></a>1단계: 호환성 수준 확인  
 데이터 액세스를 정의하는 속성은 호환성 수준에서 서로 다릅니다. 예비 단계는 데이터베이스의 호환성 수준을 확인하는 것입니다.  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 테이블 형식 모델이 있는 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성** > **호환성 수준**을 선택합니다.  
  
     값은 **SQL Server 2016(1200)** 또는 **SQL Server 2012 SP1 이상(1103)** 과 같은 이전 수준입니다. 다음 단계에서는 호환성 수준에 적용되는 지침을 따릅니다.  
  
 테이블 형식 모델을 DirectQuery 모드로 변경하면 새 데이터 저장소 모드가 즉시 적용됩니다.  
  
## <a name="step-2a-switch-a-tabular-1200-database-to-directquery-mode"></a>2a단계: 테이블 형식 1200 데이터베이스를 DirectQuery 모드로 전환  
  
1.  개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성** > **모델** > **기본 모드**를 선택합니다.  
  
2.  모드를 **DirectQuery**로 설정합니다.  
  
    |||  
    |-|-|  
    |**유효한 값**|**설명**|  
    |**DirectQuery**|쿼리는 모델에 대해 정의된 데이터 원본 연결을 사용하여 백엔드 관계형 데이터베이스에 대해 실행됩니다.<br /><br /> 모델에 대한 쿼리는 기본 데이터베이스 쿼리로 변환되고 데이터 원본으로 리디렉션됩니다.<br /><br /> DirectQuery 모드로 설정되어 있는 모델을 처리할 경우 메타데이터만 컴파일되어 배포됩니다. 데이터 자체는 작동 가능한 데이터 원본의 데이터베이스 파일에 있는 모델의 외부입니다.|  
    |**가져오기**|쿼리는 MDX 또는 DAX에서 테이블 형식 데이터베이스에 대해 실행됩니다.<br /><br /> 가져오기 모드로 설정된 모델을 처리할 때 데이터는 백엔드 데이터 원본에서 검색되어 디스크에 저장됩니다. 데이터베이스가 로드되면 데이터는 매우 빠른 테이블 검색 및 쿼리에 대해 메모리로 완전히 복사됩니다.<br /><br /> 테이블 형식 모델에 대한 기본 모드이며 특정(비관계형) 데이터 원본에 대한 유일한 모드입니다.|  
  
## <a name="step-2b-switch-a-tabular-1100-1103-database-to-directquery-mode"></a>2b단계: 테이블 형식 1100-1103 데이터베이스를 DirectQuery 모드로 전환  
  
1.  개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성** > **데이터베이스** > **DirectQueryMode**를 선택합니다.  
  
2.  모드를 **DirectQuery**로 설정합니다.  
  
     기본 모드 속성은 다음과 같이 구성되어 있습니다.  
  
    |||  
    |-|-|  
    |**유효한 값**|**설명**|  
    |**InMemory**|쿼리는 캐시된 메모리 내 데이터만 사용합니다.|  
    |**InMemoryWithDirectQuery**|클라이언트에서 연결 문자열에 다르게 지정되어 있지 않으면 기본적으로 쿼리에서 캐시를 사용합니다.<br /><br /> 파티션이 메모리 내 또는 DirectQuery를 사용하도록 개별 구성되어 있는 하이브리드 모드입니다.|  
    |**DirectQuery**|쿼리에서 관계형 데이터 원본만 사용합니다.|  
    |**DirectQuerywithInMemory**|클라이언트에서 연결 문자열에 다르게 지정되어 있지 않으면 기본적으로 쿼리에서 관계형 데이터 원본을 사용합니다.<br /><br /> 파티션이 메모리 내 또는 DirectQuery를 사용하도록 개별 구성되어 있는 하이브리드 모드입니다.|  
  
 **하이브리드 데이터 저장소**  
  
 메모리 내와 디스크 기반 액세스의 조합을 사용할 경우 여전히 캐시 사용이 가능하며 쿼리에 사용할 수 있습니다. 혼합 모드에서는 여러 가지 옵션이 제공됩니다.  
  
-   캐시와 관계형 데이터 원본 모두 사용할 수 있는 경우 기본적으로 사용되는 연결 방법을 설정할 수 있지만 궁극적으로는 클라이언트가 DirectQueryMode 연결 문자열 속성을 사용하여 사용되는 원본을 제어합니다.  
  
-   DirectQuery 모드에 사용된 기본 파티션이 절대 처리되지 않는 방식으로 캐시에 파티션을 구성할 수 있으며 항상 관계형 원본을 참조해야 합니다. 여러 가지 방법으로 파티션을 사용하여 모델 디자인 및 보고 환경을 최적화할 수 있습니다. 자세한 내용은 [DirectQuery 모델에서 파티션 정의](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)합니다.  
  
-   모델을 배포한 후 기본적으로 사용되는 연결 방법을 변경할 수 있습니다. 예를 들어 모델을 사용하는 보고서나 쿼리를 모두 철저히 테스트한 후에만 테스트에 혼합 모드를 사용하고 모델을 **DirectQuery 전용** 모드로 전환할 수 있습니다. 자세한 내용은 [DirectQuery의 기본 연결 방법 설정 또는 변경](http://msdn.microsoft.com/library/f10d5678-d678-4251-8cce-4e30cfe15751)을 참조하세요.  
  
## <a name="step-3-check-the-connection-properties-on-the-database"></a>3단계: 데이터베이스에서 연결 속성 확인  
 데이터 원본 연결 설정 방법에 따라 DirectQuery로 전환하면 연결의 보안 컨텍스트가 변경될 수 있습니다. 데이터 액세스 모드를 변경할 경우 가장 및 연결 문자열 속성을 검토하여 로그인이 백엔드 데이터베이스에 대한 현재 연결에 유효한지 확인합니다.  
  
 DirectQuery 시나리오의 사용자 ID 위임에 대한 백그라운드 정보는 **Configure Analysis Services for Kerberos constrained delegation** 에서 [신뢰할 수 있는 위임에 대한 Analysis Services 구성](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) 을 검토합니다.  
  
1.  개체 탐색기에서 **연결** 을 확장한 후 연결을 두 번 클릭하여 속성을 봅니다.  
  
     DirectQuery 모델의 경우 데이터베이스에 대해 단 하나의 연결만 정의되어 있어야 하며, 데이터 원본은 관계형이고 지원되는 데이터베이스 형식이어야 합니다. 참조 [지원 되는 데이터 원본](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)합니다.  
  
2.  **연결 문자열** 은 서버, 데이터베이스 이름은 물론 DirectQuery 작업에서 사용하는 인증 방법을 지정해야 합니다. SQL Server 인증을 사용하고 있는 경우 여기에서 데이터베이스 로그인을 지정할 수 있습니다.  
  
3.  **가장 정보** 는 Windows 인증에 사용됩니다. DirectQuery 모드에서 테이블 형식 모델에 적합한 옵션은 다음과 같습니다.  
  
    -   **서비스 계정 사용** Analysis Services 서비스 계정이 관계형 데이터베이스에 대한 읽기 권한이 있는 경우 이 옵션을 선택할 수 있습니다.  
  
    -   **특정 사용자 이름 및 암호 사용** 관계형 데이터베이스에 대한 읽기 권한이 있는 Windows 사용자 계정을 지정합니다.  
  
 이러한 자격 증명은 관계형 데이터 저장소에 대한 쿼리 응답에만 사용되며, 혼합 모델의 캐시를 처리하는 데 사용되는 자격 증명과는 다릅니다.  
  
 모델을 메모리에 내에서만 사용하는 경우에는 가장을 사용할 수 없습니다. 모델에서 DirectQuery 모드를 사용하지 않는 경우에는 **ImpersonateCurrentUser**설정이 유효하지 않습니다.  
  
## <a name="step-4-validate-directquery-access"></a>4단계: DirectQuery 액세스의 유효성 검사  
  
1.  SQL Server의 관계형 데이터베이스에 연결된 Management Studio에서 SQL Server Profiler 또는 xEvent를 사용하여 추적을 시작합니다.  
  
     Oracle 또는 Teradata를 사용하는 경우 해당 데이터베이스 플랫폼에 대한 추적 도구를 사용합니다.  
  
2.  Management Studio에 들어 가서 `select <some measure> on 0 from model.`등의 단순 MDX 쿼리를 실행합니다.  
  
3.  추적에서 관계형 데이터베이스에 대한 쿼리 실행의 증거를 확인해야 합니다.  
  
## <a name="see-also"></a>참고자료  
 [호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [지원 되는 데이터 원본](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   

  
  
