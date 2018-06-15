---
title: 데이터베이스 미러링을 사용 하 여 | Microsoft Docs
description: OLE DB Driver for SQL Server 데이터베이스 미러링을 사용 하 여
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- OLE DB Driver for SQL Server, database mirroring
- data access [OLE DB Driver for SQL Server], database mirroring
- database mirroring [SQL Server], connecting clients to
- MSOLEDBSQL, database mirroring
- OLE DB Driver for SQL Server, database mirroring
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 69cf01aa4211bcc75e2bcbecec47a42fabf57e34
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612038"
---
# <a name="using-database-mirroring"></a>데이터베이스 미러링 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 대신 사용합니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 데이터베이스 미러링은 데이터베이스 가용성과 데이터 중복을 높이는 솔루션입니다. OLE DB Driver for SQL Server 개발자가 데이터베이스에 대해 구성 되 면 다른 작업을 수행 하거나 코드를 작성 하지 않아도 되므로 데이터베이스 미러링을 암시적으로 지원을 제공 합니다.  
  
 복사본을 유지 하는 데이터베이스 미러링은 데이터베이스 단위로 구현 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로덕션 서버의 데이터베이스를 대기 합니다. 이 서버는 데이터베이스 미러링 세션의 구성 및 상태에 따라 핫 대기 서버나 웜 대기 서버가 됩니다. 핫 대기 서버는 커밋된 트랜잭션이 손실되지 않는 신속한 장애 조치(Failover)를 지원하며, 웜 대기 서버는 강제 서비스(데이터 손실 가능성이 있음)를 지원합니다.  
  
 프로덕션 데이터베이스 라고는 *주 데이터베이스*, 대기 복사본 이라고 하 고는 *미러 데이터베이스*합니다. 주 데이터베이스와 미러 데이터베이스의 개별 인스턴스에 있어야 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (서버 인스턴스) 및 가능한 경우 별도 컴퓨터에 상주 달라 야 합니다.  
  
 호출 하는 프로덕션 서버 인스턴스는 *주 서버*, 호출 하는 대기 서버 인스턴스와 통신 하는 *미러 서버*합니다. 주 서버와 미러 서버에서 데이터베이스 미러링 파트너로 작동 *세션*합니다. 주 서버가 실패 하는 경우 미러 서버 라는 프로세스를 통해 주 데이터베이스에 해당 데이터베이스를 만들 수 *장애 조치*합니다. 예를 들어 서로 파트너 관계인 Partner_A와 Partner_B 서버가 있는데, 처음에 주 데이터베이스는 주 서버인 Partner_A에 상주하고 미러 데이터베이스는 미러 서버인 Partner_B에 상주한다고 가정합니다. Partner_A가 오프라인이 된 경우 Partner_B에 있는 데이터베이스가 장애 조치(Failover)되어 현재 주 데이터베이스가 될 수 있습니다. Partner_A가 미러링 세션에 다시 참여하면 Partner_A는 미러 서버가 되고 그 데이터베이스가 미러 데이터베이스가 됩니다.  
  
 대체 데이터베이스 미러링 구성은 성능 및 데이터 안전 수준이 다르며 지원되는 장애 조치(Failover) 형태도 다릅니다. 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
 미러 데이터베이스 이름을 지정할 때 별칭을 사용할 수도 있습니다.  
  
> [!NOTE]  
>  에 초기 연결 시도 및 재연결 시도 미러된 데이터베이스에 대 한 내용은 참조 하십시오. [데이터베이스 미러링 세션에 클라이언트 연결 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)합니다.  
  
## <a name="programming-considerations"></a>프로그래밍 고려 사항  
 주 데이터베이스 서버가 실패하면 클라이언트 응용 프로그램에서 API 호출에 대한 응답으로 오류를 받게 되는데, 이는 데이터베이스 연결이 끊어졌다는 의미입니다. 이러한 경우 커밋되지 않은 데이터베이스 변경 내용이 손실되고 현재 트랜잭션은 롤백됩니다. 또한 응용 프로그램에서는 연결을 종료하거나 데이터 원본 개체를 해제한 후 다시 연결해야 합니다. 이 연결은 이제 주 서버 역할을 수행할 미러 데이터베이스로 투명하게 리디렉션됩니다.  
  
 연결이 설정되면 주 서버는 장애 조치(Failover) 파트너의 ID를 장애 조치(Failover) 시 사용할 클라이언트로 보냅니다. 응용 프로그램이 실패한 주 서버에 연결하려는 경우 클라이언트는 장애 조치(Failover) 파트너의 ID를 모릅니다. 클라이언트는 초기화 속성 및 이와 관련된 연결 문자열 키워드를 사용하여 직접 장애 조치(Failover) 파트너의 ID를 지정함으로써 이러한 시나리오에 대처할 수 있습니다. 클라이언트 특성은 이 시나리오에서만 사용되며 주 서버를 사용할 수 있는 경우에는 사용되지 않습니다. 클라이언트가 제공한 장애 조치(Failover) 파트너 서버가 장애 조치(Failover) 파트너 역할을 하는 서버를 참조하지 않는 경우 해당 서버에서 연결을 거부합니다. 연결이 설정된 후 특성을 조사하여 실제 장애 조치(Failover) 파트너의 ID를 확인하면 응용 프로그램에 구성 변경 내용을 적용할 수 있습니다. 첫 번째 연결 시도가 실패한 경우에는 파트너 정보를 캐싱하여 연결 문자열을 업데이트하거나 재시도 전략을 세우는 방법을 고려해 보십시오.  
  
> [!NOTE]  
>  이 기능을 DSN, 연결 문자열 또는 연결 속성/특성에서 사용하려는 경우에는 연결에 사용할 데이터베이스를 명시적으로 지정해야 합니다. 이렇게 하지 않으면 경우 OLE DB Driver for SQL Server 장애 조치 파트너 데이터베이스를 시도 하지 않습니다.  
>   
>  미러링은 데이터베이스의 기능입니다. 여러 데이터베이스를 사용하는 응용 프로그램에서는 이 기능을 이용하지 못할 수 있습니다.  
>   
>  또한 서버 이름은 대/소문자를 구분하지 않지만 데이터베이스 이름은 대/소문자를 구분합니다. 따라서 DSN 및 연결 문자열에서 동일한 대/소문자 조합을 사용해야 합니다.  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server  
 OLE DB Driver for SQL Server 데이터베이스 연결 및 연결을 통해 문자열 특성 미러링를 지원 합니다. DBPROPSET_SQLSERVERDBINIT 속성 집합에 SSPROP_INIT_FAILOVERPARTNER 속성이 추가 되었습니다 및 **FailoverPartner** 키워드 DBPROP_INIT_PROVIDERSTRING에 대 한 새 연결 문자열 특성입니다. 자세한 내용은 참조 [OLE DB 드라이버와 SQL Server에 대 한 연결 문자열 키워드를 사용 하 여](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)합니다.  
  
 장애 조치 캐시 될 때까지 인 공급자가 로드 상태로 유지 됩니다 **CoUninitialize** 호출 되었거나 응용 프로그램에 데이터 원본 개체와 같은 SQL Server 용 OLE DB 드라이버에서 관리 되는 일부 개체에 대 한 참조 .  
  
 SQL Server 데이터베이스 미러링 지원에 대 한 OLE DB 드라이버에 대 한 세부 정보를 참조 하십시오. [초기화 및 권한 부여 속성](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)합니다.  
 
  
## <a name="see-also"></a>관련 항목  
 [OLE DB Driver for SQL Server 기능](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [데이터베이스 미러링 세션에 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
