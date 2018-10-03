---
title: XML에서 레코드 집합 동적 속성 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 50841931d26847ba339d64634d3eff4d7a7efc1b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712548"
---
# <a name="recordset-dynamic-properties-in-xml"></a>XML의 레코드 집합 동적 속성
(Client Cursor Engine)에서 다음 레코드 집합 공급자별 속성을 XML 형식으로 현재 유지 됩니다.  
  
-   다시 동기화를 업데이트 합니다.  
  
-   고유 테이블  
  
-   고유한 스키마  
  
-   고유 카탈로그  
  
-   다시 동기화 명령  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   변형 이름  
  
-   AutoRecalc  
  
 이러한 속성은 유지 되 고 레코드 집합에 대 한 요소 정의의 특성으로 스키마 섹션에 저장 됩니다. 이러한 특성은 행 집합 스키마 네임 스페이스에 정의 되어 있으며 접두사가 있어야 합니다. "rs:".  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
