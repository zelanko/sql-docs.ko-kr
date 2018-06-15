---
title: SQLStatistics (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Text File Driver
ms.assetid: 311afc01-d656-425f-be43-4a8e7cbc9a97
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2e53ce34c9095f28ee80ca7eeaa5f1f09b0a3eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32903228"
---
# <a name="sqlstatistics-text-file-driver"></a>SQLStatistics (텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|열|설명|  
|------------|--------------|  
|TABLE_QUALIFIER|디렉터리 경로입니다.<br /><br /> 패턴 일치에서 지원 되지 않습니다는 *szTableQualifier* 인수입니다.|  
|TABLE_OWNER|소유자 이름입니다. 지원 되지 않으므로이 열에 NULL이 반환 됩니다.|  
|TABLE_NAME|구분 되지 않은 테이블 이름입니다.<br /><br /> 패턴 일치에서 지원 되지 않습니다는 *szTableName* 인수입니다.|  
|INDEX_QUALIFIER|항상 NULL이 반환 됩니다.|  
|INDEX_NAME|인덱스에 따라 다릅니다.|  
|TYPE|형식에 대 한 SQL_TABLE_STAT 또는 SQL_INDEX_OTHER만 반환 됩니다.|  
|SEQ_IN_INDEX|인덱스에 따라 다릅니다.|  
|COLUMN_NAME|인덱스에 따라 다릅니다.|  
|COLLATION|인덱스에 따라 다릅니다.|  
|PAGES|항상 NULL이 반환 됩니다.|  
  
 고유성 기반 필터링 (의 *fUnique* 인수). *fAccuracy* 매개 변수가 무시 됩니다.
