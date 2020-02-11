---
title: SQLStatistics (Paradox 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d60296a73367b4718c4da5df036befa0cd34b505
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114368"
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|열|주석|  
|------------|--------------|  
|TABLE_QUALIFIER|디렉터리에 대 한 경로입니다.<br /><br /> *Sztablequalifier* 인수에는 패턴 일치가 지원 되지 않습니다.|  
|TABLE_OWNER|소유자 이름이 지원 되지 않으므로이 열에 NULL이 반환 됩니다.|  
|TABLE_NAME|구분 기호로 분리 된 테이블 이름입니다.<br /><br /> *Sztablename* 인수에서는 패턴 일치가 지원 되지 않습니다.|  
|INDEX_QUALIFIER|NULL은 항상 반환 됩니다.|  
|INDEX_NAME|인덱스 종속.|  
|TYPE|SQL_TABLE_STAT 또는 SQL_INDEX_OTHER 형식에 대해 반환 됩니다.|  
|SEQ_IN_INDEX|인덱스 종속.|  
|COLUMN_NAME|인덱스 종속.|  
|COLLATION|인덱스 종속.|  
|PAGES|NULL은 항상 반환 됩니다.|  
  
 필터링은 고유성 ( *Funique* 인수)을 기반으로 합니다. *FAccuracy* 매개 변수는 무시 됩니다.
