---
description: 동작 변경 및 ODBC 3.x 드라이버
title: 동작 변경 내용 및 ODBC 3.x 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43f64aa4b627130308ea920918c2de6d98116020
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411339"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>동작 변경 및 ODBC 3.x 드라이버
환경 특성 SQL_ATTR_ODBC_VERSION *은 odbc 2.x* 동작 또는 odbc *2.x 동작을* 표시 해야 하는지 여부를 드라이버에 나타냅니다. SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하는 방법은 응용 프로그램에 따라 달라 집니다. ODBC *3.x 응용 프로그램은* **SQLSetEnvAttr** 를 호출 하 여 환경 핸들을 할당 한 후 **SQLAllocHandle** 를 호출 하 여 연결 핸들을 할당 하기 전에 **SQLAllocHandle** 를 호출 하 여이 특성을 설정 해야 합니다. 이 작업을 수행 하는 데 실패 하는 경우 드라이버 관리자는 **SQLAllocHandle**에 대 한 후자의 호출에서 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다.  
  
> [!NOTE]  
>  동작 변경 내용과 응용 프로그램의 작동 방식에 대 한 자세한 내용은 [동작 변경](../../../odbc/reference/develop-app/behavioral-changes.md)을 참조 하세요.  
  
 Odbc 2.x 헤더 파일을 사용 하 여 다시 *컴파일된 odbc 2.x 응용 프로그램 및* odbc 2.x *응용 프로그램은* **SQLSetEnvAttr**를 호출 하지 *않습니다.* 그러나 **SQLAllocHandle** 대신 **sqlallocenv** 를 호출 하 여 환경 핸들을 할당 합니다. 따라서 응용 프로그램이 드라이버 관리자에서 **Sqlallocenv** 를 호출 하면 드라이버 관리자는 드라이버에서 **SQLAllocHandle** 및 **SQLSetEnvAttr** 를 호출 합니다. 따라서 ODBC 2.x 드라이버는 설정 되는이 특성에서 항상 수 *있습니다.*  
  
 ODBC_STD compile 플래그를 사용 하 여 컴파일된 표준 규격 응용 프로그램이 **Sqlallocenv** 를 호출 하는 경우 (ISO **allocenv** 가 ISO에서 사용 되지 않기 때문에 발생할 수 있음) 호출은 컴파일 시간에 **SQLAllocHandleStd** 에 매핑됩니다. 런타임에 응용 프로그램은 **SQLAllocHandleStd**를 호출 합니다. 드라이버 관리자는 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC3로 설정 합니다. **SQLAllocHandleStd** 를 호출 하는 것은 SQL_HANDLE_ENV **SQLAllocHandle** *에 대 한* 호출 및 SQL_ATTR_ODBC_VERSION를 SQL_OV_ODBC3로 설정 하기 위한 **SQLSetEnvAttr** 호출에 해당 합니다.  
  
 특정 드라이버 아키텍처에서 드라이버는 연결에 *따라 odbc 2.x 드라이버 또는* *odbc 2.x* 드라이버로 표시 되어야 합니다 (예를 들어, 이 경우 드라이버는 실제로 드라이버가 아니지만 드라이버 관리자와 다른 드라이버 사이에 있는 계층이 될 수 있습니다. 예를 들어 ODBC Spy와 같은 드라이버를 모방할 수 있습니다. 또 다른 예로, a p/SQL과 같은 게이트웨이의 역할을 할 수 있습니다. ODBC *3. x* 드라이버로 표시 하려면 이러한 드라이버가 **SQLALLOCHANDLE**을 *내보내고 odbc 2.X* 드라이버로 표시 되도록 하려면 **sqlallocconnect**, **sqlallocconnect**및 **sqlallocconnect**를 내보낼 수 있어야 합니다. 환경, 연결 또는 문을 할당 해야 하는 경우 드라이버 관리자는이 드라이버가 **SQLAllocHandle**을 내보내도록 확인 합니다. 드라이버가 수행 하므로 드라이버 관리자는 드라이버에서 **SQLAllocHandle** 를 호출 합니다. 드라이버가 ODBC 2.x 드라이버를 사용 하는 *경우 드라이버는* **SQLAllocHandle** 에 대 한 호출을 **sqlallocconnect**, **sqlallocconnect**또는 **sqlallocconnect**에 적절 하 게 매핑해야 합니다. 또한 *가 ODBC 2.x* 드라이버로 동작할 때 **SQLSetEnvAttr** 호출을 사용 하 여 아무 작업도 수행 하지 않아야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Datetime 데이터 형식](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 데이터 형식의 이전 버전과의 호환성](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [고정 길이 책갈피](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 지원](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [SQL_NO_DATA 반환](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [SQLSetPos를 호출하여 데이터 삽입](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [서수로 로딩](../../../odbc/reference/appendixes/loading-by-ordinal.md)
