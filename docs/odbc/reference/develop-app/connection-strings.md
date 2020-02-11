---
title: 연결 문자열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f68a87db729df2f4a27e2766a9de60e8c75a71a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036417"
---
# <a name="connection-strings"></a>연결 문자열
연결 문자열은 연결을 설정 하는 데 사용 되는 정보를 포함 합니다. 전체 연결 문자열에는 연결을 설정 하는 데 필요한 모든 정보가 포함 됩니다. 연결 문자열은 세미콜론으로 구분 된 일련의 키워드/값 쌍입니다. (연결 문자열의 전체 구문은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조 하세요.) 연결 문자열은 다음에서 사용 됩니다.  
  
-   **SQLDriverConnect**는 사용자와의 상호 작용을 통해 연결 문자열을 완성 합니다.  
  
-   **SQLBrowseConnect**-데이터 원본으로 반복적으로 연결 문자열을 완성 합니다.  
  
 **SQLConnect** 는 연결 문자열을 사용 하지 않습니다. **SQLConnect** 를 사용 하는 것은 정확히 세 개의 키워드/값 쌍이 있는 연결 문자열을 사용 하 여 연결 하는 것과 유사 합니다 (데이터 원본 이름 및 선택적으로 사용자 ID 및 암호).
