---
title: ODBC 연결을 테스트 | Microsoft Docs
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
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dee186c832f79c59da23adc48295ef647446711e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="testing-the-odbc-connection"></a>ODBC 연결 테스트
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 Oracle에 대 한 ODBC 액세스 문제를 해결할 때 7.x 및 열고 Oracle8 RDBMS 서버 되어 있는지 확인 해야 할 수 있습니다 기본 SQL * Net 및 Oracle 프로토콜 어댑터가 제대로 설치 되어 있습니다. 이 위해 Orawin\Bin 디렉터리에 Nettest.exe는 Oracle에서 제공한 유틸리티를 사용 합니다.  
  
 설치 된 sql 문을 사용 하 여 선택한 서버에 로그온 하려고 시도 하는 간단한 유틸리티 Nettest * Oracle 클라이언트의 일부인 소프트웨어 Net 합니다. 암호 및 TNS 문자열을 연결 유틸리티 로그인 이름을 묻는 메시지가 표시 됩니다. Oracle 클라이언트가 제대로 설치 유틸리티 "Ping 성공 합니다.."에 표시 하기만 하면 합니다. 로그인 성공 하지 못한 경우에 데이터베이스 관리자에 게 문의 해야 합니다.
