---
title: "SQLGetTypeInfo (Excel 드라이버) | Microsoft Docs"
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
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb9d575ce17c4e4d8f825d5ae9f6767b22613493
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 생성 된 테이블에 반환 된 (TYPE_NAME) 형식의 이름을 **SQLGetTypeInfo** 이름이 데이터 원본에서 가장 일반적으로 사용 됩니다.  
  
 SQL_ALL_EXCEPT_LIKE이 반환할 검색 가능한 열의 바이트에 대 한 카운터, Double, 단일, Long 및 Short 데이터 형식입니다. (값 다음 비교를 수행 하는 ODBC 정식 변환 함수를 사용 하 여 문자를 변환 하는 LIKE 기능을 구현할 수 있습니다.)  
  
 Microsoft Excel 드라이버를 사용 하는 ODBC 형식 이름에서 반환 되는 TYPE_NAME 열에서 반환 됩니다 **SQLGetTypeInfo**합니다.
