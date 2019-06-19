---
title: XML 원본 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e5c992253304d2a1c493f52a9e24cf569ff29883
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770190"
---
# <a name="xml-source-custom-properties"></a>XML 원본 사용자 지정 속성
  XML 원본에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 XML 원본의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|정수|XML 데이터에 액세스하는 데 사용되는 모드입니다.|  
|UseInlineSchema|Boolean|XML 원본 내에서 인라인 스키마 정의를 사용할지 여부를 나타내는 값입니다. 이 속성의 기본값은 `False`입니다.|  
|XMLData|문자열|XML 데이터를 검색할 파일 또는 변수입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
|XMLSchemaDefinition|문자열|스키마 정의 파일(.xsd)의 경로 및 파일 이름입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
  
 다음 표에서는 XML 원본 출력의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|문자열|출력과 연결된 행 집합을 식별하는 값입니다.|  
  
 XML 원본의 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [XML Source](xml-source.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [공용 속성](../common-properties.md)  
  
  
