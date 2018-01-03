---
title: "데스크톱에 대 한 진단 데이터베이스 드라이버 | Microsoft Docs"
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
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5440d7cb38dfeef678a9b665397b789bf506be72
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="diagnostics-for-desktop-database-drivers"></a>데스크톱 데이터베이스 드라이버에 대 한 진단
모든 오류와 경고를 선택 하거나 일부만 드라이버 관리자가 선택 되어 하지 드라이버에 의해 처리 됩니다. 드라이버 매핑됩니다.이 형식은 네이티브 오류 또는 Sqlstate를 데이터 원본에 의해 반환 되는 오류입니다. 에 나열 된 각 함수는 *ODBC Programmer's Reference* 조건 및 메시지를 지정 하는 "진단" 섹션을 포함 합니다.  
  
 응용 프로그램 호출 **SQLGetDiagRec** SQLSTATE, 원시 오류 코드 및 진단 메시지를 검색할 수 있습니다. 호출 **SQLGetDiagField** 개별 진단 필드를 검색 하는 필드를 지정 하 고 있습니다. 지원 수준 진단 식별자의 다음 표에 나열 됩니다.  
  
|DiagIdentifiers|지원 수준|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|지원되지 않음|  
|SQL_DIAG_CLASS_ORIGIN|지원됩니다. 항상 "ODBC 3.0" 하 고 나중에이 드라이버의 버전 3.0에 대 한 합니다.|  
|SQL_DIAG_COLUMN_NUMBER|지원됨|  
|SQL_DIAG_CURSOR_ROW_COUNT|지원되지 않음|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|지원되지 않음|  
|SQL_DIAG_MESSAGE_TEXT|지원됨|  
|SQL_DIAG_NATIVE|지원됨|  
|SQL_DIAG_NUMBER|지원됨|  
|SQL_DIAG_RETURNCODE|그러나 드라이버 관리자에서 구현 지원|  
|SQL_DIAG_ROW_COUNT|지원됨|  
|SQL_DIAG_ROW_NUMBER|지원됨|  
|SQL_DIAG_SERVER_NAME|지원되지 않음|  
|SQL_DIAG_SQLSTATE|지원됨|  
|SQL_DIAG_SUBCLASS_ORIGIN|지원됨|
