---
title: Microsoft 인터넷 정보 서비스 사용 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c71babf933c2615e6c2464696c1023ccaf53dd7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282471"
---
# <a name="using-microsoft-internet-information-services"></a>Microsoft IIS(인터넷 정보 서비스) 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 IIS 스크립트 내에서 연결 하는 데 어려움이 있는 경우 (특히 ORA-12641 오류를 수신 하는 경우) ORA 파일에 다음 줄을 추가 합니다.  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 익명 인증을 사용 하 여 연결할 수 있도록 보안 Network Services를 사용 하지 않도록 설정 합니다.
