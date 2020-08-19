---
description: API 함수에 대한 스레드 안전 참고(Oracle용 ODBC 드라이버)
title: API 함수에 대 한 스레드 안전 정보 (Oracle 용 ODBC 드라이버) | Microsoft Docs
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
ms.openlocfilehash: 8c7da346832e2682caa02bdbdae91a1133a9cbaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449085"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 함수에 대한 스레드 안전 참고(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 Microsoft ODBC 드라이버는 스레드로부터 안전 합니다. 그러나 Oracle에서는 단일 연결에 대해 여러 동시 문을 사용할 수 없습니다. 드라이버는 이러한 제한을 적용 합니다. 즉, 다중 스레드 응용 프로그램에서 스레드가 언제 든 지 Oracle 용 ODBC 드라이버를 호출할 수 있지만 원래 스레드가 드라이버를 떠날 때까지 드라이버는 동일한 연결에서 드라이버의 다른 모든 스레드를 차단 합니다.  
  
 두 개의 서로 다른 연결에 두 개의 문이 있는 경우 드라이버는 차단 되지 않습니다. 그러나 두 개의 문을 사용 하 여 단일 연결을 사용 하는 경우 차단이 발생할 수 있습니다.
