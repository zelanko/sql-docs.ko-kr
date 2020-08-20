---
description: 평가 보고서 (AccessToSQL)
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5f1058947591fdd454ce181b2d098f88b183cbe1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497829"
---
# <a name="assessment-report-accesstosql"></a>평가 보고서 (AccessToSQL)
평가 보고서 창에는 데이터베이스 개체를 구문으로 변환한 결과가 표시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 되며 마이그레이션 프로젝트의 복잡성과 비용을 예측 하는 데에도 도움이 될 수 있습니다.  
  
평가 보고서를 만들려면 원본 메타 데이터 탐색기에서 변환할 개체를 선택 하 고 **데이터베이스**를 마우스 오른쪽 단추로 클릭 한 다음 **보고서 만들기**를 선택 합니다. 스키마를 변환한 후에는이 보고서를 자동으로 표시할 수도 있습니다. 그러나 보고서 이름은 변환 보고서가 됩니다. 자세한 내용은 [프로젝트 설정 (GUI) (SSMA Common)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)을 참조 하세요.  
  
## <a name="options"></a>옵션  
**탐색기 창**  
평가 보고서에 개체의 계층 구조를 포함 합니다. 개별 개체 및 하위 구성 요소를 보려면 폴더를 확장 합니다. 범주나 개체를 클릭 하면 해당 범주 또는 개체에 대 한 변환 통계가 세부 정보 창에 표시 됩니다.  
  
**세부 정보 창**  
선택한 개체에 대 한 변환 통계 또는 오류 및 경고 메시지를 표시 합니다. 예를 들어 테이블 폴더가 선택 된 경우 세부 정보 창에는 변환 된 외래 키, 인덱스, 기본 키 및 테이블 수가 표시 됩니다.  
  
**메시지 창**  
평가 보고서를 만들 때 생성 된 오류, 경고 및 정보 메시지를 표시 합니다. 메시지는 숫자로 그룹화 됩니다.  
  
메시지 정보를 보려면 **오류**, **경고**또는 메시지를 클릭 한 다음 **메시지를 확장**합니다. SSMA에서이 오류가 발생 한 개체의 목록을 표시 합니다. 개체를 클릭 하 여 개체에 대 한 모든 변환 정보를 표시 합니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 인터페이스 참조 (액세스)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
