---
title: 데스크톱 데이터베이스 드라이버에 대한 진단 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99603c047e77d3cd3e077c1b07c2192eeb65f93c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303484"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>데스크톱 데이터베이스 드라이버에 대한 진단
드라이버 관리자가 확인하거나 부분적으로 검사하지 않은 모든 오류 및 경고는 운전자가 처리합니다. 또한 드라이버는 기본 오류 또는 데이터 원본에서 반환되는 오류를 SQLSTATEs에 매핑합니다. *ODBC 프로그래머의 참조에* 나열된 각 기능에는 조건 및 메시지를 지정하는 "진단" 섹션이 포함되어 있습니다.  
  
 응용 프로그램은 **SQLGetDiagRec를** 호출하여 SQLSTATE, 기본 오류 코드 및 진단 메시지를 검색합니다. **SQLGetDiagField를** 호출하고 필드를 지정하면 개별 진단 필드가 검색됩니다. 진단 식별자의 지원 수준은 다음 표에 나열됩니다.  
  
|디아그식별서|지원 수준|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|지원 안 함|  
|SQL_DIAG_CLASS_ORIGIN|지원됩니다. 이 드라이버의 버전 3.0 이상에 대해 항상 "ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|지원됨|  
|SQL_DIAG_CURSOR_ROW_COUNT|지원 안 함|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|지원 안 함|  
|SQL_DIAG_MESSAGE_TEXT|지원됨|  
|SQL_DIAG_NATIVE|지원됨|  
|SQL_DIAG_NUMBER|지원됨|  
|SQL_DIAG_RETURNCODE|지원되지만 드라이버 관리자에 의해 구현됩니다.|  
|SQL_DIAG_ROW_COUNT|지원됨|  
|SQL_DIAG_ROW_NUMBER|지원됨|  
|SQL_DIAG_SERVER_NAME|지원 안 함|  
|SQL_DIAG_SQLSTATE|지원됨|  
|SQL_DIAG_SUBCLASS_ORIGIN|지원됨|
