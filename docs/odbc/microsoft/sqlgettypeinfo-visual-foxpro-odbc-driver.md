---
description: SQLGetTypeInfo(Visual FoxPro ODBC 드라이버)
title: SQLGetTypeInfo (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e24f506f1134e9191e370971795a23bbbb3bd380
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500181"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 드라이버는 SQL 결과 집합의 정보를 반환 합니다. 다음 표에서는 ODBC 데이터 형식과 해당 하는 Visual FoxPro 데이터 형식을 보여 줍니다.  
  
|ODBC 형식|Visual FoxPro 형식|  
|---------------|------------------------|  
|SQL_BIGINT|지원되지 않습니다. 64 비트 Visual FoxPro 형식이 없습니다.|  
|SQL_BIT|논리적|  
|SQL_CHAR|문자|  
|SQL_DATE|Date|  
|SQL_DECIMAL|숫자|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|정수|  
|SQL_LONGVARBINARY|메모 (이진)|  
|SQL_LONGVARCHAR|메모|  
|SQL_NUMERIC|숫자 *, 통화, 부동 소수점|  
|SQL_REAL|Double|  
|SQL_SMALLINT|정수|  
|SQL_TIME|지원되지 않습니다. Visual FoxPro *시간* 형식이 없습니다.|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|정수|  
|SQL_VARBINARY|메모 (이진) *, 일반|  
|SQL_VARCHAR|문자|  
  
 * 기본 형식  
  
 Visual FoxPro 데이터 형식에 대 한 자세한 내용은 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)를 참조 하세요. 이 함수에 대 한 자세한 내용은 *ODBC 프로그래머 참조*에서 [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) 를 참조 하세요.
