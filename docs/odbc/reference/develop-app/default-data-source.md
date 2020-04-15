---
title: 기본 데이터 원본 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 978362b7dfe92d1333f83be684f6326cf25dd69b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305994"
---
# <a name="default-data-source"></a>기본 데이터 원본
드라이버는 응용 프로그램이 명시적으로 하나를 지정하지 않는 경우에 기본 데이터 원본이라고 하는 데이터 원본을 선택할 수 있습니다.  
  
-   *ServerName* 인수가 0 길이 문자열, null 포인터 또는 DEFAULT인 **SQLConnect를** 호출합니다.  
  
-   *InConnectionString이* **DSN**=DEFAULT를 지정하거나 **DSN** 키워드로 시스템 정보에 포함되지 않은 데이터 원본을 지정하는 **SQLDriverConnect를** 호출합니다.  
  
 기본 데이터 원본을 지정하는 방법은 드라이버 정의입니다. 여기에는 관리 작업이 포함될 수 있으며 사용자에 따라 달라질 수 있습니다.
