---
title: API 기능에 대한 스레드 안전 참고 사항(오라클용 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 489f0e99ea53d419ff94dddfeb22e37573abb874
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303074"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 함수에 대한 스레드 안전 참고(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 오라클의 Microsoft ODBC 드라이버는 스레드에서 안전합니다. 그러나 오라클은 단일 연결에서 여러 개의 동시 문을 허용하지 않습니다. 드라이버는 이 제한을 적용합니다. 즉, 다중 스레드 응용 프로그램에서는 모든 스레드가 언제든지 Oracle의 ODBC Driver에 호출할 수 있지만 드라이버는 원래 스레드가 드라이버를 떠날 때까지 동일한 연결에서 드라이버에서 다른 스레드를 차단합니다.  
  
 서로 다른 두 연결에 두 개의 명령문이 있는 경우 드라이버는 차단되지 않습니다. 그러나 두 개의 명령문으로 단일 연결이 있는 경우 차단될 수 있습니다.
