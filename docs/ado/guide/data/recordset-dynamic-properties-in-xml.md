---
description: XML의 레코드 집합 동적 속성
title: XML의 레코드 집합 동적 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: rothja
ms.author: jroth
ms.openlocfilehash: 395a81108e3ceaed99ad8ccf1fbab29831dd116d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979894"
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
