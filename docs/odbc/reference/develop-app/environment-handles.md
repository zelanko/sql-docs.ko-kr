---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409b2c14282238766457d349287f65d90fe463b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114317"
---
# <a name="environment-handles"></a>환경 핸들
*환경* 데이터에 액세스 하는 전역 컨텍스트가 환경과 관련 된 정보는 본질적으로 전역 같은:  
  
-   환경 상태  
  
-   현재 환경 수준 진단  
  
-   현재 환경에 할당 된 연결의 핸들  
  
-   각 환경 특성의 현재 설정  
  
 환경 핸들을 ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드 부분 내에서이 정보를 포함 하도록 구조를 식별 합니다.  
  
 환경 핸들 ODBC 응용 프로그램에서 자주 사용 되지 않습니다. 에 대 한 호출에서 항상 사용 됩니다 **SQLDataSources** 하 고 **SQLDrivers** 에 대 한 호출에 사용 되 고 **SQLAllocHandle**를 **SQLEndTran**, **SQLFreeHandle**하십시오 **SQLGetDiagField**, 및 **SQLGetDiagRec**합니다.  
  
 ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드의 각 부분에는 하나 이상의 환경 핸들이 포함 되어 있습니다. 예를 들어 드라이버 관리자에 연결 된 각 응용 프로그램에 대 한 별도 환경 핸들을 유지 합니다. 사용 하 여 환경 핸들 할당 됩니다 **SQLAllocHandle** 및 사용 하 여 해제 된 **SQLFreeHandle**합니다.
