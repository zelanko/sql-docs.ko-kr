---
title: Microsoft 인터넷 정보 서비스를 사용 하 여 | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c1f0e1e4c21fc6e04bbaae7ec39d4b8d6ef1dd8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-microsoft-internet-information-services"></a>Microsoft 인터넷 정보 서비스를 사용 하 여
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 IIS 스크립트 (특히 사용자 오류가 나타나는 경우 또는 12641) 내에서 연결 하는 데 어려움이 있는 경우 Sqlnet.ora 파일에 다음 줄을 추가 합니다.  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 익명 인증을 사용 하 여 연결할 수 있도록 보안 네트워크 서비스 해제 됩니다.
