---
title: 플랫 파일 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0a0516d2e038f206c140f010c2ca4a459f79956a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62902050"
---
# <a name="flat-file-custom-properties"></a>플랫 파일 사용자 지정 속성
  **원본 사용자 지정 속성**  
  
 플랫 파일 원본에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 플랫 파일 원본의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|문자열|파일 이름이 포함된 출력 열의 이름입니다. 이름이 지정되지 않은 경우 파일 이름이 포함된 출력 열이 생성되지 않습니다.<br /><br /> 참고: 이 속성은 **플랫 파일 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|RetainNulls|Boolean|데이터 변환 파이프라인 엔진에서 데이터를 처리할 때 원본 파일의 Null 값을 Null 값으로 유지할지 여부를 지정하는 값입니다. 이 속성의 기본값은 `False`입니다.|  
  
 플랫 파일 원본의 출력에는 사용자 지정 속성이 없습니다.  
  
 다음 표에서는 플랫 파일 원본 출력 열의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|열이 DTS에서 제공하는 더 빠르지만 로캘을 구분하지 않는 빠른 구문 분석 루틴을 사용하는지, 아니면 로캘을 구분하는 표준 구문 분석 루틴을 사용하는지를 나타내는 값입니다. 자세한 내용은 [Fast Parse](../fast-parse.md) 및 [Standard Parse](../standard-parse.md)를 참조하세요. 이 속성의 기본값은 `False`입니다.<br /><br /> 참고: 이 속성은 **플랫 파일 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
  
 자세한 내용은 [Flat File Source](flat-file-source.md)을 참조하세요.  
  
 **대상 사용자 지정 속성**  
  
 플랫 파일 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 플랫 파일 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|헤더|문자열|데이터를 쓰기 전에 파일에 삽입할 텍스트 블록입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
|Overwrite|Boolean|이름이 같은 기존 대상 파일을 덮어쓸지, 아니면 해당 파일에 추가할지를 지정하는 값입니다. 이 속성의 기본값은 `True`입니다.|  
  
 플랫 파일 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Flat File Destination](flat-file-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [공용 속성](../common-properties.md)  
  
  
