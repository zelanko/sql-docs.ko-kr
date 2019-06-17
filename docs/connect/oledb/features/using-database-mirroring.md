---
title: 데이터베이스 미러링을 사용 하 여 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 데이터베이스 미러링을 사용 하 여
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- OLE DB Driver for SQL Server, database mirroring
- data access [OLE DB Driver for SQL Server], database mirroring
- database mirroring [SQL Server], connecting clients to
- MSOLEDBSQL, database mirroring
- OLE DB Driver for SQL Server, database mirroring
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: eba70e8a4ee641b4bccb54f67f37015a0edbd434
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802903"
---
# <a name="using-database-mirroring"></a>데이터베이스 미러링 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 대신 사용합니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 데이터베이스 미러링은 데이터베이스 가용성과 데이터 중복을 높이는 솔루션입니다. SQL Server용 OLE DB 드라이버는 데이터베이스 미러링을 암시적으로 지원하므로 데이터베이스에 미러링이 구성되고 나면 개발자는 코드를 작성하거나 별도의 조치를 취할 필요가 없습니다.  
  
 데이터베이스 단위로 구현되는 데이터베이스 미러링은 대기 서버에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로덕션 데이터베이스의 복사본을 보관합니다. 이 서버는 데이터베이스 미러링 세션의 구성 및 상태에 따라 핫 대기 서버나 웜 대기 서버가 됩니다. 핫 대기 서버는 커밋된 트랜잭션이 손실되지 않는 신속한 장애 조치(Failover)를 지원하며, 웜 대기 서버는 강제 서비스(데이터 손실 가능성이 있음)를 지원합니다.  
  
 프로덕션 데이터베이스는 *주 데이터베이스*, 대기 복사본은 *미러 데이터베이스*라고 부릅니다. 주 데이터베이스 및 미러 데이터베이스는 별도의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스(서버 인스턴스)에 상주해야 하며 가능한 한 상주하는 컴퓨터도 달라야 합니다.  
  
 *주 서버*라고 하는 프로덕션 서버 인스턴스는 *미러 서버*라고 하는 대기 서버 인스턴스와 통신합니다. 주 서버 및 미러 서버는 데이터베이스 미러링 *세션* 내에서 서로 파트너 역할을 합니다. 주 서버가 실패하면 미러 서버가 *장애 조치(failover)* 라는 프로세스를 통해 자신의 데이터베이스를 주 데이터베이스로 만듭니다. 예를 들어 서로 파트너 관계인 Partner_A와 Partner_B 서버가 있는데, 처음에 주 데이터베이스는 주 서버인 Partner_A에 상주하고 미러 데이터베이스는 미러 서버인 Partner_B에 상주한다고 가정합니다. Partner_A가 오프라인이 된 경우 Partner_B에 있는 데이터베이스가 장애 조치(Failover)되어 현재 주 데이터베이스가 될 수 있습니다. Partner_A가 미러링 세션에 다시 참여하면 Partner_A는 미러 서버가 되고 그 데이터베이스가 미러 데이터베이스가 됩니다.  
  
 대체 데이터베이스 미러링 구성은 성능 및 데이터 안전 수준이 다르며 지원되는 장애 조치(Failover) 형태도 다릅니다. 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
 미러 데이터베이스 이름을 지정할 때 별칭을 사용할 수도 있습니다.  
  
> [!NOTE]  
>  초기 연결 시도 및 재연결 시도 미러된 데이터베이스에 대 한 자세한 내용은 [데이터베이스 미러링 세션에 클라이언트 연결 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)합니다.  
  
## <a name="programming-considerations"></a>프로그래밍 고려 사항  
 주 데이터베이스 서버가 실패하면 클라이언트 응용 프로그램에서 API 호출에 대한 응답으로 오류를 받게 되는데, 이는 데이터베이스 연결이 끊어졌다는 의미입니다. 이러한 경우 커밋되지 않은 데이터베이스 변경 내용이 손실되고 현재 트랜잭션은 롤백됩니다. 또한 응용 프로그램에서는 연결을 종료하거나 데이터 원본 개체를 해제한 후 다시 연결해야 합니다. 이 연결은 이제 주 서버 역할을 수행할 미러 데이터베이스로 투명하게 리디렉션됩니다.  
  
 연결이 설정되면 주 서버는 장애 조치(Failover) 파트너의 ID를 장애 조치(Failover) 시 사용할 클라이언트로 보냅니다. 응용 프로그램이 실패한 주 서버에 연결하려는 경우 클라이언트는 장애 조치(Failover) 파트너의 ID를 모릅니다. 클라이언트는 초기화 속성 및 이와 관련된 연결 문자열 키워드를 사용하여 직접 장애 조치(Failover) 파트너의 ID를 지정함으로써 이러한 시나리오에 대처할 수 있습니다. 클라이언트 특성은 이 시나리오에서만 사용되며 주 서버를 사용할 수 있는 경우에는 사용되지 않습니다. 클라이언트가 제공한 장애 조치(Failover) 파트너 서버가 장애 조치(Failover) 파트너 역할을 하는 서버를 참조하지 않는 경우 해당 서버에서 연결을 거부합니다. 연결이 설정된 후 특성을 조사하여 실제 장애 조치(Failover) 파트너의 ID를 확인하면 응용 프로그램에 구성 변경 내용을 적용할 수 있습니다. 첫 번째 연결 시도가 실패한 경우에는 파트너 정보를 캐싱하여 연결 문자열을 업데이트하거나 재시도 전략을 세우는 방법을 고려해 보십시오.  
  
> [!NOTE]  
>  이 기능을 DSN, 연결 문자열 또는 연결 속성/특성에서 사용하려는 경우에는 연결에 사용할 데이터베이스를 명시적으로 지정해야 합니다. 이렇게 하지 않으면 하는 경우 OLE DB Driver for SQL Server 장애 조치 파트너 데이터베이스를 시도 하지 않습니다.  
>   
>  미러링은 데이터베이스의 기능입니다. 여러 데이터베이스를 사용하는 응용 프로그램에서는 이 기능을 이용하지 못할 수 있습니다.  
>   
>  또한 서버 이름은 대/소문자를 구분하지 않지만 데이터베이스 이름은 대/소문자를 구분합니다. 따라서 DSN 및 연결 문자열에서 동일한 대/소문자 조합을 사용해야 합니다.  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버  
 SQL Server용 OLE DB 드라이버는 연결 및 연결 문자열 특성을 통해 데이터베이스 미러링을 지원합니다. DBPROPSET_SQLSERVERDBINIT 속성 집합에 SSPROP_INIT_FAILOVERPARTNER 속성이 추가되었으며 DBPROP_INIT_PROVIDERSTRING의 새로운 연결 문자열 특성으로 **FailoverPartner** 키워드가 추가되었습니다. 자세한 내용은 [OLE DB Driver for SQL Server를 사용 하 여 연결 문자열 키워드를 사용 하 여](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)입니다.  
  
 장애 조치(Failover) 캐시는 공급자가 로드되어 있는 동안, 즉 **CoUninitialize**가 호출되기 전까지 또는 애플리케이션이 SQL Server용 OLE DB 드라이버가 관리하는 일부 개체(예: 데이터 원본 개체)에 대한 참조를 가지고 있는 동안 유지됩니다.  
  
 SQL Server 데이터베이스 미러링 지원에 대 한 OLE DB 드라이버에 대 한 세부 정보를 참조 하세요 [초기화 및 권한 부여 속성](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)합니다.  
 
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [데이터베이스 미러링 세션에 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
