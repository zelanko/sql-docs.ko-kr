---
title: SQLGetInfo (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 256e964e556421db62dc8f52fdc6bc759c3a200a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63018358"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLGetInfo** SQL_FILE_USAGE 정보 유형을 지원 합니다. 반환된 값은 드라이버 파일을 데이터 원본에서 직접 처리 하는 방법을 나타내는 16 비트 정수.  
  
-   SQL_FILE_NOT_SUPPORTED-드라이버는 단일 계층 드라이버 없습니다.  
  
-   SQL_FILE_TABLE-단일 계층 드라이버 파일 데이터 원본에서 테이블로 처리합니다.  
  
-   단일 계층 드라이버 SQL_FILE_QUALIFIER-파일 데이터 원본에 한정자로 처리합니다.  
  
 ODBC 드라이버는 각 파일 테이블 이므로 Textdriver에 대 한 SQL_FILE_TABLE를 반환 합니다.  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|버전|버전 번호의 형식|  
|----------|-------------|-------------------------------|  
|텍스트 모드|1.0|01.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &AMP;#124; SQL_FN_TD_CURTIME &AMP;#124; SQL_FN_TD_DAYOFMONTH &AMP;#124; SQL_FN_TD_DAYOFWEEK &AMP;#124; SQL_FN_TD_DAYOFYEAR &AMP;#124; SQL_FN_TD_HOUR &AMP;#124; SQL_FN_TD_MINUTE &AMP;#124; SQL_FN_TD_MONTH &AMP;#124; SQL_FN_TD_NOW &AMP;#124; SQL_FN_TD_SECOND &AMP;#124; SQL_FN_TD_WEEK &AMP;#124; SQL_FN_TD_YEAR
