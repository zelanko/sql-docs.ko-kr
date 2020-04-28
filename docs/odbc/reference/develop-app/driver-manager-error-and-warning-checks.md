---
title: 드라이버 관리자 오류 및 경고 검사 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305786"
---
# <a name="driver-manager-error-and-warning-checks"></a>드라이버 관리자 오류 및 경고 검사
드라이버 관리자는 여러 함수를 완전히 또는 부분적으로 구현 하므로 이러한 함수에서 오류 및 경고의 일부 또는 전부를 확인 합니다.  
  
-   드라이버 관리자는 **Sqldatasources 원본** 및 **sqldatasources** 를 구현 하 고 이러한 함수에서 모든 오류 및 경고를 확인 합니다.  
  
-   드라이버 관리자는 드라이버가 **SQLGetFunctions**를 구현 하는지 여부를 확인 합니다. 드라이버에서 **SQLGetFunctions**를 구현 하지 않는 경우 드라이버 관리자는을 구현 하 고 모든 오류 및 경고를 확인 합니다.  
  
-   드라이버 관리자는 **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**, **sqlfreehandle**, **SQLGetDiagRec**및 **SQLGetDiagField** 을 부분적으로 구현 하 고 이러한 함수에서 일부 오류가 있는지 확인 합니다. 이러한 기능 중 일부에 대 한 드라이버와 동일한 오류를 반환할 수 있습니다 .이는 모두 유사한 작업을 수행 하기 때문입니다. 예를 들어, **SQLDriverConnect**에 대 한 로그인 대화 상자를 표시할 수 없는 경우 드라이버 관리자 또는 드라이버가 SQLSTATE IM008 (대화 상자 실패)를 반환할 수 있습니다.
