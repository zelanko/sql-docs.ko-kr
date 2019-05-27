---
title: 테이블 및 뷰 선택 (데이터 피드) (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviewsdf.f1
ms.assetid: 6c4fafe0-e02e-47d1-b8bc-e70e872690af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82fcf08a84a06d33c33a520ce351f6c685092a15
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069277"
---
# <a name="select-tables-and-views-data-feeds-ssas"></a>테이블 및 뷰 선택(데이터 피드)(SSAS)
  **테이블 가져오기 마법사** 의 이 페이지에서는 가져올 데이터가 포함되어 있는 테이블과 뷰를 선택할 수 있습니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 마법사에 액세스하려면 **모델** 메뉴에서 **데이터 원본에서 가져오기**를 클릭합니다.  
  
 이 페이지에 테이블과 뷰가 표시되었다고 해서 가져오기 작업이 반드시 성공하는 것은 아닙니다. 가장 정보 페이지에 지정된 사용자에게 선택한 데이터베이스를 읽을 수 있는 권한이 없는 경우 가져오기 작업이 실패합니다.  
  
 Windows 인증을 사용하는 데이터 원본의 경우 현재 사용자의 자격 증명을 사용하여 테이블 및 뷰 선택 대화 상자에서 테이블 및 뷰를 가져옵니다. 기타 데이터 원본의 경우 연결 문자열에 제공된 자격 증명을 사용하여 데이터를 가져옵니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **데이터 피드 URL**  
 선택한 데이터 피드의 URL을 표시합니다.  
  
 **테이블 및 뷰**  
 데이터 피드의 테이블 및 뷰를 나열합니다. 가져올 각 테이블 및 뷰 옆의 확인란을 선택합니다.  
  
 **원본 테이블**  
 데이터 원본의 유형에 따라 원본 테이블의 이름을 지정합니다.  
  
 **이름**  
 원본 테이블의 이름을 지정합니다. 기본적으로 이 열에는 **원본 테이블** 열에 나타나는 원본 테이블의 이름이 표시됩니다.  
  
 **필터 세부 정보**  
 가져오고 있는 데이터에 필터가 적용된 경우 **필터 세부 정보** 대화 상자에 데이터 가져오기 필터를 표시합니다. 자세한 내용은 [필터 세부 정보&#40;SSAS&#41;](filter-details-ssas.md)를 참조하세요.  
  
 **미리 보기 및 필터**  
 가져오고 있는 데이터에 필터를 적용하는 데 사용되는 **선택한 테이블 미리 보기** 대화 상자를 표시합니다. 자세한 내용은 [선택한 테이블 미리 보기&#40;SSAS&#41;](preview-selected-table-ssas.md)를 참조하세요.  
  
 **관련된 테이블 선택**  
 선택한 테이블 및 뷰와 관련된 테이블을 선택합니다.  
  
  
