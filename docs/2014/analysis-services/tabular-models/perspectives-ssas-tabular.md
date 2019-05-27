---
title: 큐브 뷰 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1f78c3a1-ce2c-4e7f-a277-71a657692bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fcd6e438327d88b79a88b5026f28e24e19fffb5e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66066875"
---
# <a name="perspectives-ssas-tabular"></a>큐브 뷰(SSAS 테이블 형식)
  테이블 형식 모델에서 큐브 뷰는 모델의 보기 가능한 하위 집합을 정의하는데, 이를 통해 모델을 집중해서 보거나 비즈니스 또는 애플리케이션의 관점에서 파악할 수 있습니다.  
  
 이 항목의 섹션:  
  
-   [이점](#bkmk_understanding)  
  
-   [큐브 뷰 테스트](#bkmk_testpersp)  
  
-   [관련 작업](#bkmk_related_tasks)  
  
##  <a name="bkmk_understanding"></a> 이점  
 테이블 형식 모델은 너무 복잡해서 사용자가 탐색하기 어려울 수 있습니다. 단일 모델이 여러 개의 테이블, 측정값 및 차원을 포함하는 전체 데이터 웨어하우스의 내용을 나타낼 수 있습니다. 이러한 복잡성은 주로 비즈니스 인텔리전스 및 보고 요구 사항을 충족하기 위해 모델의 일부만 사용하는 사용자에게는 부담이 될 수 있습니다.  
  
 큐브 뷰에서 테이블, 열 및 측정값(KPI 포함)은 필드 개체로 정의됩니다. 각 큐브 뷰에 대해 보기 가능한 필드를 선택할 수 있습니다. 예를 들어 단일 모델에 제품, 판매, 재무, 직원 및 지리 데이터가 포함되어 있는데, 영업부에는 제품, 판매, 홍보 및 지리 데이터가 필요한 반면 직원 및 재무 데이터는 필요하지 않을 수 있습니다. 마찬가지로 인사부에는 판매 홍보 및 지리 데이터가 필요하지 않습니다.  
  
 정의된 큐브 뷰가 있는 모델(데이터 원본)에 연결하는 경우 사용자는 사용할 큐브 뷰를 선택할 수 있습니다. 예를 들어 Excel의 모델 데이터 원본에 연결할 경우 인사부의 사용자는 데이터 연결 마법사의 테이블 및 뷰 선택 페이지에서 인적 자원 큐브 뷰를 선택할 수 있습니다. 이 경우 인적 자원 큐브 뷰에 대해 정의된 필드(테이블, 열 및 측정값)만 피벗 테이블 필드 목록에 표시됩니다.  
  
 큐브 뷰는 보안 수단이 아니라 더 나은 사용자 환경을 제공하기 위한 도구입니다. 특정 큐브 뷰에 대한 모든 보안은 기본 모델에서 상속됩니다. 큐브 뷰에서 사용자에게 액세스 권한이 없는 모델 개체에 대한 액세스 권한을 부여할 수는 없습니다. 큐브 뷰를 통해 모델의 개체에 대한 액세스를 제공하려면 먼저 model 데이터베이스에 대한 보안을 해결해야 합니다. 보안 역할을 사용하여 모델 메타데이터 및 데이터에 보안을 설정할 수 있습니다. 자세한 내용은 [역할&#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)을 참조하세요.  
  
##  <a name="bkmk_testpersp"></a> 큐브 뷰 테스트  
 모델 제작 시 모델 디자이너의 Excel에서 분석 기능을 사용하여 정의한 큐브 뷰의 효율성을 테스트할 수 있습니다. 모델 디자이너의 **모델** 메뉴에서 **Excel에서 분석**을 클릭하면 Excel이 열리기 전에 **자격 증명 및 큐브 뷰 선택** 대화 상자가 나타납니다. 이 대화 상자에서 현재 사용자 이름, 다른 사용자, 역할, 그리고 데이터 원본 및 뷰 데이터로 모델 작업 영역 데이터베이스에 연결하는 데 사용할 큐브 뷰를 지정할 수 있습니다.  
  
##  <a name="bkmk_related_tasks"></a> 관련 태스크  
  
|항목|Description|  
|-----------|-----------------|  
|[큐브 뷰 만들기 및 관리&#40;SSAS 테이블 형식&#41;](perspectives-ssas-tabular.md)|모델 디자이너의 큐브 뷰 대화 상자를 사용하여 큐브 뷰를 만들고 관리하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [역할&#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)   
 [계층 구조&#40;SSAS 테이블 형식&#41;](hierarchies-ssas-tabular.md)  
  
  
