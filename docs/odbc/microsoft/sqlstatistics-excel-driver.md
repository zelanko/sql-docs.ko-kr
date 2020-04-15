---
title: SQLStatistics (엑셀 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Excel Driver
ms.assetid: 02506664-8dcc-4bd0-a8bb-d49fcbdd5722
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 51b7e59fa811dd7b4ac69f1e9c8d39b4d482c437
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299343"
---
# <a name="sqlstatistics-excel-driver"></a>SQLStatistics(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
|열|주석|  
|------------|--------------|  
|TABLE_QUALIFIER|디렉터리로 가는 경로입니다.<br /><br /> 패턴 일치는 *szTableQualifier* 인수에서 지원되지 않습니다.|  
|TABLE_OWNER|소유자 이름이 지원되지 않으므로 NULL이 이 열에서 반환됩니다.|  
|TABLE_NAME|제한되지 않은 테이블 이름입니다.<br /><br /> 패턴 일치는 *szTableName* 인수에서 지원되지 않습니다.|  
|INDEX_QUALIFIER|NULL은 항상 반환됩니다.|  
|INDEX_NAME|인덱스 에 따라 다릅니다.|  
|TYPE|TYPE에 대해 SQL_TABLE_STAT 또는 SQL_INDEX_OTHER 반환됩니다.|  
|SEQ_IN_INDEX|인덱스 에 따라 다릅니다.|  
|COLUMN_NAME|인덱스 에 따라 다릅니다.|  
|COLLATION|인덱스 에 따라 다릅니다.|  
|PAGES|NULL은 항상 반환됩니다.|  
  
 필터링은 *고유성(fUnique* 인수)을 기반으로 합니다. *fAccuracy* 매개 변수는 무시됩니다.
