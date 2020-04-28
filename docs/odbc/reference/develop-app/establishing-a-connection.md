---
title: 연결 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establishing a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establishing a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f71190a8a2ca1dd8af0d28adb5531540fb1b57e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298703"
---
# <a name="establishing-a-connection"></a>연결 설정
환경 및 연결 핸들을 할당 하 고 연결 특성을 설정 하 고 나면 응용 프로그램은 데이터 원본 또는 드라이버에 연결할 준비가 된 것입니다. 응용 프로그램에서이 작업을 수행 하는 데 사용할 수 있는 세 가지 함수는 **SQLConnect** (핵심 인터페이스 규칙 수준), **SQLDriverConnect** (core) 및 **SQLBrowseConnect** (수준 1)입니다. 각각의 세 가지는 다른 시나리오에서 사용 하도록 설계 되었습니다. 연결 하기 전에 응용 프로그램은 **sqldrivers**에서 반환 된 **connectfunctions** 키워드를 사용 하 여 지원 되는 함수를 결정할 수 있습니다.  
  
> [!NOTE]  
>  일부 드라이버는 지원 되는 활성 연결 수를 제한 합니다. 응용 프로그램은 SQL_MAX_DRIVER_CONNECTIONS 옵션으로 **SQLGetInfo** 를 호출 하 여 특정 드라이버에서 지 원하는 활성 연결 수를 확인 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기본 데이터 원본](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [SQLConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [연결 문자열](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [SQLDriverConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [SQLBrowseConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
