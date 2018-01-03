---
title: "SQLGetTypeInfo (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2e552a73289da6d78223b6416b7be7fe125e23e7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 적용:  
  
 데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 드라이버는 SQL 결과 집합의 정보를 반환 합니다. 다음 표에서 ODBC 데이터 형식 및 해당 Visual FoxPro 데이터 형식을 나열합니다.  
  
|ODBC 형식|Visual FoxPro 유형|  
|---------------|------------------------|  
|SQL_BIGINT|지원되지 않습니다. 64 비트 Visual FoxPro 형식이 없습니다.|  
|SQL_BIT|논리|  
|SQL_CHAR|문자|  
|SQL_DATE|date|  
|SQL_DECIMAL|숫자|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|정수|  
|SQL_LONGVARBINARY|메모 (이진)|  
|SQL_LONGVARCHAR|메모|  
|SQL_NUMERIC|숫자 *, 통화, Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|정수|  
|SQL_TIME|지원되지 않습니다. Visual FoxPro 없습니다는 *시간* 유형입니다.|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|정수|  
|SQL_VARBINARY|메모 (이진) *, 일반|  
|SQL_VARCHAR|문자|  
  
 * 기본 형식  
  
 Visual FoxPro 데이터 형식에 대 한 자세한 내용은 참조 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)합니다. 이 함수에 대 한 자세한 내용은 참조 [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) 에 *ODBC Programmer's Reference*합니다.
