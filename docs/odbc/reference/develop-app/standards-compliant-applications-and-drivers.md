---
title: 표준 규격 응용 프로그램 및 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4980cfe64a5a8e8404c6b5b0bdc8b1aba484f0c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107327"
---
# <a name="standards-compliant-applications-and-drivers"></a>표준 준수 애플리케이션 및 드라이버
표준 규격 응용 프로그램 또는 드라이버는 Open Group CAE Specification "데이터 관리: SQL 호출 수준 인터페이스 (CLI)" 및 ISO/IEC 9075-3:1995 (E) 호출 수준 인터페이스 (SQL/CLI)를 준수 하는 응용 프로그램 또는 드라이버입니다.  
  
 ODBC 3.x는 다음과 같은 기능을 *보장 합니다.*  
  
-   Open Group 및 ISO CLI 사양에 작성 된 응용 프로그램 *은 odbc 3.x* 드라이버를 사용 하 여 컴파일되고 *, odbc 2.x 라이브러리와* 연결 된 경우 *및 odbc 3.x 드라이버 관리자* 를 통해 드라이버에 대 한 액세스 권한을 얻는 경우에 사용 *됩니다.*  
  
-   Open Group 및 ISO CLI 사양에 작성 된 드라이버는 odbc *3.x 응용 프로그램* 또는 표준 규격 응용 프로그램 *에서 odbc 2.x 헤더 파일* 을 사용 하 여 *컴파일되고 odbc 3.x 라이브러리에* 연결 된 경우와 응용 프로그램이 odbc *2.x 드라이버 관리자를 통해 드라이버에* 액세스할 수 있는 경우에 작동 합니다.  
  
 표준 규격 응용 프로그램 및 드라이버는 ODBC_STD 컴파일 플래그를 사용 하 여 컴파일됩니다.  
  
 표준 규격 응용 프로그램은 다음과 같은 동작을 수행 합니다.  
  
-   표준 규격 응용 프로그램이 **sqlallocenv** ( **sqlallocenv** 가 OPEN Group 및 ISO CLI의 올바른 함수 이기 때문에 발생할 수 있음)를 호출 하는 경우 호출은 컴파일 시간에 **SQLAllocHandleStd** 에 매핑됩니다. 따라서 런타임에 응용 프로그램은 **SQLAllocHandleStd**를 호출 합니다. 이 호출을 처리 하는 동안 드라이버 관리자는 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC3로 설정 합니다. **SQLAllocHandleStd** 를 호출 하는 것은 SQL_HANDLE_ENV **SQLAllocHandle** *에 대 한* 호출 및 SQL_ATTR_ODBC_VERSION를 SQL_OV_ODBC3로 설정 하기 위한 **SQLSetEnvAttr** 호출에 해당 합니다.  
  
-   표준 규격 응용 프로그램이 **sqlbindparam 함수와** ( **Sqlbindparam 함수와** 가 OPEN Group 및 ISO CLI의 올바른 함수 이기 때문에 발생할 수 있음)를 호출 하는 *경우 ODBC 3.x* 드라이버 관리자는 호출을 **SQLBindParameter**의 해당 호출에 매핑합니다. (이전 버전과의 호환성을 위해 부록 G: 드라이버 지침의 [Sqlbindparam 함수와 매핑](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) 을 참조 하세요.)  
  
-   ISO CLI를 사용 하 여 정렬 하기 위해 *ODBC 2.x* 헤더 파일은 **SQLGetInfo**호출에 사용 되는 정보 형식에 대 한 별칭을 포함 합니다. 표준 규격 응용 프로그램은 ODBC *3(sp3)* 정보 형식 대신 이러한 별칭을 사용할 수 있습니다. 자세한 내용은 다음 항목인 [헤더 파일](../../../odbc/reference/develop-app/header-files.md)을 참조 하세요.  
  
-   표준 규격 응용 프로그램은 지원 되는 모든 기능이 작동 하는 드라이버에서 지원 되는지 확인 해야 합니다. SQL_ATTR_CURSOR_SCROLLABLE statement 특성을 SQL_SCROLLABLE로 설정 하 고 SQL_ATTR_CURSOR_SENSITIVITY 문 특성을 SQL_INSENSITIVE 또는 SQL_SENSITIVE로 설정 하면 표준에서 선택적 기능으로 사용할 수 있지만 ODBC *2.X 코어 수준* 에는 포함 되지 않으므로 모든 odbc *3.x 드라이버에서* 지원 되지 않을 수 있습니다. 표준 규격 응용 프로그램에서 이러한 기능을 사용 하는 경우 작동 하는 드라이버가 해당 기능을 지원 하는지 확인 해야 합니다.
