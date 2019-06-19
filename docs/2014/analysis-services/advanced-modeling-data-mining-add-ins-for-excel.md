---
title: 고급 모델링 (데이터 마이닝 추가 기능 Excel 용) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures, creating
ms.assetid: 042270a3-6ec7-4b52-b2ba-2adb6c4740d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 669fa1fcd9e4802a4d4102120a373dd615741017
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062743"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>고급 모델링(Excel용 데이터 마이닝 추가 기능)
  사용할 수는 **고급** 데이터 만드는 옵션을 사용자 지정 데이터 마이닝 구조 및 모델 매개 변수를 사용 하 여 마법사에서 만든 것과 다른 모델링 합니다. 이 섹션에서 설명하는 두 가지 마법사를 사용하면 완전히 새로운 데이터 마이닝 구조 및 새로운 마이닝 모델을 만들어 기존 데이터 마이닝 구조에 적용할 수 있습니다.  
  
## <a name="create-mining-structure"></a>마이닝 구조 만들기  
 ![Create Mining Structure 단추, 데이터 마이닝 리본의](media/dmc-createstruct.gif "Create Mining Structure 단추, 데이터 마이닝 리본 메뉴")  
  
 합니다 **마이닝 구조 만들기 마법사** 새 데이터 마이닝 구조를 작성할 수 있습니다. 구조는 지정된 데이터 원본에서 추출된 데이터의 컬렉션입니다.  원본의 새 데이터로 마이닝 구조를 업데이트할 수 있지만, 마이닝 구조를 만들 때 데이터가 분석에 사용되는 방법을 정의하는 데이터 형식과 이름을 정의합니다.  
  
 다음 데이터 원본을 사용 하 여 뷰로: Excel 테이블, Excel 범위 또는 이미 정의 된 외부 데이터 원본에 데이터를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 원본 뷰.  
  
 각 구조에 대해 테스트 및 유효성 검사에 사용할 일부 데이터를 따로 설정하는 옵션이 있습니다. 이 만들어 *홀드 아웃 데이터 집합* 데이터 원본을 설정할 때 확인할 수 있습니다는 구조를 기반으로 하는 모든 모델 테스트에 일관 된 데이터 집합을 사용할 수 있습니다.  
  
 마이닝 구조를 만든 후에는 여러 모델을 추가하여 서로 다른 분석 방법을 적용할 수 있습니다.  
  
 사용 하는 방법에 대 한 자세한 합니다 **마이닝 구조 만들기 마법사**를 참조 하세요 [Create Mining Structure &#40;SQL Server 데이터 마이닝 추가 기능&#41;](create-mining-structure-sql-server-data-mining-add-ins.md).  
  
## <a name="add-model-to-structure"></a>구조에 모델 추가  
 ![모델 구조 단추 추가](media/dmc-addmodel.gif "구조 단추에 모델 추가")  
  
 구조에 새 모델을 추가할 때 다른 알고리즘 또는 다른 매개 변수를 사용하여 데이터를 분석합니다. 이 옵션은 데이터 마이닝 클라이언트 도구에서는 표시되지 않는 알고리즘 중 하나를 사용하여 모델을 만들려는 경우 특히 유용합니다.  
  
 예를 들어, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 지원하는 다음과 같은 알고리즘을 사용할 수 있습니다.  
  
-   선형 회귀  
  
-   시퀀스 클러스터링  
  
-   중첩된 데이터 집합에 대한 연결 분석  
  
 종류의 마이닝 구조에 확인을 사용할 수를 찾아볼 수 모델 있으며 구조에 저장 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 중 하나를 클릭 하 여 **모델 관리** 하거나 **찾아보기**합니다.  
  
 현재 세션 중 만든 데이터 마이닝 구조나 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 저장된 마이닝 구조로 제한됩니다.  
  
 자세한 내용은 [구조에 모델 추가 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [모델 관리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [Excel에서 모델 찾아보기 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
