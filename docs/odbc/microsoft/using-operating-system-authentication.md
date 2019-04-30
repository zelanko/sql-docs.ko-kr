---
title: 운영 체제 인증을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a532c253ea2204fa3636c24c503cbefd3fa6311
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127819"
---
# <a name="using-operating-system-authentication"></a>운영 체제 인증 사용
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 데이터베이스 계정에 대 한 액세스를 제어 하는 기본 운영 체제 의존 하는 oracle 운영 체제 인증 합니다. 이 유형의 로그인을 사용 하는 경우 사용자가 암호를 입력 하지 해야 합니다.  
  
 이 기능을 활용 하려면 지정 "/" 사용자 ID와 다음 연결 Api 사용 하 여 연결할 때 암호를 지정 하지 않으면 및: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)하십시오 [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md), 또는 [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)합니다.  
  
 SQL을 사용 하 여 oracle 데이터베이스 * Net 인증 서비스에 로그온 하는 사용자를 인증 합니다. 이 서비스 사용자 SQLPlus; 통해 Oracle로 로그인 하는 경우에 잘 작동 그러나 로그인 한 사용자는 인터넷 정보 서비스와 같은 서비스 인증이 실패 합니다. SQL의 알려진 제한 사항\*Net 인증 하 고 다음 오류를 생성 합니다. "[Microsoft] [ODBC driver for Oracle] [Oracle] ORA-12641: TNS:authentication 서비스 초기화 하지 못했습니다. "  
  
 Sqlnet.ora 파일을 편집 하 여이 문제를 해결할 수 있습니다. 이 구성 파일은 일반적으로 Oracle 홈 디렉터리의 Network\Admin 하위 디렉터리에 저장 됩니다. Sqlnet.ora에 다음 줄을 추가 합니다.  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
