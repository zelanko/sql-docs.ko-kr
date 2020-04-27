---
title: 선택한 테이블 미리 보기 (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.previewselecttable.f1
ms.assetid: b6b34b5a-43b3-4a75-9f3b-b2ad1084b1b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0f168dabd237fe685eb90d2caeeba0db4eed97
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070717"
---
# <a name="preview-selected-table-ssas"></a>선택한 테이블 미리 보기(SSAS)
  **테이블 가져오기 마법사** 의 이 페이지에서는 선택된 테이블의 데이터를 미리 보고, 데이터 가져오기에 포함할 열을 선택하고, 선택된 열의 데이터를 필터링할 수 있습니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 마법사에 액세스하려면 **모델** 메뉴에서 **데이터 원본에서 가져오기**를 클릭합니다.  
  
 이 페이지에는 테이블의 행이 일부만 표시되지만, 사용자가 설정한 필터는 테이블을 가져올 때 해당 테이블의 모든 데이터에 적용됩니다.  
  
 Windows 인증을 사용하는 데이터 원본의 경우 현재 사용자의 자격 증명을 사용하여 미리 보기 및 필터 대화 상자에 표시된 데이터를 가져옵니다. 기타 데이터 원본의 경우 연결 문자열에 제공된 자격 증명을 사용하여 데이터를 가져옵니다.  
  
 이 페이지에 데이터가 표시되었다고 해서 가져오기 작업이 반드시 성공하는 것은 아닙니다. 가장 정보 페이지에 지정된 사용자 이름에 선택한 데이터베이스를 읽을 수 있는 권한이 없는 경우 가져오기 작업이 실패합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **열 머리글의 확인란**  
 데이터 가져오기에 열을 포함하려면 이 확인란을 선택하고, 데이터 가져오기에서 열을 제거하려면 이 확인란의 선택을 취소합니다.  
  
 **열 머리글의 아래쪽 화살표 단추**  
 열의 데이터를 필터링합니다.  
  
 **행 필터 지우기**  
 열의 데이터에 적용된 모든 필터를 제거합니다.  
  
  
