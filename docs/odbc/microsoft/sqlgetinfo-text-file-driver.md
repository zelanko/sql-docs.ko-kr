---
title: SQLGetInfo (텍스트 파일 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09ca2e42e20a6f314de3b68fe5d5b143f41269c3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298504"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 **SQLGetInfo는** SQL_FILE_USAGE 정보 형식을 지원합니다. 반환된 값은 드라이버가 데이터 원본에서 파일을 직접 처리하는 방법을 나타내는 16비트 정수입니다.  
  
-   SQL_FILE_NOT_SUPPORTED - 드라이버는 단일 계층 드라이버가 아닙니다.  
  
-   SQL_FILE_TABLE - 단일 계층 드라이버는 데이터 원본의 파일을 테이블로 처리합니다.  
  
-   SQL_FILE_QUALIFIER - 단일 계층 드라이버는 데이터 원본의 파일을 한정자로 처리합니다.  
  
 ODBC 드라이버는 각 파일이 테이블이기 때문에 textdriver에 대한 SQL_FILE_TABLE 반환합니다.  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|Isam|버전|버전 번호 의 형식|  
|----------|-------------|-------------------------------|  
|텍스트|1.0|01.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
