---
title: 연결 핸들 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab8b94835fb9a6103436026a669c86f2401d57b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036434"
---
# <a name="connection-handles"></a>연결 핸들
A *연결* 드라이버 및 데이터 원본으로 구성 됩니다. 연결 핸들을 각 연결을 식별합니다. 연결 핸들을 사용 하는 드라이버 뿐만 아니라 해당 드라이버를 사용 하는 데이터 원본을 정의 합니다. ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드의 세그먼트를 내 연결 핸들을 다음과 같은 연결 정보를 포함 하는 구조를 식별 합니다.  
  
-   연결의 상태  
  
-   현재 연결 수준 진단  
  
-   문 및 연결에 현재 할당 된 설명자 핸들  
  
-   각 연결 특성의 현재 설정  
  
 ODBC는 드라이버를 지 원하는 경우 여러 개의 동시 연결을 방지 하지 않습니다. 따라서 특정 ODBC 환경에서 여러 연결 핸들은 다양 한 데이터 원본 또는 데이터 원본 및 동일한 드라이버에 여러 연결에도 다양 한 드라이버 및 데이터 원본과 동일한 드라이버를 가리킬 수 있습니다. 일부 드라이버 지; 활성 연결 수를 제한 합니다. 옵션은 SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo** 특정 드라이버에서 지 원하는 활성 연결 수를 지정 합니다.  
  
 연결 핸들을 데이터 원본에 연결할 때 주로 사용 됩니다 (**SQLConnect**하십시오 **SQLDriverConnect**, 또는 **SQLBrowseConnect**), 데이터에서 연결 끊기 원본 (**SQLDisconnect**), 드라이버 및 데이터 원본에 대 한 정보 가져오기 (**SQLGetInfo**), 진단 검색 (**SQLGetDiagField** 및 **SQLGetDiagRec**), 트랜잭션을 수행 하 고 (**SQLEndTran**). 설정 하 고 연결 특성을 가져오는 경우 에서도 사용 됩니다 (**SQLSetConnectAttr** 하 고 **SQLGetConnectAttr**) 및 SQL 문의 네이티브 형식으로 가져올 때 (**SQLNativeSql** ).  
  
 사용 하 여 연결 핸들 할당 됩니다 **SQLAllocHandle** 및 사용 하 여 해제 된 **SQLFreeHandle**합니다.
