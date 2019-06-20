---
title: SQLGetDescField 및 SQLGetDescRec (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66361572427c3264a1b25fe1c851685a07b2e029
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188762"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 및 SQLGetDescRec(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLGetDescField** 및 **SQLGetDescRec** 커서 라이브러리의 함수입니다. 이러한 함수에 대 한 일반적인 정보를 참조 하세요 [SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 하 고 [SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)합니다.  
  
 커서 라이브러리를 실행 **SQLGetDescRec** 책갈피 열에 대 한 메타 데이터를 반환 합니다. 커서 라이브러리를 실행 **SQLGetDescField** 반환한 동일한 필드를 반환 하려면 **SQLGetDescRec**은 SQL_DESC_NAME SQL_DESC_TYPE, 값을 SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_ 길이, SQL_DESC_PRECISION, 자릿수가 SQL_DESC_SCALE, 및 SQL_DESC_NULLABLE 합니다. 일관성을 위해 **SQLGetDescField** 도 SQL_DESC_UNNAMED를 반환 합니다.  
  
 커서 라이브러리를 실행 **SQLGetDescField** 바인딩 책갈피 열에 대해 설정 된 다음의 값 필드는 반환할 호출 되는 경우: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR을 및 SQL_DESC_LENGTH 합니다.  
  
 커서 라이브러리를 실행 **SQLGetDescField** SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE, 또는 SQL_DESC_ROW_STATUS_PTR 필드의 값을 반환 하도록 호출 되는 경우. 이러한 필드는 책갈피 행 뿐 아니라 모든 행에 대해 반환할 수 있습니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLGetDescField** 커서 라이브러리 앞에서 언급 한 것과 다른 모든 필드의 값을 반환 하는 드라이버에 대 한 호출을 전달 합니다.
