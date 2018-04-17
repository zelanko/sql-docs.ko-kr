---
title: SQLGetInfo (Paradox 드라이버) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- Paradox driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Paradox Driver
ms.assetid: 43aab762-68f4-4128-b8f5-8878ea5f1258
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aee1958b5b4c010dd2f0727da5f928c38835b399
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetinfo-paradox-driver"></a>SQLGetInfo (Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLGetInfo** SQL_FILE_USAGE 정보 유형을 지원 합니다. 반환 된 값이 드라이버 파일을 데이터 원본에서 직접 처리 하는 방법을 나타내는 16 비트 정수.  
  
-   SQL_FILE_NOT_SUPPORTED — 드라이버는 단일 계층 드라이버가 아닙니다.  
  
-   SQL_FILE_TABLE-단일 계층 드라이버에서는 파일 데이터 원본의 테이블로 처리 합니다.  
  
-   SQL_FILE_QUALIFIER-단일 계층 드라이버 한정자로 데이터 원본 파일을 처리합니다.  
  
 ODBC 드라이버는 각 파일은 테이블 SQL_FILE_TABLE를 반환 합니다.  
  
## <a name="sqlaltertable"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN &AMP;#124; SQL_AT_DROP_COLUMN  
  
## <a name="sqlddlindex"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|버전|버전 번호의 형식|  
|----------|-------------|-------------------------------|  
|Paradox|3.x|03.00.0000|  
||4.x|04.00.0000|  
||5.x|05.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &AMP;#124; SQL_QU_TABLE_DEFINITION &AMP;#124; SQL_QU_INDEX_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &AMP;#124; SQL_FN_TD_DAYOFWEEK &AMP;#124; SQL_FN_TD_DAYOFYEAR &AMP;#124; SQL_FN_TD_HOUR &AMP;#124; SQL_FN_TD_MINUTE &AMP;#124; SQL_FN_TD_MONTH &AMP;#124; SQL_FN_TD_SECOND &AMP;#124; SQL_FN_TD_WEEK &AMP;#124; SQL_FN_TD_YEAR
