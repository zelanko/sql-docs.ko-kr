---
title: '9단원: 큐브 뷰 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd395e605bfde9d34ed0dc4f16060812464efb56
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078247"
---
# <a name="lesson-9-create-perspectives"></a>9단원: 큐브 뷰 만들기
  이 단원에서는 Internet Sales 큐브 뷰를 만듭니다. 큐브 뷰는 비즈니스 또는 애플리케이션 중심의 관점에서 파악할 수 있게 해 주는 보기 가능한 모델 하위 집합을 정의합니다. 사용자가 큐브 뷰를 사용하여 모델에 연결하는 경우 해당 모델 개체(테이블, 열, 측정값, 계층 및 KPI)만 해당 큐브 뷰에 정의되어 있는 필드로 볼 수 있습니다.  
  
 이 단원에서 만드는 Internet Sales 큐브 뷰에는 Customer 테이블 개체가 제외됩니다. 뷰에서 특정 개체를 제외하는 큐브 뷰를 만들면 해당 개체가 모델에는 그대로 있지만 보고 클라이언트 필드 목록에서는 보이지 않습니다. 큐브 뷰에 포함되어 있거나 포함되어 있지 않은 계산 열 및 측정값을 계속해서 제외된 개체 데이터에서 계산할 수 있습니다.  
  
 이 단원의 목표는 큐브 뷰를 만드는 방법을 설명하고 테이블 형식 모델 제작 도구를 파악하도록 돕는 데 있습니다. 나중에 추가 테이블을 포함하도록 이 모델을 확장할 경우 큐브 뷰를 추가로 만들어 모델에 대한 다양한 뷰포인트(예: Inventory 및 Sales Force)를 정의할 수 있습니다.  
  
 자세한 내용은 [큐브 뷰&#40;SSAS 테이블 형식&#41;](tabular-models/perspectives-ssas-tabular.md)를 참조하세요.  
  
 예상이 단원을 완료 시간: **5 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [8단원: 핵심 성과 지표 만들기](lesson-7-create-key-performance-indicators.md)합니다.  
  
## <a name="create-perspectives"></a>큐브 뷰 만들기  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Internet Sales 큐브 뷰를 만들려면  
  
1.  모델 디자이너에서를 클릭 합니다 **모델** 메뉴를 클릭 한 다음 **큐브 뷰**합니다.  
  
2.  **큐브 뷰** 대화 상자에서 **새 큐브 뷰**를 클릭합니다.  
  
3.  큐브 뷰의 이름을 바꾸려면 두 번 클릭 하 여 **새 큐브 뷰 1** 열 머리글을 입력 한 다음 `Internet Sales`합니다.  
  
4.  **필드**, 다음 테이블을 선택 **날짜**를 **Geography**, **제품**, **Product Category**하십시오 **product Subcategory**, 및 `Internet Sales`합니다.  
  
     이 큐브 뷰에서 Customer 테이블과 이 테이블의 모든 열을 제외했습니다. 나중에 12단원에서 Excel에서 분석 기능을 사용하여 이 큐브 뷰를 테스트합니다. Excel 피벗 테이블 필드 목록에는 Customer 테이블을 제외한 각 테이블이 포함됩니다.  
  
5.  선택 항목을 확인하여 **Customer** 테이블이 선택되어 있지 않은지 확인한 다음 **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 자습서를 계속 하려면 다음 단원으로 이동 합니다. [10 단원: 계층 구조를 만들](lesson-9-create-hierarchies.md)합니다.  
  
  
