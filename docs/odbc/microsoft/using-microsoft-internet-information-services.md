---
title: Microsoft 인터넷 정보 서비스를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 509979a38e6d7e71f979ce317b9e1626a85c5a54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633393"
---
# <a name="using-microsoft-internet-information-services"></a>Microsoft IIS(인터넷 정보 서비스) 사용
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 IIS 스크립트 (특히 오류가 표시 되 면는 ORA-12641) 내에서 연결 하는 데 문제가 있다면 Sqlnet.ora 파일에 다음 줄을 추가 합니다.  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 익명 인증을 사용 하 여 연결할 수 있도록 보안 네트워크 서비스 해제 됩니다.
