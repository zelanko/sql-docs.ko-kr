---
title: 환경 핸들 | Microsoft Docs
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
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffbc2ed4c1c496833237c3bda6d6e2c306a50cac
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="environment-handles"></a>환경 핸들
*환경* 에이 데이터에 액세스할 수 있는 전역 컨텍스트는는 환경에 연결 된와 같은 전역 특성에는 모든 정보:  
  
-   환경 상태  
  
-   현재 환경 수준 진단  
  
-   현재 환경에 할당 된 연결의 핸들  
  
-   각 환경 특성의 현재 설정  
  
 환경 핸들의 ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드 조각 내에서이 정보를 포함 하는 구조를 식별 합니다.  
  
 환경 핸들 ODBC 응용 프로그램에서 자주 사용 되지 않습니다. 에 대 한 호출에서 사용 하는 항상 **SQLDataSources** 및 **SQLDrivers** 에 대 한 호출에 자주 사용 하 고 **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**, 및 **SQLGetDiagRec**합니다.  
  
 각 ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드 조각에는 하나 이상의 환경 핸들을 포함 합니다. 예를 들어 드라이버 관리자 연결 된 각 응용 프로그램에 대 한 별도 환경 핸들을 유지 합니다. 사용 하 여 환경 핸들 할당은 **SQLAllocHandle** 로 해제 및 **SQLFreeHandle**합니다.
