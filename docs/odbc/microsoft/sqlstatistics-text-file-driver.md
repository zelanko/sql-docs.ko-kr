---
description: SQLStatistics(텍스트 파일 드라이버)
title: SQLStatistics (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Text File Driver
ms.assetid: 311afc01-d656-425f-be43-4a8e7cbc9a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 82ea614fceb2d3af108fc592aa4c068d355bd1fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500126"
---
# <a name="sqlstatistics-text-file-driver"></a>SQLStatistics(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
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
