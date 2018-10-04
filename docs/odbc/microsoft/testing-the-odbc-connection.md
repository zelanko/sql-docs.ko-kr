---
title: ODBC 연결을 테스트 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 543ab436ac7dca5e0d5965220cd90a798afb5ccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767801"
---
# <a name="testing-the-odbc-connection"></a>ODBC 연결 테스트
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle에 대 한 ODBC 액세스 문제를 해결할 때 7.x 및 열고 Oracle8 RDBMS 서버에서 확인 해야 할 수 있습니다 기본 SQL * Net 및 Oracle 프로토콜 어댑터 올바르게 설치 되어 있습니다. 이 위해 Orawin\Bin 디렉터리에 Oracle 제공 유틸리티 Nettest.exe를 사용 합니다.  
  
 Nettest만 설치 된 SQL을 사용 하 여 선택한 서버에 로그온 하려고 시도 하는 간단한 유틸리티는 * Oracle 클라이언트의 일부인 소프트웨어는 Net 합니다. 암호 및 TNS 문자열을 연결 유틸리티 로그인 이름을 묻는 메시지가 나타납니다. Oracle 클라이언트가 올바르게 설치 되어 있는 경우이 유틸리티 단순히 표시 합니다 "Ping 성공 합니다." 로그인 하지 못한 경우에 데이터베이스 관리자에 게 문의 해야 합니다.
