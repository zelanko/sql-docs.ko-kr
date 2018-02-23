---
title: "테이블 속성 | Microsoft Docs"
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.tableprop.f1
ms.assetid: 16d3347b-7e43-4a6b-9956-fdd6ede092e6
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 202902448a31fda27ab2c4d8c0bc894cc50da3db
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="table-properties"></a>Table Properties 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
이 문서에서는 테이블 형식 모델 테이블 속성을 설명 합니다. 여기에서 설명하는 테이블 속성은 원본에서 가져올 열을 지정할 수 있도록 하는 테이블 속성 편집 대화 상자의 테이블 속성과는 다릅니다.  
  
 이 항목의 섹션:  
  
-   [테이블 속성](#bkmk_properties)  
  
-   [테이블 속성 설정 구성](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> 테이블 속성  
 **Basic**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**연결 이름**|\<연결 이름 >|테이블의 데이터 원본에 대한 연결의 이름입니다.<br /><br /> 연결을 편집하려면 단추를 클릭합니다.|  
|**숨김**|False|보고 클라이언트 필드 목록에서 테이블이 숨겨지는지 여부를 지정합니다.|  
|**파티션**||**속성** 창에 표시될 수 없는 테이블의 파티션입니다. 파티션을 보거나 만들거나 편집하려면 단추를 클릭하여 파티션 관리자를 엽니다.|  
|**원본 데이터**||**속성** 창에 표시될 수 없는 테이블의 원본 데이터입니다. 원본 데이터를 보거나 편집하려면 단추를 클릭하여 테이블 속성 편집 대화 상자를 엽니다.|  
|**테이블 속성 설명**||테이블에 대한 텍스트 설명입니다.<br /><br /> [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]에서 최종 사용자가 필드 목록의 이 테이블 위에 커서를 두면 설명이 도구 설명으로 나타납니다.|  
|**테이블 이름**|\<식별 이름 >|테이블의 이름을 지정합니다. 테이블 이름은 테이블 가져오기 마법사를 사용하여 테이블을 가져올 때 지정하거나 테이블을 가져온 후 언제든지 지정할 수 있습니다. 모델의 테이블 이름을 관련된 원본 테이블 이름과 다르게 지정할 수 있습니다. 테이블 이름은 보고 클라이언트 응용 프로그램 필드 목록과 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 모델 데이터베이스에 나타납니다.|  
  
 **보고 속성**  
  
 자세한 설명 및 속성을 보고에 대 한 구성 정보에 대 한 참조 [Power View 보고 속성](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)합니다.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**기본 필드 집합**|||  
|테이블 동작|||  
  
##  <a name="bkmk_config_prop"></a> 테이블 속성 설정 구성  
  
1.  모델 디자이너의 데이터 뷰에서 테이블(탭)을 클릭하거나 다이어그램 뷰에서 테이블 머리글을 클릭합니다.  
  
2.  **속성** 창에서 속성을 클릭한 다음 값을 입력하거나 추가 구성 옵션을 표시하는 단추를 클릭합니다.  
  
  
