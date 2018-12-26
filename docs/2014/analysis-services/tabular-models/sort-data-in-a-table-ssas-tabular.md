---
title: 테이블 (SSAS 테이블 형식)의 데이터 정렬 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5fa6ad56-bf68-4aac-a226-52556173b7e2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4fd42458d59f7d591bf7de8279e983e30f754164
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48081853"
---
# <a name="sort-data-in-a-table-ssas-tabular"></a>테이블의 데이터 정렬(SSAS 테이블 형식)
  하나 이상의 열에 있는 데이터를 텍스트 및 숫자별로 오름차순 또는 내림차순으로 정렬할 수 있습니다.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-text-column"></a>텍스트 열을 기준으로 테이블의 데이터를 정렬하려면  
  
1.  모델 디자이너에서 영숫자 데이터 열의 셀 범위를 선택하거나 활성 셀이 영숫자 데이터를 포함하는 테이블 열에 있는지 확인합니다. 그런 다음 필터링하려는 열의 머리글에 있는 화살표를 클릭합니다.  
  
2.  자동 필터 메뉴에서 다음 중 하나를 수행합니다.  
  
    -   오름차순 영숫자 순서로 정렬하려면 **텍스트 오름차순 정렬**을 클릭합니다.  
  
    -   내림차순 영숫자 순서로 정렬하려면 **텍스트 내림차순 정렬**을 클릭합니다.  
  
    > [!NOTE]  
    >  다른 애플리케이션에서 가져온 데이터의 경우 데이터 앞에 선행 공백이 삽입되어 있을 수 있습니다. 데이터를 제대로 정렬하려면 선행 공백을 제거해야 합니다.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-numeric-column"></a>숫자 열을 기준으로 테이블의 데이터를 정렬하려면  
  
1.  모델 디자이너에서 영숫자 데이터 열의 셀 범위를 선택하거나 활성 셀이 영숫자 데이터를 포함하는 테이블 열에 있는지 확인합니다. 그런 다음 필터링하려는 열의 머리글에 있는 화살표를 클릭합니다.  
  
2.  자동 필터 메뉴에서 다음 중 하나를 수행합니다.  
  
    -   가장 작은 숫자에서 가장 큰 숫자 순서로 정렬하려면 **숫자 오름차순 정렬**을 클릭합니다.  
  
    -   가장 큰 숫자에서 가장 작은 숫자 순서로 정렬하려면 **숫자 내림차순 정렬**을 클릭합니다.  
  
    > [!NOTE]  
    >  결과가 예상과 다른 경우 열에 숫자가 아니라 텍스트로 저장된 숫자가 포함되어 있을 수 있습니다. 예를 들어 일부 재무 회계 시스템에서 가져온 음수 또는 '(아포스트로피)와 함께 입력한 숫자는 텍스트로 저장됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 필터링 및 정렬 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../filter-and-sort-data-ssas-tabular.md)   
 [큐브 뷰 &#40;&AMP;#40;SSAS 테이블 형식&#41;](perspectives-ssas-tabular.md)   
 [역할 &#40;&AMP;#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)  
  
  
