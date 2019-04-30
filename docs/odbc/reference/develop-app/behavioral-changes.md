---
title: 동작 변경 내용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: abe670570dd2219247da0c70b2b62e1de4e60341
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181765"
---
# <a name="behavioral-changes"></a>동작 변경
동작 변경 내용이 있는 변경 내용이 반영 합니다 *구문* 인터페이스의 동일 하지만 *의미 체계* 변경 되었습니다. 이러한 변경 내용을 ODBC 2에서 사용 되는 기능입니다. *x* ODBC 3에서 동일한 기능을 다르게 동작 합니다. *x*합니다.  
  
 여부는 응용 프로그램은 ODBC 2를 나타냅니다. *x* 동작 또는 ODBC 3. *x* 동작은 SQL_ATTR_ODBC_VERSION 환경 특성에 의해 결정 됩니다. 이 32 비트 값은 ODBC 2 보이게 SQL_OV_ODBC2에 설정 됩니다. *x* 동작과 SQL_OV_ODBC3 보이게 ODBC 3. *x* 동작 합니다.  
  
 호출 하 여 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되어 **SQLSetEnvAttr**합니다. 응용 프로그램 호출 **SQLAllocHandle** 호출 해야 환경 핸들을 할당할**SQLSetEnvAttr** 필요 동작을 설정 하는 즉시 합니다. (결과적으로, 상태가 새 환경 versionless에 할당 되지만 환경 핸들을 설명 하기 위해 상태입니다.) 자세한 내용은 참조 하세요. [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
 응용 프로그램 동작 SQL_ATTR_ODBC_VERSION 환경 특성 있지만 특성을 사용 하 여 필요는 ODBC 2를 사용 하 여 응용 프로그램의 연결에 영향을 주지 알려 줍니다. *x* 또는 ODBC 3. *x* 드라이버입니다. ODBC 3입니다. *x* 는 ODBC 2 응용 프로그램에 연결할 수 있습니다. *x* 또는 3. *x* 환경 특성의 설정에 관계 없이 드라이버입니다.  
  
 ODBC 3입니다. *x* 응용 프로그램을 호출 하지 말아야 **SQLAllocEnv**합니다. 결과적으로 드라이버 관리자에 대 한 호출을 받으면 **SQLAllocEnv**에 ODBC 2 응용 프로그램 인식. *x* 응용 프로그램입니다.  
  
 SQL_ATTR_ODBC_VERSION 특성에는 ODBC 3의 세 가지 측면을 영향을 줍니다. *x* 드라이버의 동작:  
  
-   SQLSTATE  
  
-   날짜, 시간 및 타임 스탬프에 대 한 데이터 형식  
  
-   합니다 *CatalogName* 에서 인수 **SQLTables** ODBC 3의 검색 패턴을 허용 합니다. *x*에 있지만 ODBC 2. *x*  
  
 SQL_ATTR_ODBC_VERSION 환경 특성의 설정에 영향을 주지 않습니다 **SQLSetParam** 하거나 **SQLBindParam**합니다. **SQLColAttribute** 도 영향을 받지이 비트입니다. 하지만 **SQLColAttribute** 영향을 받는 특성을 반환 합니다. ODBC 버전입니다 (날짜 형식, 정밀도, 배율 및 길이), 의도 된 동작의 값에 의해 결정 되는 *FieldIdentifier*인수. 때 *FieldIdentifier* SQL_DESC_TYPE, 같으면 **SQLColAttribute** ODBC 3을 반환 합니다. *x* 날짜, 시간 및 타임 스탬프;에 대 한 코드 때 *FieldIdentifier* SQL_COLUMN_TYPE, 같으면 **SQLColAttribute** ODBC 2를 반환 합니다. *x* 날짜, 시간 및 타임 스탬프에 대 한 코드입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLSTATE 매핑](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 데이터 형식 변경](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
