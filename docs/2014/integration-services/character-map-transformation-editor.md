---
title: 문자표 변환 편집기 문자 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- Character Map Transformation Editor
ms.assetid: 3f1dbcf9-9cca-4606-bdcc-7ea6ad48cdf3
caps.latest.revision: 25
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 94857d436adf11eb8cc9732a20918478457d95fe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223739"
---
# <a name="character-map-transformation-editor"></a>문자표 변환 편집기
  **문자표 변환 편집기** 대화 상자를 사용하여 열 데이터에 적용할 문자열 함수를 선택하고 매핑이 내부 변경인지, 아니면 새 열로 추가되었는지를 지정할 수 있습니다.  
  
 문자 매핑 변환에 대한 자세한 내용은 [Character Map Transformation](data-flow/transformations/character-map-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **사용 가능한 입력 열**  
 확인란을 사용하여 문자열 함수로 변환할 열을 선택할 수 있습니다. 아래 테이블에 선택 내용이 나타납니다.  
  
 **입력 열**  
 위 테이블에서 선택한 입력 열을 표시합니다. 사용 가능한 입력 열 목록을 사용하여 선택 내용을 변경 또는 제거할 수도 있습니다.  
  
 **대상**  
 문자열 작업 결과를 기존 열을 사용하여 내부에 저장할지, 아니면 수정된 데이터를 새 열로 저장할지를 지정합니다.  
  
|값|Description|  
|-----------|-----------------|  
|새 열|새 열에 데이터를 저장합니다. **출력 별칭**의 열 이름을 할당합니다.|  
|내부 변경|수정된 데이터를 기존 열에 저장합니다.|  
  
 **연산**  
 열 데이터에 적용할 문자열 함수를 목록에서 선택합니다.  
  
|값|Description|  
|-----------|-----------------|  
|소문자|소문자로 변환합니다.|  
|대문자|대문자로 변환합니다.|  
|바이트 반전|바이트 순서를 반대로 바꿔 변환합니다.|  
|히라가나|일본어 가타카나 문자를 히라가나로 변환합니다.|  
|가타카나|일본어 히라가나 문자를 가타카나로 변환합니다.|  
|반자|전자 문자를 반자로 변환합니다.|  
|전자|반자 문자를 전자로 변환합니다.|  
|대/소문자 구분 기능|시스템 규칙 대신 대/소문자 구분 규칙(터키어 및 다른 로캘의 유니코드 단순 대/소문자 구분 매핑)을 적용합니다.|  
|중국어(간체)|중국어 번체 문자를 간체로 변환합니다.|  
|중국어(번체)|중국어 간체 문자를 번체로 변환합니다.|  
  
 **출력 별칭**  
 각 출력 열의 별칭을 입력합니다. 기본값은 **Copy of** 뒤에 입력 열 이름이 오는 형식이지만 설명이 포함된 고유 이름을 선택할 수 있습니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](../../2014/integration-services/configure-error-output.md) 대화 상자를 사용하여 이 변환에 대한 오류 처리 옵션을 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
