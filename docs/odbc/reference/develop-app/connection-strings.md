---
title: 연결 문자열 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbbb5b4672a8ea393380063887cfd77b3e910238
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299033"
---
# <a name="connection-strings"></a>연결 문자열
연결 문자열에는 연결을 설정하는 데 사용되는 정보가 포함되어 있습니다. 전체 연결 문자열에는 연결을 설정하는 데 필요한 모든 정보가 포함됩니다. 연결 문자열은 세미콜론으로 구분된 일련의 키워드/값 쌍입니다. 연결 문자열의 전체 구문은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조하십시오. 연결 문자열은 다음에서 사용됩니다.  
  
-   **SQLDriverConnect는**사용자와의 상호 작용에 의해 연결 문자열을 완료합니다.  
  
-   **SQLBrowseConnect는**데이터 원본을 사용하여 반복적으로 연결 문자열을 완료합니다.  
  
 **SQLConnect는** 연결 문자열을 사용하지 않습니다. **SQLConnect를** 사용하는 것은 정확히 세 개의 키워드/값 쌍(데이터 원본 이름 및 선택적으로 사용자 ID 및 암호)이 있는 연결 문자열을 사용하여 연결하는 것과 유사합니다.
