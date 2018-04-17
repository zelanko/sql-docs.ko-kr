---
title: 드라이버 관리자 오류 및 경고 확인 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f212af4169b4c0be2a840f6ff8d7310abb40f53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="driver-manager-error-and-warning-checks"></a>드라이버 관리자 오류 및 경고 확인
드라이버 관리자는 완전히 또는 부분적으로 다양 한 기능을 구현 하 고 오류 및 해당 함수에는 경고의 전체 또는 일부 따라서 검사 합니다.  
  
-   드라이버 관리자를 사용 하는 구현 **SQLDataSources** 및 **SQLDrivers** 및 모든 오류와 이러한 함수에 대 한 경고를 확인 합니다.  
  
-   드라이버 관리자는 드라이버를 구현 하는지 확인 **SQLGetFunctions**합니다. 드라이버를 구현 하지 않는 경우 **SQLGetFunctions**, 드라이버 관리자를 구현 하 고 모든 오류 및 경고에 대 한 확인 합니다.  
  
-   드라이버 관리자를 사용 하는 부분적으로 구현 **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**,  **SQLFreeHandle**, **SQLGetDiagRec**, 및 **SQLGetDiagField** 및 이러한 함수에 일부 오류를 확인 합니다. 드라이브와 같은 오류가 모두 유사한 작업을 수행 하기 때문에 이러한 함수 중 일부에 대해 반환할 수 있습니다. 드라이버 관리자 또는 드라이버 SQLSTATE IM008를 반환할 수 있습니다 예를 들어 (실패 대화 상자) 경우에 대 한 로그인 대화 상자를 표시할 수 없으면 하나 **SQLDriverConnect**합니다.
