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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d0b136b9748de1991888abb0c19bc0d2ac65ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046975"
---
# <a name="driver-manager-error-and-warning-checks"></a>드라이버 관리자 오류 및 경고 검사
드라이버 관리자를 완전히 또는 부분적으로 다양 한 기능을 구현 하 고 오류와 함수에는 경고의 전체 또는 일부 따라서 확인 합니다.  
  
-   드라이버 관리자 구현 **SQLDataSources** 하 고 **SQLDrivers** 및 모든 오류와 이러한 함수에 대 한 경고를 확인 합니다.  
  
-   드라이버 관리자 드라이버를 구현 하는지 여부를 확인 **SQLGetFunctions**합니다. 드라이버를 구현 하지 않는 경우 **SQLGetFunctions**, 드라이버 관리자를 구현 하 고 모든 오류 및 경고를 확인 합니다.  
  
-   드라이버 관리자를 부분적으로 구현 **SQLAllocHandle**, **SQLConnect**를 **SQLDriverConnect**, **SQLBrowseConnect**합니다  **SQLFreeHandle**, **SQLGetDiagRec**, 및 **SQLGetDiagField** 및 이러한 함수에서 일부 오류를 확인 합니다. 둘 다 유사한 작업을 수행 하기 때문에 이러한 함수 중 일부에 대 한 드라이브와 동일한 오류를 반환할 수 있습니다. 드라이버를 드라이버 관리자 SQLSTATE IM008를 반환할 수 있습니다 예를 들어 (실패 대화 상자) 경우에 대 한 로그인 대화 상자를 표시할 수 없는 **SQLDriverConnect**합니다.
