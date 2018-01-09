---
title: "큐브, 파티션 및 차원 처리에 대 한 오류 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.cubeproperties.errorconfiguration.f1
- sql13.asvs.sqlserverstudio.partitionproperties.errorconfiguration.f1
- sql13.asvs.sqlserverstudio.dimensionproperties.errorconfiguration.f1
ms.assetid: 3f442645-790d-4dc8-b60a-709c98022aae
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9dcbefced6fd34dd5fa69537733d7820b0130f4d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="error-configuration-for-cube-partition-and-dimension-processing"></a>큐브, 파티션 및 차원 처리에 대 한 오류 구성
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]오류 구성 속성에 큐브, 파티션 또는 차원 개체 처리 시 데이터 무결성 오류가 발생할 경우 서버가 응답 하는 방법을 결정 합니다. 일반적으로 키 열의 중복 키, 누락된 키 및 Null 값에 의해 이러한 오류가 트리거되며, 오류의 원인이 되는 레코드가 데이터베이스에 추가되지 않지만 다음에 발생하는 작업을 결정하는 속성을 설정할 수 있습니다. 기본적으로 처리가 중지됩니다. 그러나 큐브를 개발하는 중에 오류가 발생하는 경우 가져온 데이터로 큐브 동작을 테스트할 수 있도록 처리를 계속할 수 있습니다(가져온 데이터가 완전하지 않은 경우 포함).  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
-   [실행 순서](#bkmk_exec)  
  
-   [기본 동작](#bkmk_default)  
  
-   [오류 구성 속성](#bkmk_props)  
  
-   [오류 구성 속성을 설정하는 위치](#bkmk_tools)  
  
-   [누락된 키(KeyNotFound)](#bkmk_missing)  
  
-   [팩트 테이블의 Null 외래 키(KeyNotFound)](#bkmk_nullfact)  
  
-   [차원의 Null 키](#bkmk_nulldim)  
  
-   [일관성 없는 관계를 발생시키는 중복 키(KeyDuplicate)](#bkmk_dupe)  
  
-   [오류 제한 또는 오류 제한 동작 변경](#bkmk_limit)  
  
-   [오류 로그 경로 설정](#bkmk_log)  
  
-   [다음 단계](#bkmk_next)  
  
##  <a name="bkmk_exec"></a> 실행 순서  
 서버는 항상 각 레코드에 대해 **NullProcessing** 규칙을 실행하기 전에 **ErrorConfiguration** 규칙을 실행합니다. Null을 0으로 변환하는 Null 처리 속성을 사용할 경우 이후에 두 개 이상의 오류 레코드의 키 열에 0이 있으면 중복 키 오류가 발생할 수 있으므로 이러한 사항을 알아 두는 것이 중요합니다.  
  
##  <a name="bkmk_default"></a> 기본 동작  
 기본적으로 키 열과 관련된 첫 번째 오류에서 처리가 중지됩니다. 이 동작은 허용되는 오류 수를 0으로 지정하는 오류 제한과 오류 제한에 도달할 경우 처리를 중지하도록 서버에 알려주는 중지 처리 지시문에 의해 제어됩니다.  
  
 Null 또는 누락된 값이나 중복 값 때문에 오류를 트리거하는 레코드는 알 수 없는 멤버로 변환되거나 삭제됩니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 데이터 무결성 제약 조건을 위반하는 데이터를 가져올 수 없습니다.  
  
-   알 수 없는 멤버로의 변환은 기본적으로 **ConvertToUnknown** 의 **KeyErrorAction**설정 때문에 발생합니다. 알 수 없는 멤버에 할당된 레코드는 처리가 완료된 후 조사할 수 있는 문제가 있다는 증거로 데이터베이스에서 격리됩니다.  
  
     알 수 없는 멤버는 쿼리 작업에서 제외되지만 **UnknownMember** 가 **표시**로 설정되어 있으면 일부 클라이언트 응용 프로그램에서 해당 멤버가 표시됩니다.  
  
     알 수 없는 멤버로 변환된 Null 개수를 추적하려는 경우 이러한 오류를 로그 또는 처리 창에 보고하도록 **NullKeyConvertedToUnknown** 속성을 수정할 수 있습니다.  
  
-   **KeyErrorAction** 속성을 **DiscardRecord**로 수동으로 설정하면 삭제가 발생합니다.  
  
 오류 구성 속성을 통해, 오류가 발생하는 경우 서버가 응답하는 방식을 결정할 수 있습니다. 즉시 처리를 중지하거나, 계속 처리하되 기록을 중지하거나, 오류 처리 및 기록 둘 다를 계속할 수 있습니다. 기본값은 오류의 심각도에 따라 달라집니다.  
  
 오류 수는 발생하는 오류 수를 추적합니다. 상한을 설정하면 해당 제한에 도달할 경우 서버 응답이 변경됩니다. 기본적으로 서버는 제한에 도달하면 처리를 중지합니다. 기본 제한은 0이며, 이 값으로 설정할 경우 개수에 포함되는 첫 번째 오류에서 처리가 중지됩니다.  
  
 키 필드에 있는 누락된 키 또는 Null 값과 같이 많은 영향을 주는 오류는 신속하게 해결해야 합니다. 기본적으로 이러한 오류는 **ReportAndContinue** 서버 동작을 따릅니다. 즉, 서버가 오류를 catch하고 오류 수에 해당 오류를 추가한 다음 계속 처리합니다(오류 제한이 0이어서 바로 처리가 중지되는 경우 제외).  
  
 오류가 반드시 데이터 무결성 문제를 일으키는 것은 아니기 때문에 다른 오류는 생성되지만 기본적으로 개수에 포함되거나 기록되지 않습니다( **IgnoreError** 설정).  
  
 오류 수는 Null 처리 설정의 영향을 받습니다. 차원 특성의 경우 Null 처리 옵션은 Null 값이 있을 경우 서버가 응답하는 방법을 결정합니다. 기본적으로 문자열 열의 Null은 공백 문자열로 처리되는 반면 숫자 열의 Null은 0으로 변환됩니다. Null 값이 **NullProcessing** 또는 **KeyNotFound** 오류로 바뀌기 전에 Null 값을 catch하도록 **KeyDuplicate** 속성을 재정의할 수 있습니다. 자세한 내용은 [차원의 Null 키](#bkmk_nulldim) 를 참조하세요.  
  
 오류는 처리 대화 상자에 기록되지만 저장되지는 않습니다. 키 오류 로그 파일 이름을 지정하여 텍스트 파일에 오류를 수집할 수 있습니다.  
  
##  <a name="bkmk_props"></a> 오류 구성 속성  
 9개의 오류 구성 속성이 있습니다. 이 중 5개는 특정 오류가 발생하는 경우 서버 응답을 결정하는 데 사용됩니다. 나머지 4개는 허용되는 오류 수, 해당 제한에 도달할 경우 수행할 작업, 로그 파일에 오류를 수집할지 여부 등과 같은 오류 구성 작업으로 한정됩니다.  
  
 **특정 오류에 대한 서버 응답**  
  
|속성|Default|다른 값|  
|--------------|-------------|------------------|  
|**CalculationError**<br /><br /> 오류 구성을 초기화할 때 발생합니다.|**IgnoreError** 는 오류를 기록하거나 오류 수를 계산하지 않습니다. 오류 수가 최대 제한 미만이면 처리가 계속됩니다.|**ReportAndContinue** 는 오류를 기록하고 오류 수를 계산합니다.<br /><br /> **ReportAndStop** 은 오류 제한에 관계없이 오류를 보고하고 즉시 처리를 중지합니다.|  
|**KeyNotFound**<br /><br /> 팩트 테이블의 외래 키에 관련 차원 테이블의 일치하는 기본 키가 없는 경우(예: Sales 팩트 테이블에 제품 ID가 Product 차원 테이블에 없는 레코드가 있는 경우) 발생합니다. 이 오류는 눈송이 차원의 차원 처리 또는 파티션 처리 중에 발생할 수 있습니다.|**ReportAndContinue** 는 오류를 기록하고 오류 수를 계산합니다.|**ReportAndStop** 은 오류 제한에 관계없이 오류를 보고하고 즉시 처리를 중지합니다.<br /><br /> **IgnoreError** 는 오류를 기록하거나 오류 수를 계산하지 않습니다. 오류 수가 최대 제한 미만이면 처리가 계속됩니다. 이 오류를 트리거하는 레코드는 기본적으로 알 수 없는 멤버로 변환되지만 대신 해당 레코드를 삭제하도록 **KeyErrorAction** 속성을 변경할 수 있습니다.|  
|**KeyDuplicate**<br /><br /> 차원에 중복 특성 키가 있는 경우 발생합니다. 대부분의 경우 중복 특성 키를 포함하도록 허용되지만 이 오류는 특성 간에 일관성 없는 관계를 발생시킬 수 있는 차원의 디자인 결함을 확인할 수 있도록 중복 사실을 알려 줍니다.|**IgnoreError** 는 오류를 기록하거나 오류 수를 계산하지 않습니다. 오류 수가 최대 제한 미만이면 처리가 계속됩니다.|**ReportAndContinue** 는 오류를 기록하고 오류 수를 계산합니다.<br /><br /> **ReportAndStop** 은 오류 제한에 관계없이 오류를 보고하고 즉시 처리를 중지합니다.|  
|**NullKeyNotAllowed**<br /><br /> 차원 특성에 대해 **NullProcessing** = **Error** 가 설정되어 있거나 멤버를 고유하게 식별하는 데 사용되는 특성 키 열에 Null 값이 있는 경우 발생합니다.|**ReportAndContinue** 는 오류를 기록하고 오류 수를 계산합니다.|**ReportAndStop** 은 오류 제한에 관계없이 오류를 보고하고 즉시 처리를 중지합니다.<br /><br /> **IgnoreError** 는 오류를 기록하거나 오류 수를 계산하지 않습니다. 오류 수가 최대 제한 미만이면 처리가 계속됩니다. 이 오류를 트리거하는 레코드는 기본적으로 알 수 없는 멤버로 변환되지만 대신 해당 레코드를 삭제하도록 **KeyErrorAction** 속성을 설정할 수 있습니다.|  
|**NullKeyConvertedToUnknown**<br /><br /> Null 값이 이후에 알 수 없는 멤버로 변환되는 경우 발생합니다. 차원 특성에 대해 **NullProcessing** = **ConvertToUnknown** 으로 설정하면 이 오류가 트리거됩니다.|**IgnoreError** 는 오류를 기록하거나 오류 수를 계산하지 않습니다. 오류 수가 최대 제한 미만이면 처리가 계속됩니다.|이 오류가 도움이 되는 정보라고 판단되면 기본값을 유지하십시오. 그렇지 않으면 **ReportAndContinue** 를 선택하여 처리 창에 오류를 보고하고 오류 제한에 오류 수를 계산할 수 있습니다.<br /><br /> **ReportAndStop** 은 오류 제한에 관계없이 오류를 보고하고 즉시 처리를 중지합니다.|  
  
 **일반 속성**  
  
|**속성**|**값**|  
|------------------|----------------|  
|**KeyErrorAction**|**KeyNotFound** 오류가 발생하는 경우 서버에서 수행하는 동작입니다. 이 오류에 대한 유효한 응답에는 **ConvertToUnknown** 또는 **DiscardRecord**가 포함됩니다.|  
|**KeyErrorLogFile**|서비스 계정이 읽기-쓰기 권한을 가지고 있는 폴더에 있는 사용자 정의 파일 이름이며, 이 파일의 확장명은 .log여야 합니다. 이 로그 파일에는 처리 중에 생성된 오류만 포함됩니다. 보다 자세한 정보가 필요한 경우 비행 레코더를 사용하십시오.|  
|**KeyErrorLimit**|서버에서 처리를 중지하기 전에 허용할 데이터 무결성 오류의 최대 수입니다. -1 값은 제한이 없음을 나타냅니다. 기본값은 0이며 처음 오류가 발생한 후 처리가 중지됨을 의미합니다. 이 값을 정수로 설정할 수도 있습니다.|  
|**KeyErrorLimitAction**|키 오류 수가 상한에 도달했을 때 서버가 수행하는 동작입니다. **처리 중지**를 사용할 경우 즉시 처리가 종료됩니다. **로깅 중지**를 사용할 경우 처리가 계속되지만 더 이상 오류가 기록되거나 오류 수가 계산되지 않습니다.|  
  
##  <a name="bkmk_tools"></a> 오류 구성 속성을 설정하는 위치  
 데이터베이스가 배포된 후 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 또는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 모델 프로젝트에서 속성 페이지를 사용할 수 있습니다. 두 도구 모두에 동일한 속성이 있습니다. msmdrsrv.ini 파일에서 오류 구성 속성을 설정하여 오류 구성에 대한 서버 기본값을 변경할 수도 있으며, 처리가 스크립팅된 작업으로 실행되는 경우 **Batch** 및 **Process** 명령에서 설정할 수도 있습니다.  
  
 독립 실행형 작업으로 처리할 수 있는 개체에 대한 오류 구성을 설정할 수 있습니다.  
  
#### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
  
1.  개체 탐색기에서 차원, 큐브, 파티션 개체 중 하나에 대한 **속성** 을 마우스 오른쪽 단추로 클릭합니다.  
  
2.  속성에서 **오류 구성**을 클릭합니다.  
  
#### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
  
1.  솔루션 탐색기에서 차원 또는 큐브를 두 번 클릭합니다. 아래 창의 속성에**ErrorConfiguration** 이 나타납니다.  
  
2.  또는 단일 차원의 경우 솔루션 탐색기에서 차원을 마우스 오른쪽 단추로 클릭하고 **처리**를 선택한 다음, 차원 처리 대화 상자에서 **설정 변경** 을 선택합니다. 차원 키 오류 탭에 오류 구성 옵션이 나타납니다.  
  
##  <a name="bkmk_missing"></a> 누락된 키(KeyNotFound)  
 키 값이 누락된 레코드는 데이터베이스에 추가할 수 없습니다. 오류가 무시되거나 오류 제한이 무제한인 경우에도 마찬가지입니다.  
  
 팩트 레코드의 테이블에 외래 키 값이 포함되어 있지만 외래 키에 관련 차원 테이블의 해당 레코드가 없는 경우 서버는 파티션 처리 중에 **KeyNotFound** 오류를 생성합니다. 한 차원의 레코드가 관련 차원에 없는 외래 키를 지정하는 관련된 차원 테이블 또는 눈송이 차원 테이블을 처리할 때도 이 오류가 발생합니다.  
  
 **KeyNotFound** 오류가 발생하면 오류가 발생한 레코드가 알 수 없는 멤버에 할당됩니다. 추가 조사를 위해 할당된 레코드를 볼 수 있도록 이 동작은 **ConvertToUnknown**으로 설정된 **키 동작**을 통해 제어됩니다.  
  
##  <a name="bkmk_nullfact"></a> 팩트 테이블의 Null 외래 키(KeyNotFound)  
 기본적으로 팩트 테이블의 외래 키 열에 있는 Null 값은 0으로 변환됩니다. 0이 유효한 외래 키 값이 아니라고 가정하면 **KeyNotFound** 오류가 기록되고 기본적으로 0인 오류 제한에 오류 수가 계산됩니다.  
  
 처리가 계속되도록 하기 위해, Null이 변환되고 오류가 확인되기 전에 Null을 처리할 수 있습니다. 이렇게 하려면 **NullProcessing** 을 **오류**로 설정하십시오.  
  
#### <a name="set-nullprocessing-property-on-a-measure"></a>측정값에 대한 NullProcessing 속성 설정  
  
1.  SQL Server Data Tools의 솔루션 탐색기에서 큐브를 두 번 클릭하여 큐브 디자이너에서 엽니다.  
  
2.  측정값 창에서 측정값을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  속성에서 **Source** 를 확장하여 **NullProcessing** 속성을 확인합니다. 이 속성은 **자동** 으로 기본 설정되어 있으므로 OLAP 항목에 대해 숫자 데이터를 포함하는 필드의 경우 Null을 0으로 변환합니다.  
  
4.  Null이 숫자 0으로 변환되지 않도록 값을 **Error** 로 변경하여 Null 값을 가진 레코드를 제외합니다. 이렇게 수정하면 키 열의 값이 0인 여러 레코드와 관련된 중복 키 오류가 발생하지 않고, 값이 0인 외래 키에 관련 차원 테이블의 해당 기본 키가 없는 경우 **KeyNotFound** 오류가 발생하지 않습니다.  
  
##  <a name="bkmk_nulldim"></a> 차원의 Null 키  
 눈송이 차원의 외래 키에 Null 값이 있는 경우 처리를 계속하려면 먼저 차원 속성의 **NullProcessing** 에서 **KeyColumn** 을 설정하여 Null 값을 처리하십시오. 그러면 **KeyNotFound** 오류가 발생하기 전에 레코드가 삭제되거나 변환됩니다.  
  
 차원 특성의 Null을 처리하기 위한 두 가지 옵션이 있습니다.  
  
-   **NullProcessing**=**UnknownMember** 로 설정하여 Null 값이 있는 레코드를 알 수 없는 멤버에 할당합니다. 그러면 **NullKeyConvertedToUnknown** 오류가 생성되며 이 오류는 기본적으로 무시됩니다.  
  
-   **NullProcessing**=**Error** 로 설정하여 Null 값이 있는 레코드를 제외합니다. 그러면 **NullKeyNotAllowed** 오류가 생성됩니다. 이 오류는 기록되고 키 오류 제한에 오류 수가 계산됩니다. **Null 키가 허용되지 않는 경우** 에서 오류 구성 속성을 **IgnoreError** 로 설정하여 처리가 계속되도록 할 수 있습니다.  
  
 MDX 쿼리는 Null이 0으로 해석되는지 공백으로 해석되는지에 따라 다른 값을 반환하므로 키가 아닌 필드의 경우 Null이 문제가 될 수 있습니다. 이러한 이유로, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 원하는 변환 동작을 미리 정의할 수 있도록 Null 처리 옵션을 제공합니다. 자세한 내용은 [알 수 없는 멤버 및 Null 처리 속성 정의](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) 및 <xref:Microsoft.AnalysisServices.NullProcessing> 를 참조하세요.  
  
#### <a name="set-nullprocessing-property-on-a-dimension-attribute"></a>차원 특성에 대한 NullProcessing 속성 설정  
  
1.  SQL Server Data Tools의 솔루션 탐색기에서 차원을 두 번 클릭하여 차원 디자이너에서 엽니다.  
  
2.  특성 창에서 특성을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  속성에서 **KeyColumns** 를 확장하여 **NullProcessing** 속성을 확인합니다. 이 속성은 **자동** 으로 기본 설정되어 있으므로 숫자 데이터를 포함하는 필드의 경우 Null을 0으로 변환합니다. 값을 **Error** 또는 **UnknownMember**로 변경합니다.  
  
     이렇게 수정하면 오류가 확인되기 전에 레코드를 삭제하거나 변환하여 **KeyNotFound** 를 트리거하는 기본 조건이 제거됩니다.  
  
     오류 구성에 따라 이러한 동작 중 하나로 인해 보고 및 계산되는 오류가 발생할 수 있습니다. **KeyNotFound** 를 **ReportAndContinue** 로 설정하거나 **KeyErrorLimit** 를 0이 아닌 값으로 설정하는 것과 같이 추가 속성을 조정하여 이러한 오류가 보고 및 계산될 때 처리를 계속하도록 허용해야 할 수 있습니다.  
  
##  <a name="bkmk_dupe"></a> 일관성 없는 관계를 발생시키는 중복 키(KeyDuplicate)  
 기본적으로 중복 키가 있다고 해서 처리가 중지되지는 않지만 오류가 무시되고 중복 레코드가 데이터베이스에서 제외됩니다.  
  
 이 동작을 변경하려면 **KeyDuplicate** 을 **ReportAndContinue** 또는 **ReportAndStop** 으로 설정하여 오류를 보고하십시오. 그러면 오류를 검사하여 차원 디자인의 잠재적 결함을 확인할 수 있습니다.  
  
##  <a name="bkmk_limit"></a> 오류 제한 또는 오류 제한 동작 변경  
 처리 중에 더 많은 오류가 허용되도록 오류 제한을 높일 수 있습니다. 오류 제한을 높이는 데 대한 지침은 없으며 시나리오에 따라 적합한 값이 달라집니다. 오류 제한은 **의** ErrorConfiguration **속성에서** KeyErrorLimit [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]로 지정되거나 **의 차원, 큐브 또는 측정값 그룹의 속성에 대한 오류 구성 탭에서** 오류 개수 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]로 지정됩니다.  
  
 오류 제한에 도달하면 처리가 중지되거나 로깅이 중지되도록 지정할 수 있습니다. 예를 들어 오류 제한 100에 대한 동작을 **StopLogging** 으로 설정했다고 가정해 보겠습니다. 101번째 오류가 발생할 경우 처리는 계속되지만 더 이상 오류가 기록되거나 오류 수가 계산되지 않습니다. 오류 제한 동작은 **의** ErrorConfiguration **속성에서** KeyErrorLimitAction [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]으로 지정되거나 **의 차원, 큐브 또는 측정값 그룹의 속성에 대한 오류 구성 탭에서** 오류 시 수행할 동작 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]으로 지정됩니다.  
  
##  <a name="bkmk_log"></a> 오류 로그 경로 설정  
 처리 중에 보고되는 키 관련 오류 메시지를 저장할 파일을 지정할 수 있습니다. 기본적으로 오류는 대화형 처리 중에 처리 창에 표시된 다음 창 또는 세션을 종료할 경우 삭제됩니다. 로그는 처리 대화 상자에서 보고된 오류와 동일한 키와 관련된 오류 정보만 포함합니다.  
  
 오류는 텍스트 파일에 기록되며 파일 확장명이 .log여야 합니다. 오류가 발생하지 않으면 해당 파일은 비어 있게 됩니다. 기본적으로 파일은 DATA 폴더에 만들어집니다. Analysis Services 서비스 계정이 다른 폴더에 기록할 수 있으면 해당 폴더를 지정할 수 있습니다.  
  
##  <a name="bkmk_next"></a> 다음 단계  
 오류로 인해 처리를 중지할지 오류를 무시할지 결정합니다. 오류만 무시됩니다. 오류를 발생시킨 레코드는 무시되지 않으며 삭제되거나 알 수 없는 멤버로 변환됩니다. 데이터 무결성 규칙을 위반하는 레코드는 데이터베이스에 추가되지 않습니다. 기본적으로 첫 번째 오류가 발생할 때 처리가 중지되지만 오류 제한을 높여서 이를 변경할 수 있습니다. 큐브 개발 시 오류 구성 규칙을 완화하여 테스트할 데이터가 있도록 처리를 계속할 수 있게 허용하는 것이 유용할 수 있습니다.  
  
 기본 Null 처리 동작을 변경할지 여부를 결정합니다. 기본적으로 숫자 열의 Null은 0으로 처리되는 반면 문자열 열의 Null은 빈 값으로 처리됩니다. 특성에 대한 Null 처리를 설정하는 데 대한 지침은 [Defining the Unknown Member and Null Processing Properties](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) 를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [로그 속성](../../analysis-services/server-properties/log-properties.md)   
 [알 수 없는 멤버 및 Null 처리 속성 정의](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
  
