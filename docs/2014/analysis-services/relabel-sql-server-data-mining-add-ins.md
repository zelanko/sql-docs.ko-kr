---
title: (SQL Server 데이터 마이닝 추가 기능) 레이블 재지정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74e2322416ec06c36a7834f35581ed611480b6e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748326"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>레이블 재지정(SQL Server 데이터 마이닝 추가 기능)
  ![레이블 재지정 도구에 대 한 office 13 아이콘](media/dm13-relabel.gif "레이블 재지정 도구에 대 한 Office 13 아이콘")  
  
 Excel용 데이터 마이닝 클라이언트를 사용하면 분석 결과를 보다 쉽게 이해할 수 있도록 새 데이터 레이블을 만들 수 있습니다.  
  
 레이블 재지정 이유는 다음과 같습니다.  
  
-   데이터에 코딩된 결과(예: 남자의 경우 1, 여자의 경우 2)가 포함되어 있습니다.  
  
-   숫자 값을 버킷팅하고 있고 범위에 설명이 포함된 이름을 지정하려고 합니다.  
  
-   긴 이름을 단순화하려고 합니다.  
  
## <a name="using-the-relabel-wizard"></a>레이블 재지정 마법사 사용  
  
1.  **데이터 마이닝** 리본에서 **정리** 를 클릭한 다음 **레이블 재지정**을 선택합니다.  
  
2.  수정하려는 데이터가 포함된 테이블 또는 데이터 범위를 선택합니다.  
  
3.  마법사의 **레이블 재지정** 페이지에서 드롭다운 목록의 열을 선택하거나 **데이터 샘플** 창의 열을 클릭하여 단일 열을 선택합니다.  
  
     **데이터 샘플** 창은 약 50개의 데이터 행만 표시하지만 이들은 값의 좋은 분포를 확인할 수 있도록 샘플링됩니다.  
  
     **개수** 의 개수 헤더를 클릭하여 각 값의 개수를 기준으로 정렬합니다.  
  
     **원래 레이블**로 정렬할 수도 있습니다. 이것은 가장 높거나 낮은 값을 먼저 다시 레이블 지정하려는 경우에 유용합니다.  
  
4.  마법사의 **레이블 재지정** 데이터 페이지에서 **원래 레이블** 열의 값을 검토하여 이러한 값을 어떻게 그룹화하거나 편집할지 결정합니다.  
  
5.  **새로운 레이블**아래의 행에 새 값을 입력합니다. 기존 값 목록에서 값을 선택할 수도 있습니다. 새 값을 입력하면 즉시 다시 사용 가능하게 됩니다.  
  
6.  행을 충분히 입력 한 후, 클릭 **다음**, 및를 **대상 선택** 페이지에서 레이블 재지정된 된 데이터를 저장할 위치를 선택 합니다.  
  
    -   **현재 워크시트에 새 열으로 추가**  
  
         새 값을 포함하는 테이블에 새 열을 추가하려면 클릭합니다.  
  
    -   **시트 데이터와 해당 변경 내용 새 워크시트에 복사**  
  
         업데이트된 데이터를 포함하는 새 워크시트를 만들려면 클릭합니다.  
  
    -   **현재 위치에서 데이터를 변경 합니다.**  
  
         원래 데이터를 새 값으로 바꾸려면 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 탐색 및 지우기](exploring-and-cleaning-data.md)  
  
  
