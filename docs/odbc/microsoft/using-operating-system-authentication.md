---
description: 운영 체제 인증 사용
title: 운영 체제 인증 사용 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94563fee00c979addb6fc088bfb3881763e4d188
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471325"
---
# <a name="using-operating-system-authentication"></a>운영 체제 인증 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 운영 체제 인증은 기본 운영 체제를 사용 하 여 데이터베이스 계정에 대 한 액세스를 제어 합니다. 이 유형의 로그인을 사용 하는 경우 사용자가 암호를 입력 하지 않아도 됩니다.  
  
 이 기능을 활용 하려면 사용자 ID로 "/"를 지정 하 고 [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)또는 [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)연결 api 중 하나를 사용 하 여 연결할 때 암호를 지정 하지 마십시오.  
  
 Oracle 데이터베이스는 SQL * Net 인증 서비스를 사용 하 여 로그온 한 사용자를 인증 합니다. 이 서비스는 사용자가 SQLPlus를 통해 Oracle에 로그인 한 경우 제대로 작동 합니다. 그러나 로그인 한 사용자가 인터넷 정보 서비스 같은 서비스인 경우 인증이 실패 합니다. 이는 SQL Net 인증의 알려진 제한 사항입니다 \* . "[Microsoft] [oracle driver For oracle] [oracle] ORA-12641: TNS: Authentication service를 초기화 하지 못했습니다." 오류를 생성 합니다.  
  
 Ora 파일을 편집 하 여이 문제를 해결할 수 있습니다. 이 구성 파일은 일반적으로 Oracle 홈 디렉터리의 Network\Admin 하위 디렉터리에 저장 됩니다. Ora에 다음 줄을 추가 합니다.  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
