---
title: API 함수 (Oracle 용 ODBC 드라이버)에 대 한 스레드 안전 참고 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 926b2285bcce9a28579fffc4004c5454b2837392
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912429"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 함수에 대한 스레드 안전 참고(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 Microsoft ODBC 드라이버는 스레드로부터 안전 합니다. 그러나 Oracle에서는 단일 연결에서 여러 동시 문의 수 없습니다. 드라이버는이 제한 사항을 적용 합니다. 즉, 다중 스레드 응용 프로그램에서 언제 든 지 Oracle 용 ODBC 드라이버에 모든 스레드에서 호출할 수 있지만 드라이버 차단 다른 스레드의 동일한 연결에서 드라이버 원본 스레드는 드라이버를 떠날 때까지 합니다.  
  
 두 개의 서로 다른 연결에서 두 개의 문이 있을 경우에 드라이버를 차단 하지 않습니다. 그러나 두 문 사용 하 여 단일 연결 인 경우 차단 가능성.
