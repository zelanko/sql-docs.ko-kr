---
title: 데이터 탐색 (데이터 마이닝 추가 기능 SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4a20484a85b459dad58e5e6687a6cc34a093b130
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528359"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>데이터 탐색(SQL Server 데이터 마이닝 추가 기능)
  ![데이터 탐색 마법사](media/dmc-explore.gif "데이터 탐색 마법사")  
  
 **데이터 탐색** 마법사를 사용 하 여 데이터 테이블에 있는 데이터의 유형과 크기를 이해할 수 있습니다. 이 마법사는 선택한 열에 대한 분포와 값을 한 번에 한 열씩 그래프로 표시합니다. 그러면 데이터 그룹화 방식을 변경하여 시험해 보거나 내용을 표시하는 차트를 Excel 통합 문서에 복사하여 검토할 수 있습니다.  
  
 데이터에 연속 숫자 데이터가 포함된 경우 다음 두 뷰 사이를 전환할 수 있습니다.  
  
-   **선 그래프입니다.** 이 그래프는 X축에는 데이터 값이 Y축에는 사례 수가 있는 그래프입니다.  
  
-   **가로 막대형 차트입니다.** 이 그래프는 각 값에 대한 사례 수로 값을 그룹화합니다.  
  
 마법사가 데이터에서 그룹을 찾으면 데이터 값의 실제 분포가 사용됩니다. 따라서 가로 막대형 차트는 10 또는 100과 같은 일반적인 정수 숫자 축 표식을 표시하지 않습니다. 대신 가로 막대형 차트에 표시되는 범위는 43521-55603(Income 열의 경우)과 같습니다.  
  
 다른 범위로 데이터를 그룹화하려면 데이터를 분석하기 전에 Excel에서 이 작업을 수행해야 합니다. 또는 [레이블 재지정](relabel-sql-server-data-mining-add-ins.md) 마법사를 사용 하 여 데이터를 레이블 재지정 수 있습니다.  
  
## <a name="using-the-explore-data-wizard"></a>데이터 탐색 마법사 사용  
  
1.  **데이터 마이닝** 리본에서 **데이터 탐색**을 클릭 합니다.  
  
2.  **원본 선택** 대화 상자에서 데이터를 포함 하는 테이블 또는 셀 범위를 선택 합니다.  
  
3.  **열 선택** 대화 상자에서 분석할 열을 창에 표시 된 샘플 데이터에서 선택 합니다.  
  
4.  **데이터 탐색** 대화 상자에서 데이터 분포를 표시할 차트 종류를 선택 합니다.  
  
5.  필요에 따라 새 열을 데이터에 추가하거나 데이터 분할 방식을 변경하거나 차트를 Excel로 복사할 수 있습니다.  
  
### <a name="requirements"></a>요구 사항  
 **데이터 탐색** 마법사를 사용 하려면 데이터가 Excel 데이터 테이블에 있어야 합니다.   
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 준비 검사 목록](checklist-of-preparation-for-data-mining.md)  
  
  
