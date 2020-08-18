---
description: Oracle용 ODBC 드라이버
title: Oracle 용 ODBC 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a561539ff960dfa6691d26496b1b62d2ee8ae763
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449335"
---
# <a name="odbc-driver-for-oracle"></a>Oracle용 ODBC 드라이버
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 Microsoft® ODBC Driver를 사용 하면 ODBC 규격 응용 프로그램을 Oracle 데이터베이스에 연결할 수 있습니다. Oracle 용 ODBC 드라이버는 odbc *프로그래머 참조*에 설명 된 Odbc (Open Database Connectivity) 사양을 준수 합니다. 이를 통해 인터넷 정보 서비스 (IIS) 내에서 PL/SQL 패키지, XA/DTC 통합 및 Oracle 액세스에 액세스할 수 있습니다.  
  
 Oracle RDBMS는 다양 한 워크스테이션 및 minicomputer 운영 체제에서 실행 되는 다중 사용자 관계형 데이터베이스 관리 시스템입니다. Microsoft Windows를 실행 하는 IBM 호환 컴퓨터는 네트워크를 통해 Oracle 데이터베이스 서버와 통신할 수 있습니다. 지원 되는 네트워크에는 Microsoft LAN Manager, NetWare, VINES, DECnet 및 TCP/IP를 지 원하는 모든 네트워크가 포함 됩니다.  
  
 Oracle 용 ODBC 드라이버를 사용 하면 응용 프로그램에서 ODBC 인터페이스를 통해 Oracle 데이터베이스의 데이터에 액세스할 수 있습니다. 드라이버는 로컬 Oracle 데이터베이스에 액세스 하거나 SQL * Net을 통해 네트워크와 통신할 수 있습니다. 다음 다이어그램에서는이 응용 프로그램 및 드라이버 아키텍처에 대해 자세히 설명 합니다.  
  
 ![Oracle 용 ODBC 드라이버 앱&#47;드라이버 아키텍처](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Oracle 용 ODBC 드라이버는 API 규칙 수준 1 및 SQL 규칙 수준 코어를 준수 합니다. 또한 API 규칙 수준 2의 일부 기능과 핵심 및 확장 된 SQL 규칙 수준의 문법을 지원 합니다. 드라이버는 ODBC 2.5 규격 이며 32 비트 시스템을 지원 합니다. Oracle 7.3 x는 완벽 하 게 지원 됩니다. Oracle8는 제한적으로 지원 됩니다. Oracle 용 ODBC 드라이버는 새로운 Oracle8 데이터 형식 (유니코드 데이터 형식, Blob, Clob 등)을 지원 하지 않으며 Oracle의 새로운 관계형 개체 모델도 지원 하지 않습니다. 지원 되는 데이터 형식에 대 한 자세한 내용은이 가이드의 [지원 되는 데이터 형식](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) 을 참조 하세요.  
  
 Oracle 데이터에 액세스 하려면 다음 구성 요소가 필요 합니다.  
  
-   Oracle 용 ODBC 드라이버  
  
-   Oracle RDBMS 데이터베이스  
  
-   Oracle 클라이언트 소프트웨어  
  
 또한 원격 연결에 대해 다음을 수행 합니다.  
  
-   드라이버와 데이터베이스를 실행 하는 컴퓨터를 연결 하는 네트워크입니다. 네트워크에서 SQL * Net 연결을 지원 해야 합니다.  
  
## <a name="component-documentation"></a>구성 요소 설명서  
 이 가이드에는 Oracle 용 Microsoft ODBC 드라이버를 설정 및 구성 하 고 프로그래밍 기능을 추가 하는 방법에 대 한 자세한 내용이 포함 되어 있습니다. 기술 참조 자료도 포함 되어 있습니다.  
  
 Oracle 제품의 특정 동작에 대 한 자세한 내용은 Oracle 제품과 함께 제공 되는 설명서를 참조 하십시오.  
  
 ODBC 데이터 원본 관리자를 사용 하 여 Oracle 용 Microsoft ODBC 드라이버를 설정 하거나 구성 하는 방법에 대 한 자세한 내용은 [Odbc 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md) 설명서를 참조 하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Oracle용 ODBC 드라이버 사용자 가이드](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Oracle용 ODBC 드라이버 프로그래머 참조](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
