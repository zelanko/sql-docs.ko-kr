---
title: 연결 설정 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298703"
---
# <a name="establishing-a-connection"></a>연결 설정
환경 및 연결 핸들을 할당하고 연결 특성을 설정하면 응용 프로그램이 데이터 원본 또는 드라이버에 연결할 준비가 된 것입니다. 응용 프로그램에서 이 작업을 수행하는 데 사용할 수 있는 세 가지 기능은 **SQLConnect(코어** 인터페이스 적합성 수준), **SQLDriverConnect(코어),** **SQLBrowseConnect(수준** 1)의 세 가지 다른 함수입니다. 세 가지 각각은 서로 다른 시나리오에서 사용되도록 설계되었습니다. 연결하기 전에 응용 프로그램은 **SQLDriver에서**반환되는 **ConnectFunctions** 키워드로 지원되는 함수를 결정할 수 있습니다.  
  
> [!NOTE]  
>  일부 드라이버는 지원하는 활성 연결 수를 제한합니다. 응용 프로그램은 **SQLGetInfo를** SQL_MAX_DRIVER_CONNECTIONS 옵션으로 호출하여 특정 드라이버가 지원하는 활성 연결 수를 결정합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기본 데이터 원본](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [SQLConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [연결 문자열](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [SQLDriverConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [SQLBrowseConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
