---
title: Union All 변환 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- Union All Transformation Editor
ms.assetid: 32fbc1c1-da83-4684-9479-31fc3e2df98c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b62fb5e33311f1011911c40fc858723b218bac55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054828"
---
# <a name="union-all-transformation-editor"></a>UNION ALL 변환 편집기
  **UNION ALL 변환 편집기** 대화 상자를 사용하여 여러 개의 입력 행 집합을 단일 출력 행 집합으로 병합할 수 있습니다. Union All 변환을 데이터 흐름에 포함하면 여러 데이터 흐름의 데이터를 병합하고, Union All 변환을 중첩하여 복잡한 데이터 세트를 만들고, 데이터의 오류를 수정하고, 행을 다시 병합할 수 있습니다.  
  
 UNION ALL 변환에 대한 자세한 내용은 [Union All Transformation](data-flow/transformations/union-all-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **출력 열 이름**  
 각 열의 별칭을 입력합니다. 기본값은 첫 번째(참조) 입력의 입력 열 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **UNION ALL 입력 1**  
 첫 번째(참조) 입력의 사용 가능한 입력 열 목록에서 선택합니다. 매핑된 열의 메타데이터가 일치해야 합니다.  
  
 **UNION ALL 입력 n**  
 두 번째 및 추가 입력의 사용 가능한 입력 열 목록에서 선택합니다. 매핑된 열의 메타데이터가 일치해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [UNION ALL 변환을 사용하여 데이터 병합](data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)   
 [병합 변환](data-flow/transformations/merge-transformation.md)   
 [병합 조인 변환](data-flow/transformations/merge-join-transformation.md)  
  
  
