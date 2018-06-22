---
title: 고급 모델링 (데이터 마이닝 추가 기능 Excel 용) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining structures, creating
ms.assetid: 042270a3-6ec7-4b52-b2ba-2adb6c4740d5
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: de7eea9099b458a9f16e6928c1535dc4a03eb81a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081966"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>고급 모델링(Excel용 데이터 마이닝 추가 기능)
  사용할 수는 **고급** 데이터 모델링 옵션을 사용자 지정 데이터 마이닝 구조 및 모델 매개 변수가 만들기 마법사에서 만든 속성과 다릅니다. 이 섹션에서 설명하는 두 가지 마법사를 사용하면 완전히 새로운 데이터 마이닝 구조 및 새로운 마이닝 모델을 만들어 기존 데이터 마이닝 구조에 적용할 수 있습니다.  
  
## <a name="create-mining-structure"></a>마이닝 구조 만들기  
 ![데이터 마이닝 리본, 마이닝 구조 만들기 단추](media/dmc-createstruct.gif "데이터 마이닝 리본, 마이닝 구조 만들기 단추")  
  
 **마이닝 구조 마법사** 새 데이터 마이닝 구조를 작성할 수 있도록 합니다. 구조는 지정된 데이터 원본에서 추출된 데이터의 컬렉션입니다.  원본의 새 데이터로 마이닝 구조를 업데이트할 수 있지만, 마이닝 구조를 만들 때 데이터가 분석에 사용되는 방법을 정의하는 데이터 형식과 이름을 정의합니다.  
  
 프로그램 구조를 작성 하는 다음 데이터 소스를 사용할 수 있습니다: Excel 테이블, Excel 범위 또는로 이미 정의 되어 있는 외부 데이터 원본에서 데이터는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 원본 뷰를 합니다.  
  
 각 구조에 대해 테스트 및 유효성 검사에 사용할 일부 데이터를 따로 설정하는 옵션이 있습니다. 이 만들어 *홀드 아웃 데이터 집합* 데이터 원본 연결을 설정할 때 구조를 기반으로 하는 모든 모델 테스트에 일관 된 데이터 집합을 사용할 수 있는지 확인할 수 있습니다.  
  
 마이닝 구조를 만든 후에는 여러 모델을 추가하여 서로 다른 분석 방법을 적용할 수 있습니다.  
  
 사용 하는 방법에 대 한 자세한 내용은 **마이닝 구조 만들기 마법사**, 참조 [Create Mining Structure &#40;SQL Server 데이터 마이닝 추가 기능&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)합니다.  
  
## <a name="add-model-to-structure"></a>구조에 모델 추가  
 ![모델을 구조 단추 추가](media/dmc-addmodel.gif "구조 단추에 모델 추가")  
  
 구조에 새 모델을 추가할 때 다른 알고리즘 또는 다른 매개 변수를 사용하여 데이터를 분석합니다. 이 옵션은 데이터 마이닝 클라이언트 도구에서는 표시되지 않는 알고리즘 중 하나를 사용하여 모델을 만들려는 경우 특히 유용합니다.  
  
 예를 들어, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 지원하는 다음과 같은 알고리즘을 사용할 수 있습니다.  
  
-   선형 회귀  
  
-   시퀀스 클러스터링  
  
-   중첩된 데이터 집합에 대한 연결 분석  
  
 마이닝 구조 종류를 확인 하려면를 사용할 수 있습니다를 찾아볼 수 모델 있으며 구조에 저장 된 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 중 하나를 클릭 하 여 **모델 관리** 또는 **찾아보기**합니다.  
  
 현재 세션 중 만든 데이터 마이닝 구조나 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 저장된 마이닝 구조로 제한됩니다.  
  
 자세한 내용은 참조 [구조에 모델 추가 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [모델 관리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [Excel에서 모델 찾아보기 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  