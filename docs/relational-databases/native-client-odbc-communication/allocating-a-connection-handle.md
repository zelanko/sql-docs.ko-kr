---
title: "연결 핸들 할당 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-communication
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC applications, passwords
- ODBC applications, connections
- handles [SQL Server Native Client]
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- SQL Server Native Client ODBC driver, connection handles
- connection handles [SQL Server Native Client]
- modifying passwords
- SQLAllocHandle function
ms.assetid: 471d8a31-199c-4f92-bb10-004fc7733b35
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58dce8d2ba1d69d3885d47fe6eff210a61482d68
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="allocating-a-connection-handle"></a>연결 핸들 할당
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  응용 프로그램이 데이터 원본이나 드라이버에 연결하려면 먼저 연결 핸들을 할당해야 합니다. 호출 하 여 이렇게 **SQLAllocHandle** 와 *HandleType* 매개 변수를 SQL_HANDLE_DBC로 설정 하 고 *InputHandle* 초기화 된 환경 핸들을 가리키는 합니다.  
  
 연결의 특징은 연결 특성을 설정하여 제어합니다. 예를 들어 트랜잭션이 연결 수준에서 발생하기 때문에 트랜잭션 격리 수준은 연결 특성입니다. 마찬가지로, 시간 초과되기 전에 연결을 기다리는 시간(초)인 로그인 제한 시간은 연결 특성입니다.  
  
 연결 특성으로 설정 되어 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), 하며 현재 설정 된 검색 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)합니다. 경우 **SQLSetConnectAttr** 은 연결이 시도 되기 전에 호출 ODBC 드라이버 관리자 해당 연결 구조는 특성을 저장 하 고 드라이버에서 연결 프로세스의 일환으로 설정 합니다. 일부 연결 특성은 응용 프로그램이 연결하기 전에 설정해야 하고, 다른 연결 특성은 연결이 완료된 후에 설정할 수 있습니다. 예를 들어 SQL_ATTR_ODBC_CURSORS는 연결하기 전에 설정해야 하지만 SQL_ATTR_AUTOCOMMIT은 연결한 후에 설정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 이상 버전에 대해 응용 프로그램을 실행하는 경우 TDS(Tabular Data Stream) 네트워크 패킷 크기를 다시 설정하면 성능이 향상될 수도 있습니다. 기본 패킷 크기는 서버에서 4KB로 설정됩니다. 일반적으로 패킷 크기가 4KB에서 8KB 사이일 때 최상의 성능을 얻을 수 있습니다. 테스트 결과, 다른 패킷 크기에서 성능이 더 빠른 경우 응용 프로그램에서 패킷 크기를 다시 설정할 수 있습니다. ODBC 응용 프로그램에서는 이렇게 하려면 호출 하 여 연결 하기 전에 **SQLSetConnectAttr** SQL_ATTR_PACKET_SIZE 옵션과 함께 합니다. 큰 패킷 크기에서 성능이 더 나은 응용 프로그램도 있지만 일반적으로 패킷 크기가 8KB보다 크면 성능 향상이 최소화됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 다양 한 응용 프로그램에서 기능 증가 하는 데 사용할 수 있는 확장 된 연결 특성이 있습니다. 이러한 특성 중 일부는 데이터 원본에 지정할 수 있는 것과 동일한 옵션을 제어하며, 데이터 원본에 설정된 옵션을 무시하는 데 사용됩니다. 예를 들어 응용 프로그램에서 따옴표 붙은 식별자를 사용하는 경우 드라이버별 특성 SQL_COPT_SS_QUOTED_IDENT를 SQL_QI_ON으로 설정하여 데이터 원본의 설정에 관계없이 이 옵션이 항상 설정되도록 할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server &#40; ODBC &#41;와 통신](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
