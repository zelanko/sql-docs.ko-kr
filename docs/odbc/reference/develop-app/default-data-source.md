---
title: 데이터 원본 기본 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b756f9b553c622028266d1fc591596bf58ddf45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="default-data-source"></a>기본 데이터 원본
드라이버는 데이터 소스에 없는 응용 프로그램이 명시적으로 하나 지정 하지 않으면 특정 한 경우에는 기본 데이터 소스 라는 선택할 수 있습니다.  
  
-   에 대 한 호출에서 **SQLConnect** 여기서는 *ServerName* 인수는 길이가 0 인 문자열, null 포인터 또는 DEFAULT입니다.  
  
-   에 대 한 호출에서 **SQLDriverConnect** 여기서 *InConnectionString* 중 하나를 지정 **DSN**= 기본값 또는 사용 하 여 지정 된 **DSN** 키워드는 시스템 정보에 포함 되지 않은 데이터 원본입니다.  
  
 드라이버 정의 된 기본 데이터 원본을 지정 하는 방법 이 관리 작업에 포함 될 수 있습니다 및 사용자에 따라 달라질 수 있습니다.
