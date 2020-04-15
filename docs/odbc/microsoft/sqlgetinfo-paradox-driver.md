---
title: SQLGetInfo (역설 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Paradox Driver
ms.assetid: 43aab762-68f4-4128-b8f5-8878ea5f1258
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 354fa7f08797ee1fbfb057bfc2f2c192a8c5eddc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298573"
---
# <a name="sqlgetinfo-paradox-driver"></a>SQLGetInfo(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 역설 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 **SQLGetInfo는** SQL_FILE_USAGE 정보 형식을 지원합니다. 반환된 값은 드라이버가 데이터 원본에서 파일을 직접 처리하는 방법을 나타내는 16비트 정수입니다.  
  
-   SQL_FILE_NOT_SUPPORTED - 드라이버는 단일 계층 드라이버가 아닙니다.  
  
-   SQL_FILE_TABLE - 단일 계층 드라이버는 데이터 원본의 파일을 테이블로 처리합니다.  
  
-   SQL_FILE_QUALIFIER - 단일 계층 드라이버는 데이터 원본의 파일을 한정자로 처리합니다.  
  
 ODBC 드라이버는 각 파일이 테이블이기 때문에 SQL_FILE_TABLE 반환합니다.  
  
## <a name="sql_alter_table"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN &#124; SQL_AT_DROP_COLUMN  
  
## <a name="sql_ddl_index"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|Isam|버전|버전 번호 의 형식|  
|----------|-------------|-------------------------------|  
|역설|3.x|03.00.0000|  
||4.x|04.00.0000|  
||5.x|05.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION &#124; SQL_QU_INDEX_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
