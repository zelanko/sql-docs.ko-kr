---
title: 선택 테이블 및 뷰 (데이터 원본 뷰 마법사) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.selecttablesandviews.f1
ms.assetid: ea7d1232-f213-46e9-90d9-0fd616ca003d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f4b940d5cb3c91cc8257ef1a3e6828286bc1c240
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069246"
---
# <a name="select-tables-and-views-data-source-view-wizard-analysis-services"></a>테이블 및 뷰 선택(데이터 원본 뷰 마법사)(Analysis Services)
  **테이블 및 뷰 선택** 페이지를 사용하여 데이터 원본 뷰에 포함시킬 데이터 원본의 테이블 또는 뷰를 선택할 수 있습니다.  
  
## <a name="options"></a>변수  
 **사용 가능한 개체**  
 데이터 원본 스키마의 테이블 및 뷰를 나열합니다. 두 개 이상의 스키마가 나열되는 경우 모든 개체의 이름 앞에 스키마 이름이 붙습니다. 스키마가 하나만 나열되는 경우 개체 이름 앞에 스키마의 이름이 붙지 않습니다.  
  
 목록을 오름차순이나 내림차순으로 다시 정렬하려면 **이름** 또는 **유형**을 클릭합니다.  
  
 **포함 된 개체**  
 데이터 원본 뷰에 포함시킬 테이블 및 뷰를 나열합니다.  
  
 목록을 오름차순이나 내림차순으로 다시 정렬하려면 **이름** 또는 **유형**을 클릭합니다.  
  
 **Assert**  
 **사용 가능한 개체**에 나열된 개체를 필터링합니다. 문자열을 입력한 다음 **필터** 를 클릭하여 지정한 문자열이 포함된 이름만 나열합니다. 입력한 문자열과 정확히 일치하는 개체를 찾으려면 해당 문자열을 큰따옴표로 묶습니다. 필터는 대/소문자를 구분하지 않습니다.  
  
 아래 표에 나열된 와일드카드 문자는 필터 문자열의 어느 위치에나 포함시킬 수 있습니다.  
  
|와일드카드 문자|값|  
|------------------------|-----------|  
|**\***|임의의 문자열|  
|**%**|임의의 문자열|  
|**?**|단일 문자|  
|**"** *string* **"**|리터럴 문자열. 이 와일드카드 문자가 개체 이름의 부분 문자열과 일치하는 경우 모두 나열됩니다.|  
  
 **시스템 개체 표시**  
 **사용 가능한 개체**에 시스템 개체를 표시합니다. 이 옵션은 데이터 원본 공급자가 시스템 개체를 표시하는 경우에만 사용할 수 있습니다. **포함된 개체** 목록에서 시스템 개체를 제거하면 이 옵션이 자동으로 선택됩니다.  
  
 **관련된 테이블 추가**  
 **포함된 개체**에 나열된 테이블과 관련된 모든 테이블을 추가합니다. 이 옵션을 통해 뷰는 추가할 수 없지만 분할된 테이블은 추가할 수 있습니다. 마법사의 **이름 일치** 페이지에서 이름 일치 조건을 선택한 경우에는 선택한 조건에 따라 논리적으로 관련된 테이블도 포함시킬 수 있습니다. 새로 추가된 관련 테이블과 관련되어 있고 원래 테이블과 구조가 동일한 테이블도 포함시킬 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 뷰 마법사 F1 도움말 &#40;Analysis Services&#41;](data-source-view-wizard-f1-help-analysis-services.md)   
 [다차원 모델의 데이터 원본 뷰](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
