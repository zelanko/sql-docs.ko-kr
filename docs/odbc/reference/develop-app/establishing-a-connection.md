---
title: "연결을 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establising a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establising a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 43e7ab9f883df271f47b0ad55a931ce1a2d2c220
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="establishing-a-connection"></a>연결 설정
환경 및 연결 핸들을 할당 하 고 모든 연결 특성 설정, 후 응용 프로그램 데이터 원본이 나 드라이버에 연결할 준비가 되었습니다. 세 가지 다른 함수가이 작업을 수행 하는 응용 프로그램 צ ְ ײ: **SQLConnect** (인터페이스 규칙 수준은 기본), **SQLDriverConnect** (기본), 및 **SQLBrowseConnect**(수준 1). 세 개의 각 옵션은 서로 다른 시나리오에에서 사용할 하도록 설계 되었습니다. 에 연결 하기 전에 응용 프로그램을 사용할 수 있는 이러한 함수 중 확인할 수는 **ConnectFunctions** 반환한 키워드 **SQLDrivers**합니다.  
  
> [!NOTE]  
>  일부 드라이버의 지원 되는 활성 연결 수를 제한 합니다. 응용 프로그램이 호출 **SQLGetInfo** 활성 연결 수를 결정 하는 SQL_MAX_DRIVER_CONNECTIONS 옵션과 함께 특정 드라이버를 지원 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기본 데이터 원본](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [SQLConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [연결 문자열](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [SQLDriverConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [SQLBrowseConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
