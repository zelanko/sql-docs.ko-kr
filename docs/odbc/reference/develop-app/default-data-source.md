---
title: 기본 데이터 원본 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305994"
---
# <a name="default-data-source"></a>기본 데이터 원본
응용 프로그램에서 명시적으로 지정 하지 않는 특정 한 경우 드라이버는 기본 데이터 원본 이라는 데이터 원본을 선택할 수 있습니다.  
  
-   *ServerName* 인수가 길이가 0 인 문자열, null 포인터 또는 DEFAULT 인 **SQLConnect** 를 호출 합니다.  
  
-   **SQLDriverConnect** 에 대 한 호출에서 *inconnectionstring* 은 **dsn**= DEFAULT를 지정 하거나 시스템 정보에 포함 되지 않은 데이터 원본을 **dsn** 키워드를 사용 하 여 지정 합니다.  
  
 기본 데이터 원본을 지정 하는 방법에 대 한 드라이버 정의입니다. 여기에는 관리 작업이 포함 될 수 있으며 사용자에 따라 달라질 수 있습니다.
