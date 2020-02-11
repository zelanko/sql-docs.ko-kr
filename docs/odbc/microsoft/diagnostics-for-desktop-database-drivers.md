---
title: 데스크톱 데이터베이스 드라이버에 대 한 진단 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4e7c8ea96708886f9edf54047bd2a2104ba0ec8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031226"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>데스크톱 데이터베이스 드라이버에 대한 진단
드라이버 관리자가 검사 하거나 부분적으로 검사 하지 않은 모든 오류 및 경고는 드라이버에 의해 처리 됩니다. 또한 드라이버는 네이티브 오류 또는 데이터 소스에서 반환 된 오류를 SQLSTATEs에 매핑합니다. *ODBC 프로그래머 참조* 에 나열 된 각 함수에는 조건 및 메시지를 지정 하는 "진단" 섹션이 포함 되어 있습니다.  
  
 응용 프로그램은 **SQLGetDiagRec** 를 호출 하 여 SQLSTATE, 네이티브 오류 코드 및 진단 메시지를 검색 합니다. **SQLGetDiagField** 를 호출 하 고 필드를 지정 하면 개별 진단 필드가 검색 됩니다. 다음 표에는 진단 식별자의 지원 수준이 나와 있습니다.  
  
|DiagIdentifiers|지원 수준|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|지원되지 않음|  
|SQL_DIAG_CLASS_ORIGIN|지원됩니다. 이 드라이버의 버전 3.0 이상에서는 항상 "ODBC 3.0"입니다.|  
|SQL_DIAG_COLUMN_NUMBER|지원됨|  
|SQL_DIAG_CURSOR_ROW_COUNT|지원되지 않음|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|지원되지 않음|  
|SQL_DIAG_MESSAGE_TEXT|지원됨|  
|SQL_DIAG_NATIVE|지원됨|  
|SQL_DIAG_NUMBER|지원됨|  
|SQL_DIAG_RETURNCODE|지원 되지만 드라이버 관리자에 의해 구현 됨|  
|SQL_DIAG_ROW_COUNT|지원됨|  
|SQL_DIAG_ROW_NUMBER|지원됨|  
|SQL_DIAG_SERVER_NAME|지원되지 않음|  
|SQL_DIAG_SQLSTATE|지원됨|  
|SQL_DIAG_SUBCLASS_ORIGIN|지원됨|
