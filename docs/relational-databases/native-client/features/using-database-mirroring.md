---
title: "데이터베이스 미러링을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- SQL Server Native Client, database mirroring
- data access [SQL Server Native Client], database mirroring
- database mirroring [SQL Server], connecting clients to
- SQLNCLI, database mirroring
- SQL Server Native Client ODBC driver, database mirroring
- SQL Server Native Client OLE DB provider, database mirroring
ms.assetid: 71b15712-7972-4465-9274-e0ddc271eedc
caps.latest.revision: "55"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b57f77a051e2490238d88f8bc336ce34fb0e380b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="using-database-mirroring"></a>데이터베이스 미러링 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 대신 사용합니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 데이터베이스 미러링은 데이터베이스 가용성과 데이터 중복을 높이는 솔루션입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client는 개발자가 데이터베이스에 대해 구성 되 면 다른 작업을 수행 하거나 코드를 작성 하지 않아도 되므로 데이터베이스 미러링에 대 한 암시적으로 지원을 제공 합니다.  
  
 복사본을 유지 하는 데이터베이스 미러링은 데이터베이스 단위로 구현 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로덕션 서버의 데이터베이스를 대기 합니다. 이 서버는 데이터베이스 미러링 세션의 구성 및 상태에 따라 핫 대기 서버나 웜 대기 서버가 됩니다. 핫 대기 서버는 커밋된 트랜잭션이 손실되지 않는 신속한 장애 조치(Failover)를 지원하며, 웜 대기 서버는 강제 서비스(데이터 손실 가능성이 있음)를 지원합니다.  
  
 프로덕션 데이터베이스 라고는 *주 데이터베이스*, 대기 복사본 이라고 하 고는 *미러 데이터베이스*합니다. 주 데이터베이스와 미러 데이터베이스의 개별 인스턴스에 있어야 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (서버 인스턴스) 및 가능한 경우 별도 컴퓨터에 상주 달라 야 합니다.  
  
 호출 하는 프로덕션 서버 인스턴스는 *주 서버*, 호출 하는 대기 서버 인스턴스와 통신 하는 *미러 서버*합니다. 주 서버와 미러 서버에서 데이터베이스 미러링 파트너로 작동 *세션*합니다. 주 서버가 실패 하는 경우 미러 서버 라는 프로세스를 통해 주 데이터베이스에 해당 데이터베이스를 만들 수 *장애 조치*합니다. 예를 들어 서로 파트너 관계인 Partner_A와 Partner_B 서버가 있는데, 처음에 주 데이터베이스는 주 서버인 Partner_A에 상주하고 미러 데이터베이스는 미러 서버인 Partner_B에 상주한다고 가정합니다. Partner_A가 오프라인이 된 경우 Partner_B에 있는 데이터베이스가 장애 조치(Failover)되어 현재 주 데이터베이스가 될 수 있습니다. Partner_A가 미러링 세션에 다시 참여하면 Partner_A는 미러 서버가 되고 그 데이터베이스가 미러 데이터베이스가 됩니다.  
  
 대체 데이터베이스 미러링 구성은 성능 및 데이터 안전 수준이 다르며 지원되는 장애 조치(Failover) 형태도 다릅니다. 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
 미러 데이터베이스 이름을 지정할 때 별칭을 사용할 수도 있습니다.  
  
> [!NOTE]  
>  에 초기 연결 시도 및 재연결 시도 미러된 데이터베이스에 대 한 내용은 참조 하세요. [데이터베이스 미러링 세션 &#40;에 클라이언트 연결 SQL Server &#41; ](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
## <a name="programming-considerations"></a>프로그래밍 고려 사항  
 주 데이터베이스 서버가 실패하면 클라이언트 응용 프로그램에서 API 호출에 대한 응답으로 오류를 받게 되는데, 이는 데이터베이스 연결이 끊어졌다는 의미입니다. 이러한 경우 커밋되지 않은 데이터베이스 변경 내용이 손실되고 현재 트랜잭션은 롤백됩니다. 또한 응용 프로그램에서는 연결을 종료하거나 데이터 원본 개체를 해제한 후 다시 연결해야 합니다. 이 연결은 이제 주 서버 역할을 수행할 미러 데이터베이스로 투명하게 리디렉션됩니다.  
  
 연결이 설정되면 주 서버는 장애 조치(Failover) 파트너의 ID를 장애 조치(Failover) 시 사용할 클라이언트로 보냅니다. 응용 프로그램이 실패한 주 서버에 연결하려는 경우 클라이언트는 장애 조치(Failover) 파트너의 ID를 모릅니다. 클라이언트는 초기화 속성 및 이와 관련된 연결 문자열 키워드를 사용하여 직접 장애 조치(Failover) 파트너의 ID를 지정함으로써 이러한 시나리오에 대처할 수 있습니다. 클라이언트 특성은 이 시나리오에서만 사용되며 주 서버를 사용할 수 있는 경우에는 사용되지 않습니다. 클라이언트가 제공한 장애 조치(Failover) 파트너 서버가 장애 조치(Failover) 파트너 역할을 하는 서버를 참조하지 않는 경우 해당 서버에서 연결을 거부합니다. 연결이 설정된 후 특성을 조사하여 실제 장애 조치(Failover) 파트너의 ID를 확인하면 응용 프로그램에 구성 변경 내용을 적용할 수 있습니다. 첫 번째 연결 시도가 실패한 경우에는 파트너 정보를 캐싱하여 연결 문자열을 업데이트하거나 재시도 전략을 세우는 방법을 고려해 보십시오.  
  
> [!NOTE]  
>  이 기능을 DSN, 연결 문자열 또는 연결 속성/특성에서 사용하려는 경우에는 연결에 사용할 데이터베이스를 명시적으로 지정해야 합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 파트너 데이터베이스에 장애 조치(Failover)를 시도하지 않습니다.  
>   
>  미러링은 데이터베이스의 기능입니다. 여러 데이터베이스를 사용하는 응용 프로그램에서는 이 기능을 이용하지 못할 수 있습니다.  
>   
>  또한 서버 이름은 대/소문자를 구분하지 않지만 데이터베이스 이름은 대/소문자를 구분합니다. 따라서 DSN 및 연결 문자열에서 동일한 대/소문자 조합을 사용해야 합니다.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 연결 및 연결 문자열 특성을 통해 데이터베이스 미러링을 지원 합니다. DBPROPSET_SQLSERVERDBINIT 속성 집합에 SSPROP_INIT_FAILOVERPARTNER 속성이 추가 되었습니다 및 **FailoverPartner** 키워드 DBPROP_INIT_PROVIDERSTRING에 대 한 새 연결 문자열 특성입니다. 자세한 내용은 참조 [Connection String Keywords with SQL Server Native Client를 사용 하 여](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)합니다.  
  
 장애 조치 캐시 될 때까지 인 공급자가 로드 상태로 유지 됩니다 **CoUninitialize** 호출 되었거나 응용 프로그램에 의해 관리 되는 일부 개체에 대 한 참조는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 와 같은 Native Client OLE DB 공급자는 데이터 원본 개체입니다.  
  
 에 대 한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 지원 데이터베이스 미러링에 대 한 참조 [초기화 및 권한 부여 속성](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)합니다.  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결 및 연결 문자열 특성을 통해 데이터베이스 미러링을 지원 합니다. 와 함께 사용할 수 있는 SQL_COPT_SS_FAILOVER_PARTNER 특성이 추가 되었습니다 특히는 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 함수 및 **에서 Failover_Partner** 키워드가 새로운 연결 문자열 특성으로 추가 되었습니다.  
  
 장애 조치(Failover) 캐시는 응용 프로그램에 한 개 이상의 환경 핸들이 할당되어 있는 동안 유지됩니다. 반대로 마지막 환경 핸들의 할당이 취소되면 장애 조치(Failover) 캐시가 손실됩니다.  
  
> [!NOTE]  
>  ODBC 드라이버 관리자는 장애 조치(Failover) 서버 이름의 사양을 지원하도록 향상되었습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [데이터베이스 미러링 세션에 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
