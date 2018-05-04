---
title: SQLGetDescField 및 SQLGetDescRec (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4df2bb337eeff7e6d2661fa0809deb5e7cc4a3e1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 및 SQLGetDescRec (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLGetDescField** 및 **SQLGetDescRec** 커서 라이브러리의 함수입니다. 이러한 함수에 대 한 일반 정보를 참조 하십시오. [SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 및 [SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)합니다.  
  
 커서 라이브러리 실행 **SQLGetDescRec** 책갈피 열에 대 한 메타 데이터를 반환 합니다. 커서 라이브러리 실행 **SQLGetDescField** 반환한 동일한 필드를 반환 하려면 **SQLGetDescRec**는 SQL_DESC_NAME, SQL_DESC_TYPE, 값을 SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_ 길이, SQL_DESC_PRECISION, SQL_DESC_SCALE, 및 SQL_DESC_NULLABLE 합니다. 일관성을 위해 **SQLGetDescField** SQL_DESC_UNNAMED도 반환 합니다.  
  
 커서 라이브러리 실행 **SQLGetDescField** 바인딩 책갈피 열에 대해 설정 되는 다음의 값 필드를 반환 하기 위해 호출 되는 경우: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR, 및 SQL_DESC_LENGTH 합니다.  
  
 커서 라이브러리 실행 **SQLGetDescField** SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE, 또는 SQL_DESC_ROW_STATUS_PTR 필드의 값을 반환 하도록 호출 됩니다. 이러한 필드는 책갈피 행 뿐 아니라 행에 대해 반환할 수 있습니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLGetDescField** 커서 라이브러리를 이전에 언급 된 것과 다른 모든 필드의 값을 반환 하려면 드라이버에 대 한 호출을 전달 합니다.
