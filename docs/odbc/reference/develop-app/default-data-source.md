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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 909f9b3e7c8087add8eb66ca2f5c15253026304c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267646"
---
# <a name="default-data-source"></a>기본 데이터 원본
드라이버는 기본 데이터 원본 특정 응용 프로그램 않습니다 하지 명시적으로 지정 하는 경우 하나에서 데이터 원본을 선택할 수 있습니다.  
  
-   에 대 한 호출에서 **SQLConnect** 여기서 합니다 *ServerName* 인수가 길이가 0 인 문자열로, null 포인터 이거나 기본입니다.  
  
-   호출에서 **SQLDriverConnect** 여기서 *InConnectionString* 지정 하거나 **DSN**= DEFAULT 또는 사용 하 여 지정 합니다 **DSN** 키워드는 시스템 정보에 포함 되지 않은 데이터 원본입니다.  
  
 이 경우 드라이버에서 정의 된 기본 데이터 원본을 지정 하는 방법을 이 관리 작업을 포함할 수 있습니다 하 고 사용자에 따라 달라질 수 있습니다.
