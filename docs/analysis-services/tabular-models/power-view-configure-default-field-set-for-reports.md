---
title: "Power View 보고서 (SSAS 테이블 형식)에 대 한 기본 필드 집합 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- ql12.asvs.bidtoolset.deffieldset.f1
ms.assetid: 6836b42f-28b8-4a98-a86d-2c3c109f0189
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc0a2fd4178189a072a9b194e502ae1c58de3f92
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="power-view---configure-default-field-set-for-reports"></a>Power View-보고서에 대 한 기본 필드 집합 구성
  기본 필드 집합은 보고서 필드 목록에서 테이블을 선택할 때 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서 캔버스에 자동으로 추가되는 미리 정의된 열 및 측정값 목록입니다. 테이블 형식 모델 작성자는 보고서에 모델을 사용하는 보고서 작성자를 위해 기본 필드 집합을 만들어 중복된 단계를 제거할 수 있습니다. 예를 들어, 고객 연락처 정보를 사용하는 대부분의 보고서 작성자가 항상 연락처 이름, 기본 전화 번호, 전자 메일 주소 및 회사 이름을 보려고 하는 것으로 파악되는 경우 해당 열을 미리 선택하여 작성자가 Customer Contact 테이블을 클릭할 때 보고서 캔버스에 이러한 정보가 항상 추가되도록 할 수 있습니다.  
  
> [!NOTE]  
>  기본 필드 집합은 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]에서 데이터 모델로 사용되는 테이블 형식 모델에만 적용됩니다. Excel 피벗 보고서에서는 기본 필드 집합이 지원되지 않습니다.  
  
## <a name="creating-a-default-field-set"></a>기본 필드 집합 만들기  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]에서 특정 테이블이 선택될 때마다 기본적으로 포함되는 필드를 결정할 수 있습니다. 목록에 필드가 나타나는 순서도 결정할 수 있습니다. 기본 필드 집합을 지정하려면 테이블 형식 모델 프로젝트에서 보고서 속성을 설정합니다.  
  
#### <a name="to-add-a-default-field-set"></a>기본 필드 집합을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 기본 필드 목록을 구성 중인 테이블(탭)을 클릭합니다.  
  
2.  **속성** 창의 **기본 필드 집합** 속성에서 **편집하려면 클릭**을 클릭합니다.  
  
3.  기본 필드 집합 대화 상자에서 필드를 하나 이상 선택합니다. 측정값을 비롯하여 테이블의 모든 필드를 선택할 수 있습니다. Shift 키를 누른 채 범위를 선택하거나 Ctrl 키를 누른 채 개별 필드를 선택합니다.  
  
4.  **추가** 를 클릭하여 선택한 필드를 기본 필드 집합에 추가합니다.  
  
5.  위쪽 및 아래쪽 단추를 사용하여 필드 목록의 필드 순서를 지정합니다. 필드 집합에 대해 정의된 순서로 필드가 보고서에 추가됩니다.  
  
6.  통합 문서의 다른 테이블에 대해 이러한 단계를 반복합니다.  
  
## <a name="next-step"></a>다음 단계  
 기본 필드 집합을 만든 후에는 기본 레이블, 기본 이미지, 기본 그룹 동작 또는 같은 값의 여러 행이 한 행에 함께 그룹화되는지 아니면 따로 나열되는지 지정하여 보고서 디자인 환경을 더 자세히 사용자 지정합니다. 자세한 내용은 [파워 뷰 보고서의 테이블 동작 속성 구성&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/power-view-configure-table-behavior-properties-for-reports.md)을 참조하세요.  
  
  

