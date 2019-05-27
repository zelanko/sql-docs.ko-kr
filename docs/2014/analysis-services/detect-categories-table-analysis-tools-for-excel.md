---
title: 검색 범주 (Excel 용 테이블 분석 도구) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- clustering [data mining]
- mining model, decision tree
- category detection
ms.assetid: 3c7e9ebb-d0c9-498e-a9ba-cc13eaa43520
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06c466eb5e3275818a710a9f9d90c705ed93c957
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081863"
---
# <a name="detect-categories-table-analysis-tools-for-excel"></a>범주 검색(Excel용 테이블 분석 도구)
  ![리본 메뉴에서 검색 범주 단추](media/tat-detectcat.gif "리본의 범주 검색 단추")  
  
 합니다 **범주 검색** 도구 비슷한 특징이 있는 테이블의 행을 자동으로 검색 합니다.  
  
 도구를 완료하면 검색한 범주 및 구별되는 특성을 함께 나열한 보고서가 생성됩니다. 기본적으로 도구는 각 데이터 행에 대해 제안된 범주가 포함된 데이터 테이블에 새 열을 추가합니다. 사용자는 범주를 검토하고 이름을 바꿀 수 있습니다.  
  
## <a name="using-the-detect-categories-tool"></a>범주 검색 도구 사용  
  
1.  Excel 테이블을 엽니다.  
  
2.  클릭 **범주 검색**합니다.  
  
3.  분석에 사용할 열을 지정합니다. 개인 이름이나 레코드 ID와 같은 고유 값을 포함한 열은 분석에 유용하지 않을 수 있으므로 선택을 취소할 수 있습니다.  
  
4.  필요에 따라 생성할 범주의 최대 개수를 지정합니다. 기본적으로 도구는 자동으로 검색한 수만큼 범주를 만듭니다.  
  
5.  **실행**을 클릭합니다.  
  
6.  이 도구는 범주 보고서로 명명된 범주 목록과 특성을 포함하는 새 워크시트를 만듭니다.  
  
 도구에 대 한 옵션을 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [범주 검색 대화 상자 (Excel 용 테이블 분석 도구)](detect-categories-table-analysis-tools-for-excel.md)합니다.  
  
## <a name="understanding-the-categories-report"></a>범주 보고서 이해  
 합니다 **범주 보고서** 두 테이블이 **범주 목록** 및 **범주 특징**, 및 **범주 프로필** 차트입니다.  
  
### <a name="category-list"></a>범주 목록  
 첫 번째 테이블에는 발견된 범주가 나열됩니다. 합니다 **행 개수** 열 각 범주에 할당 된 데이터의 행 수를 나타냅니다.  
  
 모델은 각 범주에 대 한 임시 이름을 만들지만 수 만큼 범주 이름을 바꿀 수 있습니다. 예를 들어, 다음 예에서 첫 번째 범주 바뀌었습니다 **Low Income**이기 때문입니다 클러스터의 가장 중요 한 특성입니다.  
  
 ![범주 검색 도구로 만든 보고서](media/dm13-tat-detectcat-report1.gif "범주 검색 도구로 만든 보고서")  
  
 새 레이블을 입력하자마자 변경된 레이블이 다른 모든 차트와 원본 데이터 워크시트에서 추가된 범주 목록으로 전파됩니다.  
  
### <a name="category-characteristics"></a>범주 특징  
 두 번째 테이블인 **범주 특징**는 각 범주 구성에 대 한 세부 정보가 표시 됩니다. 클릭 합니다 **필터** 맨 위에 있는 단추를 **범주** 열을 한 개 이상의 범주에 포커스를 확인 합니다.  
  
 ![범주 검색 도구로 만든 보고서](media/dm13-tat-detectcat-report2.gif "범주 검색 도구로 만든 보고서")  
  
 열에서 음영 **상대적 중요도**, 나타냅니다 구별 요소로 서은 해당 특성 및 값의 조합이 중요 합니다. 표시줄이 길수록 이 특성이 이 범주를 대표할 가능성이 높아집니다.  
  
### <a name="categories-profile-chart"></a>범주 프로필 차트  
 최종 차트인 합니다 **범주 보고서** 워크시트 **범주 프로필**에 대화형 **피벗 차트** 다시 정렬 하 고 필드를 숨기 거 나 값에 필터링에 사용할 수 있습니다 및 차트의 모양을 사용자 지정 합니다.  
  
 Excel 2013에서 이제 제공 **차트 스타일** 하 고 **차트 요소** 오른쪽 차트 디자인을 개선할 수 있도록 하는 디자인 화면에서 제어 합니다.  
  
 ![범주 검색 도구로 만든 보고서](media/dm13-tat-detectcat-report3.gif "범주 검색 도구로 만든 보고서")  
  
## <a name="requirements"></a>요구 사항  
 합니다 **범주 검색** 도구에 양 또는 데이터 형식에 대 한 요구 사항이 없습니다.  
  
> [!NOTE]  
>  사용 하는 경우는 **범주 검색** 도구를 만들면 새 열을 범주, 원래 데이터 테이블에 있습니다. 이 열을 데이터 테이블에 남겨두고 후속 데이터 마이닝 작업을 수행할 경우 이 열이 결과에 영향을 줄 수 있습니다. 이 열이 다른 작업에 영향을 주지 않도록 하려면 다른 데이터 마이닝 도구를 사용하기 전에 범주 열이 없는 데이터 테이블의 복사본을 만들어야 합니다.  
  
## <a name="related-tools"></a>관련 도구  
 경우는 **범주 검색** 도구는 데이터를 사용 하 여 데이터 마이닝 구조 및 데이터 마이닝 모델을 만들면는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터링 알고리즘입니다.  
  
 사용 하 여 데이터 마이닝 모델을 만든 후 합니다 **주요 영향 요인 분석** 도구인 모델을 탐색 하 고 관계를 자세하게 Excel 용 데이터 마이닝 클라이언트를 사용할 수 있습니다. Excel용 데이터 마이닝 클라이언트는 고급 데이터 마이닝 기능을 제공하는 별도의 추가 기능입니다. 정보를 참조 하세요 [Excel에서 모델 찾아보기 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)합니다.  
  
 Excel 용 데이터 마이닝 클라이언트의 기능을 모델링 하는 데이터를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [데이터 마이닝 모델을 만드는](creating-a-data-mining-model.md)합니다.  
  
 사용 되는 알고리즘에 대 한 자세한 내용은 합니다 **범주 검색** 도구에서 "Microsoft 클러스터링 알고리즘" 항목을 참조 하십시오 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목  
 [Excel용 테이블 분석 도구](table-analysis-tools-for-excel.md)  
  
  
