---
title: API 함수 (ODBC Driver for Oracle)의 스레드 보안 메모 | Microsoft Docs
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
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31ac813b6419b75f63ee9c7152f888dd1396238e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 함수 (ODBC Driver for Oracle)의 스레드 보안 메모
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 Microsoft ODBC Driver for Oracle은 스레드로부터 안전 합니다. 그러나 Oracle 단일 연결에 여러 개의 동시 문을 허용 하지 않습니다. 드라이버는이 제한 사항을 적용 합니다. 즉, 다중 스레드 응용 프로그램에서 언제 든 지 Oracle에 대 한 ODBC 드라이버에 모든 스레드에서 호출할 수 있지만 드라이버 차단 다른 스레드가 동일한 연결에서 드라이버에서 원래 스레드가 드라이버를 떠날 때까지 합니다.  
  
 두 개의 서로 다른 연결에서 두 개의 문이 있을 경우 드라이버를 차단 하지 않습니다. 그러나 두 개의 문으로 단일 연결 인 경우 있기 차단 합니다.
