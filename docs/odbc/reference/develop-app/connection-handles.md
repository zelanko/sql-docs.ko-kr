---
title: 연결 핸들 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5b03e0733e35984350d2a218b885dc148ca8f8f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299023"
---
# <a name="connection-handles"></a>연결 핸들
*연결은* 드라이버와 데이터 원본으로 구성됩니다. 연결 핸들은 각 연결을 식별합니다. 연결 핸들은 사용할 드라이버뿐만 아니라 해당 드라이버와 함께 사용할 데이터 원본을 정의합니다. ODBC(드라이버 관리자 또는 드라이버)를 구현하는 코드 세그먼트 내에서 연결 핸들은 다음과 같은 연결 정보를 포함하는 구조를 식별합니다.  
  
-   연결 상태  
  
-   현재 연결 수준 진단  
  
-   연결에 현재 할당된 명령문 및 설명자의 핸들  
  
-   각 연결 특성의 현재 설정  
  
 ODBC는 드라이버가 이를 지원하는 경우 여러 개의 동시 연결을 방지하지 않습니다. 따라서 특정 ODBC 환경에서 여러 연결 핸들은 다양한 드라이버 및 데이터 원본, 동일한 드라이버 및 다양한 데이터 원본 또는 동일한 드라이버 및 데이터 원본에 대한 여러 연결을 가리킬 수 있습니다. 일부 드라이버는 지원하는 활성 연결 수를 제한합니다. **SQLGetInfo의** SQL_MAX_DRIVER_CONNECTIONS 옵션은 특정 드라이버가 지원하는 활성 연결 수를 지정합니다.  
  
 연결 핸들은 주로 데이터**원본(SQLConnect,** **SQLDriverConnect**또는 **SQLBrowseConnect)에**연결할 때 사용되며, 데이터 원본에서 연결을 끊고(SQLGetInfo), 진단**SQLDisconnect**검색(SQLGetDiagField 및 **SQLGetDiagRec),****SQLGetInfo**트랜잭션(SQLEndTran)을 수행합니다.**SQLGetDiagField** **SQLEndTran** 또한 연결**특성(SQLSetConnectAttr** 및 **SQLGetConnectAttr)을**설정하고 가져오는 경우와 SQL 문(SQLNativeSql)의 기본 형식을 가져오는 경우에도 사용됩니다.**SQLNativeSql**  
  
 연결 핸들은 **SQLAllocHandle으로** 할당되고 **SQLFreeHandle**.
