---
title: 운영 체제 인증을 사용 하 여 | Microsoft Docs
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
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ca92a0642c436c6c04afdbca265192444c20634
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="using-operating-system-authentication"></a>운영 체제 인증을 사용 하 여
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 운영 체제 인증은 oracle 데이터베이스 계정에 대 한 액세스를 제어 하는 기본 운영 체제를 사용 합니다. 이 유형의 로그인을 사용 하는 경우 사용자가 암호를 입력 하지 필요 합니다.  
  
 이 기능을 활용 하려면 지정 "/" 사용자 ID와 Api 다음 연결 중 하나를 사용 하 여 연결할 때 암호를 지정 하지 않습니다: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md), 또는 [ SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)합니다.  
  
 SQL을 사용 하 여 oracle 데이터베이스 * Net 인증 서비스에서 기록 되는 사용자를 인증 합니다. 이 서비스는 SQLPlus;를 통해 Oracle에 사용자가 로그인 하는 경우에 작동 하며 그러나 로그인 한 사용자는 인터넷 정보 서비스 같은 서비스 인증이 실패 합니다. 이 SQL의 알려진된 제한 사항\*Net 인증 하 고 다음과 같은 오류가 생성: "[Microsoft] [ODBC driver for Oracle] [Oracle] 또는 12641: TNS:authentication 서비스 초기화 하지 못했습니다."  
  
 Sqlnet.ora 파일을 편집 하 여이 문제를 해결할 수 있습니다. 이 구성 파일은 일반적으로 Oracle 홈 디렉터리의 Network\Admin 하위 디렉터리에 저장 됩니다. Sqlnet.ora에 다음 줄을 추가 합니다.  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
