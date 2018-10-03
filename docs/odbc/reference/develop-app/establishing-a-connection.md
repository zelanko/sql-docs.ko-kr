---
title: 에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70f459f60616e7edd77078a7e9653ab9dff097e9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606383"
---
# <a name="establishing-a-connection"></a>연결 설정
환경 및 연결 핸들을 할당 하 고 모든 연결 특성을 설정, 후 응용 프로그램 데이터 원본 또는 드라이버에 연결할 준비가 되었습니다. 응용 프로그램이이 작업을 수행 하 여 다른 함수는 세 가지가: **SQLConnect** (핵심 인터페이스 적합성 수준), **SQLDriverConnect** (코어), 및 **SQLBrowseConnect**(수준 1). 각 세 가지 다른 시나리오에 사용할 설계 되었습니다. 에 연결 하기 전에 응용 프로그램으로는 이러한 함수는 확인할 수는 **ConnectFunctions** 반환한 키워드 **SQLDrivers**합니다.  
  
> [!NOTE]  
>  일부 드라이버 지 활성 연결 수를 제한 합니다. 응용 프로그램 호출 **SQLGetInfo** 활성 연결 수를 확인 하려면 SQL_MAX_DRIVER_CONNECTIONS 옵션을 사용 하 여 특정 드라이버를 지원 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기본 데이터 원본](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [SQLConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [연결 문자열](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [SQLDriverConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [SQLBrowseConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
