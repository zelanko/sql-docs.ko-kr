---
title: 개체 명명 규칙 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f45ccaa0caab2e1dcc7e96e80e217d82d4f1f805
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "69530887"
---
# <a name="object-naming-rules-analysis-services"></a>개체 명명 규칙(Analysis Services)
  이 항목에서는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 코드 또는 스크립트, 개체 이름에 사용할 수 없는 예약어 및 문자뿐만 아니라 개체 명명 규칙에 대해 설명합니다.  
  
##  <a name="naming-conventions"></a><a name="bkmk_Names"></a>명명 규칙  
 모든 개체에는 부모 컬렉션의 범위 내에서 고유해야 하는 `Name` 및 `ID` 속성이 있습니다. 예를 들어 두 차원은 각각이 다른 데이터베이스에 상주하는 한 같은 이름을 가질 수 있습니다.  
  
 이름을 수동으로 지정할 수 있지만 `ID`는 개체를 만들 때 일반적으로 자동 생성됩니다. 모델을 만들었으면 `ID`를 변경해서는 안 됩니다. 모델 전반의 모든 개체 참조는 `ID`를 기반으로 합니다. 따라서 `ID`를 변경하면 모델이 쉽게 손상될 수 있습니다.  
  
 `DataSource` 및 `DataSourceView` 개체에는 명명 규칙에 대해 주목할 만한 예외가 있습니다. `DataSource` ID를 현재 데이터베이스에 대한 참조로 단일 점(.)으로 설정할 수 있지만 고유하지 않습니다. 두 번째 예외는 `DataSourceView`로, .NET Framework의 `DataSet` 개체에 정의된 명명 규칙을 준수합니다. 여기서 `Name`은 식별자로 사용됩니다.  
  
 다음은 `Name` 및 `ID` 속성에 적용되는 추가 규칙입니다.  
  
-   이름은 대/소문자를 구분하지 않습니다. 이름이 "sales"이 고 이름이 "Sales" 인 큐브를 같은 데이터베이스에 포함할 수 없습니다.  
  
-   이름 내에 공백을 포함할 수 있더라도 개체 이름에 선행 또는 후행 공백을 사용할 수 없습니다. 선행 공백과 후행 공백은 암시적으로 잘립니다. 이는 개체의 `Name` 및 `ID`에 모두 적용됩니다.  
  
-   최대 문자 수는 100자입니다.  
  
-   식별자의 첫 문자에는 특별한 요구 사항이 없습니다. 첫 문자는 모든 유효한 문자일 수 있습니다.  
  
##  <a name="reserved-words-and-characters"></a><a name="bkmk_reserved"></a>예약어 및 문자  
 예약어는 영어로 되어 있으며 캡션이 아닌 개체 이름에 적용됩니다. 개체 이름에 실수로 예약어를 사용하는 경우 유효성 검사 오류가 발생합니다. 다차원 및 데이터 마이닝 모델의 경우 아래에 명시된 예약어를 어떤 경우에도 개체 이름에 사용할 수 없습니다.  
  
 테이블 형식 모델의 경우 데이터베이스 호환성이 1103으로 설정되어 있고 특정 개체에 대해 유효성 검사 규칙이 해제되었으며 확장 문자 요구 사항 및 특정 클라이언트 애플리케이션 명명 규칙을 준수하지 않습니다. 이러한 조건을 충족하는 데이터베이스는 보다 덜 엄격한 유효성 검사 규칙을 따릅니다. 이 경우 개체 이름에 제한된 문자를 포함할 수 있으며 유효성 검사도 통과합니다.  
  
 **예약어**  
  
-   AUX  
  
-   CLOCK$  
  
-   COM1 - COM9(COM1, COM2, COM3 등)  
  
-   CON  
  
-   LPT1 - LPT9(LPT1, LPT2, LPT3 등)  
  
-   NUL  
  
-   PRN  
  
-   XML 내의 문자열에는 NULL 문자를 사용할 수 없습니다.  
  
 **예약 문자**  
  
 다음 표에서는 개체별로 유효하지 않은 문자열 보여 줍니다.  
  
|Object|잘못된 문자|  
|------------|------------------------|  
|`Server`|서버 개체 이름을 지정할 대 Windows 서버 명명 규칙을 따르십시오. 자세한 내용은 [명명 규칙(Windows)](/windows/desktop/DNS/naming-conventions) 을 참조하십시오.|  
|`DataSource`| `: / \ * \| ? " () [] {} <>` |  
|`Level` 또는 `Attribute`|````. , ; ' ` : / \ * & \| ? " & % $ ! + = [] {} < >````|  
|`Dimension` 또는 `Hierarchy`|````. , ; ' ` : / \ * \| ? " & % $ ! + = () [] {} <,>````|  
|기타 모든 개체|````. , ; ' ` : / \ * \| ? " & % $ ! + = () [] {} < >````|  
  
 **예외: 예약 문자가 허용되는 경우**  
  
 앞에서 설명한 것처럼 특정 형식 및 호환성 수준의 데이터베이스에는 예약 문자를 포함하는 개체 이름이 있을 수 있습니다. 차원 특성, 계층 구조, 수준, 측정값 및 KPI 개체 이름은 예약 문자를 포함할 수 있으며 확장 문자 사용이 허용되는 테이블 형식 데이터베이스(1103 이상)의 경우 다음과 같습니다.  
  
|서버 모드 및 데이터베이스 호환성 수준|예약 문자 허용 여부|  
|--------------------------------------------------|----------------------------------|  
|MOLAP(모든 버전)|아니요|  
|테이블 형식 - 1050|아니요|  
|테이블 형식 - 1100|아니요|  
|테이블 형식-1130 이상|예|  
  
 데이터베이스 기본 ModelType을 가질 수 있습니다. 기본값은 다차원과 같으므로 열 이름에 예약 문자를 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDX 예약어](/sql/mdx/mdx-reserved-words)   
 [번역 &#40;Analysis Services&#41;](/analysis-services/translation-support-in-analysis-services)   
 [XMLA&#41;&#40;XML for Analysis 준수](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
