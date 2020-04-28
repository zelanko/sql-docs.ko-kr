---
title: XML의 레코드 집합 동적 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a058a2d0c5a808f29807744c6ba01f658bebc120
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924442"
---
# <a name="recordset-dynamic-properties-in-xml"></a>XML의 레코드 집합 동적 속성
클라이언트 커서 엔진에서 다음과 같은 레코드 집합 공급자별 속성은 현재 XML 형식으로 유지 됩니다.  
  
-   업데이트 다시 동기화  
  
-   고유한 테이블  
  
-   고유 스키마  
  
-   고유 카탈로그  
  
-   다시 동기화 명령  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   이름 변경  
  
-   AutoRecalc  
  
 이러한 속성은 유지 되는 레코드 집합에 대 한 요소 정의의 특성으로 스키마 섹션에 저장 됩니다. 이러한 특성은 행 집합 스키마 네임 스페이스에 정의 되며 접두사 "rs:"를 포함 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
