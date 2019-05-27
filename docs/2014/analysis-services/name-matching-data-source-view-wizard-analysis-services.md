---
title: 이름 일치 (데이터 원본 뷰 마법사) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.namematchingcriteria.f1
ms.assetid: 7f811e02-0fe6-45c9-a7b7-29c61032d96b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 866bdea710033a0cfa3bdadb34282c96c810d730
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072402"
---
# <a name="name-matching-data-source-view-wizard-analysis-services"></a>이름 일치(데이터 원본 뷰 마법사)(Analysis Services)
  **이름 일치** 페이지를 사용하여 스키마의 데이터 원본 뷰에 대해 선택한 테이블과 해당 스키마의 다른 테이블 간의 관계를 감지하는 데 사용할 조건을 선택할 수 있습니다. 테이블 간에 물리적 외래 키 관계가 없으면 이 기준이 관련 테이블을 식별하고 데이터 원본 뷰에 추가하는 데 도움이 됩니다. 이름 일치로 식별된 논리적 관계도 데이터 원본 뷰에 추가됩니다.  
  
> [!NOTE]  
>  여러 테이블이 있지만 테이블 간에 외래 키 관계가 없는 데이터 원본을 선택하는 경우에만 이 페이지가 표시됩니다.  
  
## <a name="options"></a>변수  
 **일치 하는 열에서 논리적 관계 만들기**  
 이름 일치 조건을 사용하여 스키마의 데이터 원본 뷰에 대해 선택한 테이블과 해당 스키마의 다른 테이블 간의 논리적 종속성 및 관계를 감지하려면 선택합니다. 이 확인란 선택을 취소하면 데이터 원본의 테이블 간에 논리적 관계를 식별하는 데 이름 일치 조건을 사용하지 않습니다.  
  
 **외래 키 일치**  
 데이터 원본의 테이블과 뷰 간에 논리적 관계를 만드는 데 사용할 기준을 선택합니다. 영숫자 이외의 문자는 일치 문자열에서 무시됩니다. 예를 들어 "Customer ID", "Customer_ID", "CustomerID"는 모두 일치합니다. 지정한 조건으로 관계를 만들려면 다음 표의 옵션 중 하나를 선택합니다.  
  
|선택|만들 관계|  
|------------|---------------|  
|**기본 키와 같은 이름**|열 이름이 선택한 테이블의 기본 키 열 이름과 같은 테이블에 대한 논리적 관계|  
|**대상 테이블 이름과 같은 이름**|열 이름이 선택한 테이블의 이름과 일치하는 테이블에 대한 논리적 관계|  
|**대상 테이블 이름 + 기본 키 이름**|열 이름이 선택한 테이블 이름과 선택한 테이블에 대한 기본 키 열 이름이 이 순서대로 연결되는 이름과 일치하는 테이블에 대한 논리적 관계. 이 연결에서 영숫자 이외의 문자는 무시됩니다. 예를 들어 "Product ID", "Product_ID" 및 "ProductID"는 모두 일치합니다.|  
  
 **설명 및 샘플**  
 선택한 조건에 대한 설명과 샘플을 표시합니다.  
  
  
