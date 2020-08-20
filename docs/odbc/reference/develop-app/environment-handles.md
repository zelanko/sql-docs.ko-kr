---
description: 환경 핸들
title: 환경 핸들 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa22a89288f4dd5a8400484078f57b60fc135fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461505"
---
# <a name="environment-handles"></a>환경 핸들
*환경은* 데이터에 액세스할 수 있는 전역 컨텍스트입니다. 환경에 연결 된 것은 다음과 같이 본질적으로 전체적으로 사용 되는 모든 정보입니다.  
  
-   환경 상태  
  
-   현재 환경 수준 진단  
  
-   환경에 현재 할당 된 연결의 핸들입니다.  
  
-   각 환경 특성의 현재 설정  
  
 ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드 조각 내에서 환경 핸들은이 정보를 포함 하는 구조를 식별 합니다.  
  
 환경 핸들은 ODBC 응용 프로그램에서 자주 사용 되지 않습니다. **Sqldatasources 원본** 및 **sqldatasources** 에 대 한 호출에서 항상 사용 되며 경우에 따라 **SQLAllocHandle**, **sqlendtran**, **sqlfreehandle**, **SQLGetDiagField**및 **SQLGetDiagRec**에 대 한 호출에 사용 됩니다.  
  
 ODBC를 구현 하는 각 코드 조각 (드라이버 관리자 또는 드라이버)에는 하나 이상의 환경 핸들이 포함 됩니다. 예를 들어 드라이버 관리자는 연결 된 각 응용 프로그램에 대해 별도의 환경 핸들을 유지 관리 합니다. 환경 핸들은 **SQLAllocHandle** 를 사용 하 여 할당 되 고 **sqlfreehandle**을 사용 하 여 해제 됩니다.
