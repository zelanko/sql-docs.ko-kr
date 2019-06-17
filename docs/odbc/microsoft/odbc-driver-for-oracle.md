---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4685d209d768bd3ff41c1c7367ef6cb6dcd45bcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043866"
---
# <a name="odbc-driver-for-oracle"></a>Oracle용 ODBC 드라이버
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 Microsoft® ODBC 드라이버를 사용 하면 Oracle 데이터베이스를 ODBC 호환 응용 프로그램에 연결할 수 있습니다. Oracle 용 ODBC 드라이버에 설명 된 ODBC Open Database Connectivity () 사양을 준수 합니다 *ODBC 프로그래머 참조*합니다. PL/SQL 패키지, XA/DTC 통합 및 인터넷 정보 서비스 (IIS) 내에서 Oracle 액세스에 액세스할 수 있습니다.  
  
 RDBMS oracle은 다양 한 워크스테이션 및 미니 컴퓨터 운영 체제를 실행 하는 다중 사용자 관계형 데이터베이스 관리 시스템입니다. Microsoft Windows를 실행 하는 IBM-호환 되는 컴퓨터는 네트워크를 통해 Oracle 데이터베이스 서버와 통신할 수 있습니다. 지원 되는 네트워크 Microsoft LAN Manager, NetWare, VINES, DECnet 및 TCP/IP를 지 원하는 모든 네트워크 포함 합니다.  
  
 Oracle 용 ODBC 드라이버에 응용을 프로그램이 ODBC 인터페이스를 통해 Oracle 데이터베이스의 데이터에에서 액세스할 수 있습니다. 드라이버가 로컬 Oracle 데이터베이스를 액세스할 수 있거나 SQL 통해 네트워크와 통신할 수 * 순입니다. 다음 다이어그램은이 응용 프로그램 및 드라이버 아키텍처를 자세히 설명합니다.  
  
 ![Oracle 앱에 대 한 ODBC 드라이버&#47;드라이버 아키텍처](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Oracle 용 ODBC 드라이버 적합성 수준 1 API 및 SQL 적합성 수준 Core 준수합니다. 또한 API 적합성 수준 2 코어 및 확장 SQL 적합성 수준에서 문법의 대부분에 일부 기능을 지원합니다. 드라이버는 ODBC 2.5 규정을 준수 하 고 32 비트 시스템을 지원 합니다. Oracle 7.3 x는 완전히; 지원 열고 Oracle8 제한적으로 지원 합니다. Oracle 용 ODBC 드라이버-유니코드 데이터 형식, Blob, Clob, 및 등-새 열고 Oracle8 데이터 형식 중 하나를 지원 하지 않습니다도 Oracle의 새로운 관계형 개체 모델을 지원 하지 않습니다. 지원 되는 데이터 형식에 대 한 자세한 내용은 참조 하세요. [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) 이 가이드에서.  
  
 Oracle 데이터에 액세스 하려면 다음 구성 요소가 필요 합니다.  
  
-   Oracle 용 ODBC 드라이버  
  
-   Oracle의 RDBMS 데이터베이스를  
  
-   Oracle 클라이언트 소프트웨어  
  
 또한 연결용 원격:  
  
-   드라이버 및 데이터베이스를 실행 하는 컴퓨터에 연결 되는 네트워크입니다. SQL을 지원 해야 하는 네트워크 * Net 연결 합니다.  
  
## <a name="component-documentation"></a>구성 요소 설명서  
 이 가이드에는 설정 및 Oracle 용 Microsoft ODBC 드라이버를 구성 하 고 프로그래밍 방식으로 기능을 추가 하는 방법에 대 한 자세한 정보가 있습니다. 기술 참조 자료도 포함합니다.  
  
 특정 Oracle 제품 동작에 대 한 정보에 대 한 Oracle 제품을 함께 제공 되는 설명서를 참조 하세요.  
  
 설정 또는 ODBC 데이터 원본 관리자를 사용 하 여 Oracle 용 Microsoft ODBC 드라이버 구성에 대 한 내용은 참조는 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md) 설명서.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Oracle용 ODBC 드라이버 사용자 가이드](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Oracle용 ODBC 드라이버 프로그래머 참고 자료](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
