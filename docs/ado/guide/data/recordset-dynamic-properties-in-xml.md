---
title: "XML에서 레코드 집합 동적 속성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62d9b59fc1145e09f89bbe69b8d7b6e561798e70
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-dynamic-properties-in-xml"></a>XML에서 레코드 집합 동적 속성
(Client Cursor Engine)에서 다음 레코드 집합 공급자별 속성이 현재 XML 형식으로 유지 됩니다.  
  
-   다시 동기화를 업데이트 합니다.  
  
-   고유 테이블  
  
-   고유한 스키마  
  
-   고유한 카탈로그  
  
-   다시 동기화 명령  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Name 모양 변경  
  
-   AutoRecalc  
  
 이러한 속성은 스키마 섹션에 유지 되 고 레코드 집합에 대 한 요소 정의의 특성으로 저장 됩니다. 이러한 특성은 행 집합 스키마 네임 스페이스에 정의 되어 있고 접두사를가지고 있어야 "rs:".  
  
## <a name="see-also"></a>관련 항목:  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)

