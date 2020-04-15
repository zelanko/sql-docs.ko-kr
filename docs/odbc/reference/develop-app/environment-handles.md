---
title: 환경 핸들 | 마이크로 소프트 문서
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
ms.openlocfilehash: b504995e99dfad032598485e370b4d5a6681ae81
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300443"
---
# <a name="environment-handles"></a>환경 핸들
*환경은* 데이터에 액세스하는 전역 컨텍스트입니다. 환경과 연관된 정보는 다음과 같이 본질적으로 글로벌한 정보입니다.  
  
-   환경의 상태  
  
-   현재 환경 수준 진단  
  
-   환경에 현재 할당된 연결 핸들  
  
-   각 환경 특성의 현재 설정  
  
 ODBC(드라이버 관리자 또는 드라이버)를 구현하는 코드 내에서 환경 핸들은 이 정보를 포함하는 구조를 식별합니다.  
  
 환경 핸들은 ODBC 응용 프로그램에서 자주 사용되지 않습니다. 항상 **SQLDataSource** 및 **SQLDriver에** 대한 호출에 사용되며 **SQLAllocHandle,** **SQLEndTran**, **SQLFreeHandle,** **SQLGetDiagField**및 **SQLGetDiagRec**에 대한 호출에 사용됩니다.  
  
 ODBC(드라이버 관리자 또는 드라이버)를 구현하는 각 코드에는 하나 이상의 환경 핸들이 포함되어 있습니다. 예를 들어 드라이버 관리자는 연결된 각 응용 프로그램에 대해 별도의 환경 핸들을 유지 관리합니다. 환경 핸들은 **SQLAllocHandle으로** 할당되고 **SQLFreeHandle**.
