---
title: Microsoft 구성 요소 서비스를 사용 하 여 | Microsoft Docs
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
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c28df0cd6000a4ae0b2cb500a9521dc32facc6c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-microsoft-component-services"></a>Microsoft 구성 요소 서비스를 사용 하 여
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 Microsoft Windows NT/Windows 2000 및 Microsoft Windows 95/98 트랜잭션 구성 요소 서비스 (또는 Windows NT를 사용 하는 경우에 MTS)를 사용 하려면 Oracle 데이터베이스를 사용할 수 있습니다. 트랜잭션을 지 원하는 구성 요소 서비스를 사용 하려면 Oracle 데이터베이스를 사용 하려면 시스템 관리자 V$ XATRANS$ 라는 뷰를 만들어야 합니다. 이 스크립트를 만들려면 Oracle에서 제공 하는 스크립트를 실행 해야 합니다. 자세한 내용은 구성 요소 서비스 도움말 또는 Oracle 설명서를 참조 하십시오.
