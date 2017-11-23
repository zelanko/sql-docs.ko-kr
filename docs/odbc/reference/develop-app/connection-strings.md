---
title: "연결 문자열 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to driver [ODBC], connection strings
- functions [ODBC], data source or driver connections
- connection strings [ODBC], about connection strings
- connecting to data source [ODBC], connection strings
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: 724c7b86-300a-4fa9-ad96-4afa0fdcb3e9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 99c0ebcad365396bd2ebab2d03df4cb6a6627003
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="connection-strings"></a>연결 문자열
연결 문자열을 연결 구성에 사용 되는 정보를 포함 합니다. 전체 연결 문자열을 연결을 설정 하는 데 필요한 모든 정보를 포함 합니다. 연결 문자열은 일련의 세미콜론으로 구분 하는 키워드/값 쌍입니다. (연결 문자열의 전체 구문을 참조 하십시오.는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.) 연결 문자열에서 사용 됩니다.  
  
-   **SQLDriverConnect**, 사용자와 상호 작용 하 여 연결 문자열을 마칩니다.  
  
-   **SQLBrowseConnect**, 연결 문자열은 데이터 소스와 반복적으로 마칩니다.  
  
 **SQLConnect** 연결 문자열을 사용 하지 않습니다; 사용 하 여 **SQLConnect** 는 정확히 세 개의 키워드/값 쌍으로 연결 문자열을 사용 하 여 연결 하는 것과 유사 (데이터 원본 이름 및 필요에 따라 사용자 ID와 암호) .
