---
title: 반 가산적 동작 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- semiadditive
- Business Intelligence enhancements [Analysis Services], semiadditive behavior
- measures [Analysis Services], semiadditive
ms.assetid: b25726bc-728b-4601-ad87-9015c39dc615
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84b5d71a14c08c47d630ed834ef0a6e436b52edd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190273"
---
# <a name="define-semiadditive-behavior"></a>반가산적 동작 정의
  다양한 비즈니스 시나리오에서 모든 차원에 대해 균일하게 집계되지 않는 반가산적 측정값이 있는 경우가 많습니다. 시간에 따른 균형에 대한 스냅숏을 기반으로 하는 모든 큐브에서 이 문제가 발생합니다. 보안, 잔액, 예산, 인력 관리, 보험 정책, 지불 청구 및 기타 비즈니스 분야를 처리하는 애플리케이션에서 이러한 스냅숏을 찾을 수 있습니다.  
  
 큐브에 반가산적 동작을 추가하여 개별 측정값이나 해당 계정 유형 특성의 멤버에 대한 집계 방법을 정의합니다. 큐브에 계정 차원이 포함되는 경우 해당 계정 유형 기반의 반가산적 동작을 자동으로 설정할 수 있습니다.  
  
 반가산적 동작을 추가하려면 큐브 디자이너에서 큐브를 열고 큐브 메뉴에서 **비즈니스 인텔리전스 추가** 를 선택합니다. 비즈니스 인텔리전스 마법사의 **기능 선택** 페이지에서 **반가산적 동작 정의** 옵션을 선택합니다. 그런 다음 마법사의 안내를 따라 반가산적 동작이 있는 측정값을 식별합니다.  
  
 표준 버전에서 제공되는 LastChild를 제외하고, 반가산적 동작은 비즈니스 인텔리전스 또는 엔터프라이즈 버전에서만 사용할 수 있습니다.  
  
## <a name="define-semiadditive-behavior"></a>반가산적 동작 정의  
 마법사의 **반가산적 동작 정의** 페이지에서 다음 옵션 중 하나를 선택하여 반가산성을 정의하는 방법을 선택합니다.  
  
 **반가산적 동작 해제**  
 이전에 반가산적 동작이 정의된 큐브에서 반가산적 동작을 제거합니다. 이 옵션을이 선택 하면 측정값이 다시 설정 `SUM` 다음 집계 함수 유형 중 하나에 설정 된 경우:  
  
-   By Account  
  
-   Average of Children  
  
-   First Child  
  
-   Last Child  
  
-   Last Nonempty Child  
  
-   First Nonempty Child  
  
-   없음  
  
 이 옵션은 일반 집계 함수로 측정값을 변경 되지 않습니다: `Sum`, `Min`를 `Max`, `Count`, 또는 `Distinct``Count`합니다.  
  
 **마법사에서 반가산적 멤버가 포함된 'Account' 계정 차원을 검색했습니다. 서버는 각 계정 유형에 지정 된 반 가산적 동작에 따라이 차원의 멤버를 집계 합니다.**  
 시스템에서 계정 유형 차원별로 차원이 구분된 측정값 그룹의 모든 측정값을 By Account 집계 함수로 설정하도록 하며 서버는 각 계정 유형에 지정된 반가산적 동작에 따라 차원의 멤버를 집계합니다.  
  
> [!NOTE]  
>  마법사에서 계정 유형 차원을 찾은 경우 이 옵션이 기본적으로 선택됩니다.  
  
 **개별 측정값에 대한 반가산적 동작 정의**  
 각 측정값의 반가산적 동작을 개별적으로 선택합니다. 기본 설정은 `SUM` (완전 가산적)입니다.  
  
> [!NOTE]  
>  마법사에서 계정 유형 차원을 찾지 못한 경우 이 옵션이 기본적으로 선택됩니다.  
  
 각 측정값에 대해 다음 표에서 설명하는 유형의 반가산적 함수를 선택할 수 있습니다.  
  
|반가산적 함수|Description|  
|---------------------------|-----------------|  
|Average of Children|멤버 자식의 평균을 집계합니다.|  
|ByAccount|시스템에서 계정 유형에 지정된 반가산적 동작을 읽습니다.|  
|개수|멤버 개수를 집계합니다.|  
|Distinct Count|고유 멤버의 개수를 집계합니다.|  
|First Child|멤버 값이 시간 차원에 따른 첫 번째 자식의 값으로 계산됩니다.|  
|FirstNonEmpty|멤버 값이 시간 차원에 따른 데이터를 포함하는 첫 번째 자식의 값으로 계산됩니다.|  
|LastChild|멤버 값이 시간 차원에 따른 마지막 자식의 값으로 계산됩니다.|  
|LastNonEmpty|멤버 값이 시간 차원에 따른 데이터를 포함하는 마지막 자식의 값으로 계산됩니다.|  
|최대값|표준 최대 집계 함수가 적용됩니다.|  
|최소값|표준 최소 집계 함수가 적용됩니다.|  
|없음|집계가 적용되지 않습니다.|  
|SUM|표준 합계 함수가 적용됩니다.|  
  
 마법사를 완료하면 기존의 모든 반가산적 동작을 덮어씁니다.  
  
  
