---
title: ODBC 연결 테스트 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8de19af2b50a58eef22ec074a308f86717278a48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303114"
---
# <a name="testing-the-odbc-connection"></a>ODBC 연결 테스트
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 오라클 7.x 및 Oracle8 RDBMS 서버에 대한 ODBC 액세스 문제를 해결할 때 기본 SQL*Net 및 Oracle 프로토콜 어댑터가 올바르게 설치되었는지 확인해야 할 수 있습니다. 이렇게 하려면 오라윈\빈 디렉토리에서 Oracle 제공 유틸리티 Nettest.exe를 사용합니다.  
  
 Nettest는 Oracle 클라이언트의 일부인 설치된 SQL*Net 소프트웨어만 사용하여 선택한 서버에 로그온하려고 시도하는 간단한 유틸리티입니다. 유틸리티는 로그인 이름, 암호 및 TNS 연결 문자열을 요청합니다. Oracle 클라이언트가 올바르게 설치되면 유틸리티에 "Ping 성공"이 표시됩니다. 로그인에 성공하지 못하면 데이터베이스 관리자와 상의해야 합니다.
