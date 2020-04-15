---
title: 드라이버 관리자 오류 및 경고 검사 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee8a0f5ebfac8b6f87281806f07989f4980eb9b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305786"
---
# <a name="driver-manager-error-and-warning-checks"></a>드라이버 관리자 오류 및 경고 검사
드라이버 관리자는 여러 기능을 완전히 또는 부분적으로 구현하므로 해당 함수의 오류 및 경고 전부 또는 일부를 확인합니다.  
  
-   드라이버 관리자는 **SQLDataSource** 및 **SQLDriver를** 구현하고 이러한 함수의 모든 오류 및 경고를 확인합니다.  
  
-   드라이버 관리자는 드라이버가 **SQLGetFunctions를**구현하는지 여부를 확인합니다. 드라이버가 **SQLGetFunctions를**구현하지 않는 경우 드라이버 관리자는 모든 오류 및 경고를 구현하고 확인합니다.  
  
-   드라이버 관리자는 **SQLAllocHandle,** **SQLDriverConnect, SQLDriverConnect,** **SQLConnect** **SQLFreeHandle,** **SQLGetDiagRec 및 SQLGetDiagField**및 **SQLGetDiagField를** 부분적으로 구현하고 이러한 함수의 일부 오류를 확인합니다. **SQLBrowseConnect** 둘 다 유사한 작업을 수행하기 때문에 이러한 함수 중 일부에 대해 드라이버와 동일한 오류를 반환할 수 있습니다. 예를 들어 드라이버 관리자 또는 드라이버는 **SQLDriverConnect**에 대한 로그인 대화 상자를 표시할 수 없는 경우 SQLSTATE IM008(대화 기록 실패)을 반환할 수 있습니다.
