---
title: 평가 보고서 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1278552f1bfe1ccfb7ab250f843e86c62e63440b
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659849"
---
# <a name="assessment-report-accesstosql"></a>평가 보고서 (AccessToSQL)
평가 보고서 창에 데이터베이스 개체의 변환 결과 보여 줍니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 마이그레이션 프로젝트의 비용과 복잡성을 예측할 수 있습니다.  
  
원본 메타 데이터 탐색기에서 변환할 개체를 선택할 평가 보고서를 만들려면 **데이터베이스**를 선택한 후 **보고서 만들기**합니다. 스키마를 변환한 후 자동으로이 보고서를 표시할 수 있습니다도 합니다. 그러나 보고서 이름을 변환 보고서 됩니다. 자세한 내용은 [프로젝트 설정 (GUI) (SSMA 공통)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)합니다.  
  
## <a name="options"></a>변수  
**탐색기 창**  
평가 보고서에 개체 계층을 포함 합니다. 개별 개체와 하위 구성 요소를 표시할 폴더를 확장 합니다. 범주 또는 개체를 클릭 하면 해당 범주 또는 개체에 대 한 변환 통계 세부 정보 창에 나타납니다.  
  
**세부 정보 창**  
선택한 개체에 대 한 통계 또는 오류 및 경고 메시지 변환을 보여 줍니다. 예를 들어 테이블 폴더를 선택 하는 경우 세부 정보 창 외래 키, 인덱스, 기본 키 및 변환 된 테이블 수가 표시 됩니다.  
  
**메시지 창**  
오류, 경고 및 평가 보고서를 만들 때 생성 된 정보 메시지를 보여 줍니다. 메시지 수로 그룹화 됩니다.  
  
메시지 세부 정보를 보려면 중 하나를 클릭 **오류**를 **경고**, 또는 **메시지**, 한 다음 메시지를 확장 합니다. SSMA는이 오류가 있는 개체 목록이 표시 됩니다. 개체에 대 한 모든 변환 정보를 표시 하는 개체를 클릭 합니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 인터페이스 Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
