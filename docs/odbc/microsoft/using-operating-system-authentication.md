---
title: 운영 체제 인증 사용 | 마이크로 소프트 문서
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
ms.openlocfilehash: d6520202bdbc31baf1156531457cb70a98656e88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292843"
---
# <a name="using-operating-system-authentication"></a>운영 체제 인증 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 Oracle 운영 체제 인증은 데이터베이스 계정에 대한 액세스를 제어하기 위해 기본 운영 체제에 의존합니다. 사용자는 이러한 유형의 로그인을 사용할 때 암호를 입력할 필요가 없습니다.  
  
 이 기능을 활용하려면 "/"를 사용자 ID로 지정하고 다음 연결 API 를 사용하여 연결할 때 암호를 지정하지 않습니다: [SQLBrowseConnect,](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)또는 [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 오라클 데이터베이스는 SQL*Net 인증 서비스를 사용하여 로그온한 사용자를 인증합니다. 이 서비스는 사용자가 SQLPlus를 통해 오라클에 로그인한 경우에 효과적입니다. 그러나 로그인한 사용자가 인터넷 정보 서비스와 같은 서비스인 경우 인증이 실패합니다. 이는 SQL\*Net 인증의 알려진 제한 사항이며 다음과 같은 오류를 생성합니다.  
  
 Sqlnet.ora 파일을 편집하여 이 문제를 해결할 수 있습니다. 이 구성 파일은 일반적으로 Oracle 홈 디렉터리의 Network\Admin 하위 디렉터리에 저장됩니다. Sqlnet.ora에 다음 줄을 추가합니다.  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
