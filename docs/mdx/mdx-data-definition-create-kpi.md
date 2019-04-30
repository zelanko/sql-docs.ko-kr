---
title: CREATE KPI 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a905c223418392ee9d3bd45dffbfe2ab821a298
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181545"
---
# <a name="mdx-data-definition---create-kpi"></a>MDX 데이터 정의 - CREATE KPI


  KPI(핵심 성과 지표)를 만듭니다. KPI는 비즈니스 또는 목표 성과를 평가하는 데 사용되는 큐브의 측정값 그룹과 관련된 계산 모음입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE KPI CURRENTCUBE | <Cube Name>.KPI_Name AS KPI_Value  
   [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>인수  
 *KPI_Name*  
 KPI 이름을 지정하는 유효한 문자열입니다.  
  
 *KPI_Value*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
 *Property_Name*  
 KPI 속성의 이름을 지정하는 유효한 문자열입니다.  
  
 *Property_Value*  
 KPI 속성의 값을 정의하는 유효한 스칼라 식입니다.  
  
## <a name="remarks"></a>Remarks  
 현재 연결된 큐브가 아닌 다른 큐브를 지정하면 오류가 발생합니다. 따라서 큐브 이름에서 CURRENTCUBE를 사용하여 현재 큐브를 표시해야 합니다.  
  
## <a name="kpi-properties"></a>KPI 속성  
 다음 표에서는 모든 KPI 속성에 대해 설명합니다. 이 속성에는 기본값이 없습니다. 따라서 KPI 속성에 특정 값을 할당할 때까지 이 속성에 대한 쿼리는 null 값을 반환합니다.  
  
|속성 식별자|의미|  
|-------------------------|-------------|  
|GOAL|숫자 값을 반환하는 유효한 MDX 식입니다.|  
|STATUS|숫자 값을 반환하는 유효한 MDX 식입니다.|  
|STATUS_GRAPHIC|클라이언트 응용 프로그램이 사용하는 그래픽 이미지의 집합을 정의하는 문자열입니다.|  
|TREND|숫자 값을 반환하는 유효한 MDX 식입니다.|  
|TREND_GRAPHIC|클라이언트 응용 프로그램이 사용하는 그래픽 이미지의 집합을 정의하는 문자열입니다.|  
|WEIGHT|숫자 값을 반환하는 유효한 MDX 식입니다.|  
|CURRENT_TIME_MEMBER|시간 차원의 멤버를 반환하는 유효한 MDX 식입니다. CURRENT_TIME_MEMBER는 모든 상대적 시간 함수의 참조 지점을 설정합니다.|  
|PARENT_KPI|부모 KPI의 이름을 지정하는 문자열입니다.|  
|CAPTION|클라이언트 응용 프로그램이 KPI에 대한 캡션으로 사용하는 문자열입니다.|  
|DISPLAY_FOLDER|클라이언트 응용 프로그램이 KPI를 표시하는 표시 폴더의 경로를 지정하는 문자열입니다. 폴더 수준 구분 기호는 클라이언트 응용 프로그램에서 정의합니다. 도구 및 클라이언트에서 제공한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 백슬래시 (\\)가 수준 구분 기호입니다. 정의 멤버에 대해 여러 표시 폴더를 제공하려면 세미콜론(;)을 사용하여 폴더를 구분하십시오.|  
|ASSOCIATED_MEASURE_GROUP|모든 MDX 계산에서 참조하는 측정값 그룹의 이름을 지정하는 문자열입니다.|  
  
 GOAL, STATUS 및 TREND 속성의 값은 -1과 1 사이의 값으로 계산되는 MDX 식입니다. 그러나 이러한 속성 값의 실제 범위는 클라이언트 응용 프로그램에서 정의합니다. 사용 하는 경우 클라이언트에서 제공 하 고 도구 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Kpi를 찾아볼-1 보다 작은 값으로 처리할지-1 및 1 보다 큰 값은 1로 처리 됩니다.  
  
 STATUS_GRAPHIC 및 TREND_GRAPHIC은 클라이언트 응용 프로그램이 표시할 올바른 이미지 집합을 식별할 때 사용하는 문자열 값입니다. 이 문자열은 표시 함수의 동작도 정의합니다. 이 동작에는 표시할 상태 수(일반적으로 홀수)와 각 상태에 사용할 이미지가 포함됩니다.  
  
### <a name="kpi-graphics-in-sql-server-data-tools"></a>SQL Server Data Tools의 KPI 그래픽  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 KPI 그래픽은 세 가지 또는 다섯 가지 상태로 나타낼 수 있습니다. 다음 표에서 각 상태에 대 한 값을 정의합니다.  
  
|KPI 그래픽의 상태 수|상태 값|  
|--------------------------------------|---------------------------|  
|3|불량 = -1 ~ -0.5<br /><br /> 확인 하려면 0.4999-0.4999 =<br /><br /> 양호 = 0.50 ~ 1|  
|5|불량 = -1 ~ -0.75<br /><br /> 위험 = -0.7499 ~ -0.25<br /><br /> 보통 = -0.2499 ~ 0.2499<br /><br /> 향상 = 0.25 ~ 0.7499<br /><br /> 양호 = 0.75 ~ 1|  
  
> [!NOTE]  
>  역방향 계기 또는 역방향 상태 화살표와 같은 일부 그래픽에서는 범위가 반대로 됩니다. 즉, -1이 양호가 되고 1이 불량이 됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서는 KPI 그래픽의 이름으로 해당 그래픽의 상태가 3개인지 또는 5개인지 알 수 있습니다. 다음 표에서 사용, 이름 및 수가 나타내는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서 KPI 그래픽을 사용 하 여 연결 합니다.  
  
|그래픽 사용|KPI 그래픽 이름|상태 수|  
|--------------------|-------------------------|----------------------|  
|상태|셰이프|3|  
|상태|신호등|3|  
|상태|도로 표지|3|  
|상태|계기|3|  
|상태|역방향 계기|5|  
|상태|온도계|3|  
|상태|실린더|3|  
|상태|면|3|  
|상태|분산 화살표|3|  
|추세|일반 화살표|3|  
|추세|상태 화살표|3|  
|추세|역방향 상태 화살표|5|  
|추세|면|3|  
  
## <a name="see-also"></a>관련 항목  
 [DROP KPI 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-kpi.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
