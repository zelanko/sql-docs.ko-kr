---
title: 오라클을 위한 ODBC 드라이버 | 마이크로 소프트 문서
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
ms.openlocfilehash: 2b5f1aabd23a587e681c33aed4b4119523444219
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402607"
---
# <a name="odbc-driver-for-oracle"></a>Oracle용 ODBC 드라이버
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 [오라클에서 제공하는 ODBC 드라이버를](https://www.oracle.com/database/technologies/releasenote-odbc-ic.html)사용합니다.  
  
 오라클용 Microsoft® ODBC 드라이버를 사용하면 ODBC 호환 응용 프로그램을 Oracle 데이터베이스에 연결할 수 있습니다. 오라클의 ODBC 드라이버는 *ODBC 프로그래머의 참조에*설명된 개방형 데이터베이스 연결(ODBC) 사양을 준수합니다. 인터넷 정보 서비스(IIS) 내에서 PL/SQL 패키지, XA/DTC 통합 및 오라클 액세스에 액세스할 수 있습니다.  
  
 Oracle RDBMS는 다양한 워크스테이션 및 미니컴퓨터 운영 체제에서 실행되는 다중 사용자 관계형 데이터베이스 관리 시스템입니다. Microsoft Windows를 실행하는 IBM 호환 컴퓨터는 네트워크를 통해 오라클 데이터베이스 서버와 통신할 수 있습니다. 지원되는 네트워크에는 Microsoft LAN 관리자, 넷웨어, VINES, DECnet 및 TCP/IP를 지원하는 모든 네트워크가 포함됩니다.  
  
 오라클용 ODBC 드라이버를 사용하면 애플리케이션이 ODBC 인터페이스를 통해 Oracle 데이터베이스의 데이터에 액세스할 수 있습니다. 드라이버는 로컬 Oracle 데이터베이스에 액세스하거나 SQL*Net을 통해 네트워크와 통신할 수 있습니다. 다음 다이어그램은 이 응용 프로그램 및 드라이버 아키텍처에 대해 자세히 설명합니다.  
  
 ![오라클 앱&#47;드라이버 아키텍처를 위한 ODBC 드라이버](../../odbc/microsoft/media/orcdrvsdkarch.gif "오크드르브스드크아크")  
  
 오라클의 ODBC 드라이버는 API 적합성 수준 1 및 SQL 적합성 수준 코어를 준수합니다. 또한 API 적합성 수준 2의 일부 함수와 코어 및 확장 SQL 준수 수준에서 대부분의 문법을 지원합니다. 드라이버는 ODBC 2.5를 준수하며 32비트 시스템을 지원합니다. 오라클 7.3x는 완벽하게 지원됩니다. Oracle8은 지원이 제한되어 있습니다. 오라클용 ODBC 드라이버는 유니코드 데이터 유형, BLOB, CLOB 등 새로운 Oracle8 데이터 형식을 지원하지 않으며 오라클의 새로운 관계형 개체 모델을 지원하지도 않습니다. 지원되는 데이터 형식에 대한 자세한 내용은 이 가이드의 [지원되는 데이터 형식을](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) 참조하십시오.  
  
 Oracle 데이터에 액세스하려면 다음 구성 요소가 필요합니다.  
  
-   오라클의 ODBC 드라이버  
  
-   오라클 RDBMS 데이터베이스  
  
-   오라클 클라이언트 소프트웨어  
  
 또한 원격 연결의 경우:  
  
-   드라이버와 데이터베이스를 실행하는 컴퓨터를 연결하는 네트워크입니다. 네트워크는 SQL*Net 연결을 지원해야 합니다.  
  
## <a name="component-documentation"></a>구성 요소 설명서  
 이 가이드에는 오라클용 Microsoft ODBC 드라이버를 설정하고 구성하고 프로그래밍 기능을 추가하는 것에 대한 자세한 정보가 포함되어 있습니다. 또한 기술 참조 자료가 포함되어 있습니다.  
  
 특정 오라클 제품 동작에 대한 자세한 내용은 Oracle 제품과 함께 제공되는 설명서를 참조하십시오.  
  
 ODBC 데이터 원본 관리자를 사용하여 오라클의 Microsoft ODBC 드라이버를 설정하거나 구성하는 것에 대한 자세한 내용은 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md) 설명서를 참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Oracle용 ODBC 드라이버 사용자 가이드](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Oracle용 ODBC 드라이버 프로그래머 참조](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
