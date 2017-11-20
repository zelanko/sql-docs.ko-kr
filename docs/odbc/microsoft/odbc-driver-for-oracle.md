---
title: ODBC Driver for Oracle | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e66dd7ed6406287c0fb4e6722d8b5915428f705b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-driver-for-oracle"></a>Oracle에 대 한 ODBC 드라이버
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 Oracle 용 Microsoft® ODBC 드라이버를 사용 하면 Oracle 데이터베이스에 ODBC 호환 응용 프로그램을 연결할 수 있습니다. ODBC Driver for Oracle 사양을 준수 하는 ODBC Open Database Connectivity ()에 설명 된는 *ODBC Programmer's Reference*합니다. PL/SQL 패키지, XA/DTC 통합 및 인터넷 정보 서비스 (IIS) 내에서 Oracle 액세스에 액세스할 수 있습니다.  
  
 Oracle RDBMS는 다양 한 워크스테이션과 미니 컴퓨터 운영 체제를 실행 하는 다중 사용자 관계형 데이터베이스 관리 시스템입니다. Microsoft Windows를 실행 하는 IBM 호환 컴퓨터 네트워크를 통해 Oracle 데이터베이스 서버와 통신할 수 있습니다. 지원 되는 네트워크, 등이 Microsoft LAN Manager NetWare, VINES, DECnet TCP/IP를 지 원하는 모든 네트워크입니다.  
  
 Oracle에 대 한 ODBC 드라이버 응용을 프로그램을 ODBC 인터페이스를 통해 Oracle 데이터베이스에서 데이터에 액세스할 수 있습니다. SQL 통해 네트워크와 통신할 수 또는 드라이버 로컬 Oracle 데이터베이스를 액세스할 수 있는 * Net 합니다. 다음 다이어그램은이 응용 프로그램 / 드라이버 아키텍처에 자세히 설명 합니다.  
  
 ![ODBC Driver for Oracle 응용 프로그램 &#47; 드라이버 아키텍처](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Oracle에 대 한 ODBC 드라이버 API 규칙에 따라 수준 1 및 SQL 규칙 수준 코어 준수합니다. 또한 API 규칙에 따라 수준 2와 대부분의 핵심 및 확장 SQL 받는 규칙 수준에서 문법의 일부 함수를 지원합니다. 드라이버는 ODBC 2.5 규격와 32 비트 시스템을 지원 합니다. Oracle 7.3 x는 완전히; 지원 열고 Oracle8에 제한적으로 지원 합니다. Oracle에 대 한 ODBC 드라이버는 새로운 열고 Oracle8 데이터 형식 중 하나를 지원 하지 않습니다-유니코드 데이터 형식, Blob, Clob, 등-하거나 Oracle의 새로운 관계형 개체 모델을 지원 하지 않습니다. 지원 되는 데이터 형식에 대 한 자세한 내용은 참조 [지원 되는 데이터 유형](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) 이 가이드의 합니다.  
  
 Oracle 데이터에 액세스 하려면 다음 구성 요소가 필요 합니다.  
  
-   Oracle에 대 한 ODBC 드라이버  
  
-   RDBMS Oracle 데이터베이스  
  
-   Oracle 클라이언트 소프트웨어  
  
 또한 원격 연결에 대 한:  
  
-   드라이버와 데이터베이스를 실행 하는 컴퓨터를 연결 하는 네트워크입니다. 네트워크 SQL을 지원 해야 합니다 * Net 연결 합니다.  
  
## <a name="component-documentation"></a>구성 요소 설명서  
 이 가이드에는 설정 및 Microsoft ODBC Driver for Oracle 구성 하 고 프로그래밍 기능을 추가 하는 방법에 대 한 자세한 정보가 있습니다. 또한 기술 참조 자료도 포함 됩니다.  
  
 특정 Oracle 제품 동작에 대 한 정보를 Oracle 제품을 함께 제공 되는 설명서를 참조 하십시오.  
  
 설정 또는 ODBC 데이터 원본 관리자를 사용 하 여 Oracle 용 Microsoft ODBC 드라이버를 구성 하는 방법에 대 한 정보를 참조 하십시오.는 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md) 설명서입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Oracle용 ODBC 드라이버 사용자 가이드](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Oracle용 ODBC 드라이버 프로그래머 참고 자료](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)

