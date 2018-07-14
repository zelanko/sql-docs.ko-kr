---
title: 다른 주석 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 01e0af9b72790b8a2ddf396434c84f25ee270313
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223133"
---
# <a name="other-annotations-sqlxml-40"></a>기타 주석(SQLXML 4.0)
  XML 대량 로드는 이 섹션의 이전 항목에서 설명한 주석 외에 다음과 같은 기타 주석도 해석합니다.  
  
 `sql:id-prefix`  
 스키마에서 접두사를 XML 데이터로 지정한 경우 XML 대량 로드는 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 보내기 전에 접두사를 제거합니다.  
  
 `sql:use-cdata`  
 XML 대량 로드는 CDATA 섹션에 저장된 텍스트를 읽어 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 보냅니다.  
  
 `sql:url-encode`  
 XML 대량 로드는 이 주석을 지원하지 않습니다. 예를 들어 XML 데이터 입력에 URL을 지정하면 XML 대량 로드는 데이터베이스의 해당 데이터 저장 위치에서 데이터를 읽지 못합니다.  
  
 `sql:is-mapping-schema`  
 XML 대량 로드는 이 주석이나 `sql:id`를 지원하지 않습니다.  
  
> [!NOTE]  
>  XML 대량 로드는 인라인 매핑 스키마를 지원하지 않습니다.  
  
 `sql:key-fields`  
 XML 대량 로드는 이 주석을 항상 무시합니다.  
  
## <a name="see-also"></a>관련 항목  
 [주석 해석 &#40;SQLXML 4.0&#41;](annotation-interpretation-sqlxml-4-0.md)  
  
  
