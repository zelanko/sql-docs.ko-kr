---
title: SQL드라이버커넥트연결 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6cd95364d8a5316a50d9f55616236a8677bf99e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299073"
---
# <a name="connecting-with-sqldriverconnect"></a>SQLDriverConnect로 연결
**SQLDriverConnect는** 연결 문자열을 사용하여 데이터 원본에 연결하는 데 사용됩니다. **SQLDriverConnect는** 다음과 같은 이유로 **SQLConnect** 대신 사용됩니다.  
  
-   응용 프로그램에서 드라이버 관련 연결 정보를 사용하도록 합니다.  
  
-   드라이버가 연결 정보를 묻는 메시지를 사용자에게 표시하도록 하려는 경우  
  
-   데이터 원본을 지정하지 않고 연결합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [드라이버별 연결 정보](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [사용자에게 연결 정보 요청](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [파일 데이터 원본을 사용하여 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [드라이버에 직접 연결](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
