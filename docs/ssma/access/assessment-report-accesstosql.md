---
title: 평가 보고서 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6d9d1f0cb60af9065c1ed1e071ad250840f6ac69
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="assessment-report-accesstosql"></a>평가 보고서 (AccessToSQL)
데이터베이스 개체를 변환의 결과 표시 하는 평가 보고서 창 [!INCLUDE[tsql](../../includes/tsql_md.md)] 구문, 복잡성과 비용이 마이그레이션 프로젝트를 예상할 수 있습니다.  
  
원본 메타 데이터 탐색기에서 변환 하려면 객체 선택 평가 보고서를 만드는 마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **보고서 만들기**합니다. 스키마를 변환한 후 자동으로이 보고서를 표시할 수 수도 있습니다. 그러나 보고서 이름을 변환 보고서 됩니다. 자세한 내용은 참조 [프로젝트 설정 (GUI) (SSMA 공통)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)합니다.  
  
## <a name="options"></a>옵션  
**탐색기 창**  
평가 보고서에 있는 개체의 계층 구조를 포함합니다. 개별 개체 및 하위 구성 요소를 표시할 폴더를 확장 합니다. 범주 또는 개체를 클릭할 때 해당 범주 또는 개체에 대 한 변환 통계 세부 정보 창에 나타납니다.  
  
**세부 정보 창**  
선택한 개체에 대 한 통계 또는 오류 및 경고 메시지 변환을 보여 줍니다. 예를 들어 테이블 폴더를 선택 하는 경우 세부 정보 창 외래 키, 인덱스, 기본 키 및 변환 된 테이블의 수를 표시 됩니다.  
  
**메시지 창**  
오류, 경고 및 평가 보고서를 만들 때 생성 된 정보 메시지를 표시 합니다. 메시지 수로 그룹화 됩니다.  
  
메시지 세부 정보를 보려면 클릭 하거나 **오류**, **경고**, 또는 **메시지**, 메시지를 차례로 확장 합니다. SSMA는이 오류가 발생 하는 개체의 목록이 표시 됩니다. 개체는 개체에 대 한 모든 변환 정보를 표시 하려면 클릭 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[사용자 인터페이스 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
