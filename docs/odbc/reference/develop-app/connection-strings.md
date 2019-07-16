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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036417"
---
# <a name="connection-strings"></a>연결 문자열
연결을 설정 하는 데 사용 되는 정보를 포함 하는 연결 문자열입니다. 전체 연결 문자열을 연결 하는 데 필요한 모든 정보를 포함 합니다. 연결 문자열은 일련의 키워드/값 쌍을 세미콜론으로 구분 합니다. (연결 문자열의 전체 구문에 대 한 참조를 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.) 연결 문자열에서 사용 됩니다.  
  
-   **SQLDriverConnect**, 사용자 상호 작용 하 여 연결 문자열을 완료 하는 합니다.  
  
-   **SQLBrowseConnect**를 반복적으로 데이터 원본 연결 문자열을 완료 하는 합니다.  
  
 **SQLConnect** 사용 하 여; 연결 문자열을 사용 하지 않습니다 **SQLConnect** 정확히 세 개의 키워드/값 쌍을 사용 하 여 연결 문자열을 사용 하 여 연결 비슷합니다 (데이터 원본 이름 및 필요에 따라 사용자에 대 한 ID 및 암호) .
