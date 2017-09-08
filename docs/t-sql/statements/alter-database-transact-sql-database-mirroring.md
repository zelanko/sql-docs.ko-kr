---
title: "ALTER DATABASE 데이터베이스 미러링 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- witness [SQL Server], establishing
- manual failover [SQL Server]
- ALTER DATABASE statement, database mirroring
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 27a032ef-1cf6-4959-8e67-03d28c4b3465
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96ac469df9660e29c0394226cf7199e451df9d8c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-transact-sql-database-mirroring"></a>ALTER DATABASE (Transact SQL) 데이터베이스 미러링 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 대신 사용합니다.  
  
 데이터베이스에 대한 데이터베이스 미러링을 제어합니다. 데이터베이스 미러링 옵션에 지정한 값은 두 개의 데이터베이스 복사본 및 데이터베이스 미러링 세션에 전체적으로 적용됩니다. 하나의 \<문당 > ALTER DATABASE 문당 허용 됩니다.  
  
> [!NOTE]  
>  구성이 성능에 영향을 줄 수 있으므로 사용률이 낮은 시간에 데이터베이스 미러링을 구성하는 것이 좋습니다.  
  
 ALTER DATABASE 옵션을 참조 하세요. [ALTER database&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md). ALTER DATABASE SET 옵션에 대 한 참조 [ALTER DATABASE SET 옵션 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER DATABASE database_name   
SET { <partner_option> | <witness_option> }  
  <partner_option> ::=  
    PARTNER { = 'partner_server'   
            | FAILOVER   
            | FORCE_SERVICE_ALLOW_DATA_LOSS  
            | OFF  
            | RESUME   
            | SAFETY { FULL | OFF }  
            | SUSPEND   
            | TIMEOUT integer  
            }  
  <witness_option> ::=  
    WITNESS { = 'witness_server'   
            | OFF   
            }  
  
```  
  
## <a name="arguments"></a>인수  
  
> [!IMPORTANT]  
>  SET PARTNER 또는 SET WITNESS 명령은 입력 시 성공적으로 완료될 수 있지만 나중에 실패합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에는 ALTER DATABASE 데이터베이스 미러링 옵션을 사용할 수 없습니다.  
  
 *database_name*  
 수정할 데이터베이스의 이름입니다.  
  
 파트너 \<_ o p >  
 데이터베이스 미러링 세션의 장애 조치 파트너 및 이들의 동작을 정의하는 데이터베이스 속성을 제어합니다. SET PARTNER 옵션에는 주 서버 또는 미러 서버로 제한되는 옵션과 어느 파트너에든 설정할 수 있는 옵션이 있습니다. 자세한 내용은 다음의 개별 PARTNER 옵션을 참조하십시오. SET PARTNER 절은 지정된 파트너에 관계없이 데이터베이스 복사본 양쪽 모두에 영향을 줍니다.  
  
 SET PARTNER 문을 실행하려면 두 파트너의 끝점에 대한 STATE가 STARTED로 설정되어 있어야 합니다. 또한 각 파트너 서버 인스턴스에 대한 데이터베이스 미러링 끝점의 ROLE이 PARTNER 또는 ALL로 설정되어 있어야 합니다. 끝점을 지정 하는 방법에 대 한 정보를 참조 하세요. [만들기는 끝점에 대 한 Windows 인증 데이터베이스 미러링 &#40; Transact SQL &#41; ](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md). 서버 인스턴스에 대한 데이터베이스 미러링 끝점의 역할 및 상태를 확인하려면 해당 인스턴스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하십시오.  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
 **\<_ o p >:: =**  
  
> [!NOTE]  
>  하나의 \<_ o p > SET PARTNER 절 당 허용 됩니다.  
  
 **'** *partner_server* **'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 서버 네트워크 주소가 새 데이터베이스 미러링 세션에서 장애 조치 파트너로 작동하도록 지정합니다. 각 세션에는 각각 주 서버와 미러 서버로 시작할 두 개의 파트너가 필요합니다. 각 파트너는 다른 컴퓨터에 있는 것이 좋습니다.  
  
 이 옵션은 각 파트너에서 세션당 한 번 지정합니다. 두 개의 ALTER DATABASE 권한이 필요 데이터베이스 미러링 세션을 시작 *데이터베이스* SET PARTNER **='***partner_server***'** 문 . 순서가 중요합니다. 첫째, 미러 서버에 연결 하 고으로 주 서버 인스턴스를 지정 *partner_server* (SET PARTNER **='***principal_server***'**). 둘째, 주 서버에 연결 하 고로 미러 서버 인스턴스를 지정 *partner_server* (SET PARTNER **='***mirror_server***'**); 미러링 세션 두 파트너 간에 데이터베이스를 시작 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)을 참조하세요.  
  
 값 *partner_server* 는 서버 네트워크 주소입니다. 구문은 다음과 같습니다.  
  
 TCP**://***\<system-address>***:***\<port>*  
  
 여기서  
  
-   *\<시스템 주소 >* 등 시스템 이름, 정규화 된 도메인 이름 또는 IP 주소를 대상 컴퓨터 시스템을 명확 하 게 식별 하는 문자열입니다.  
  
-   *\<포트 >* 는 파트너 서버 인스턴스의 미러링 끝점과 연결 된 포트 번호입니다.  
  
 자세햔 내용은 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)을 사용합니다.  
  
 다음 예제에서는 SET PARTNER **='***partner_server***'** 절:  
  
```  
'TCP://MYSERVER.mydomain.Adventure-Works.com:7777'  
```  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 대신 ALTER DATABASE 문을 사용하여 세션을 설정한 경우 이 세션은 기본적으로 전체 트랜잭션 보안으로 설정(SAFETY가 FULL로 설정됨)되며 자동 장애 조치(Failover) 없는 보호 우선 모드에서 실행됩니다. 자동 장애 조치를 허용하려면 미러링 모니터 서버를 구성하고 성능 우선 모드로 실행하려면 트랜잭션 보안을 해제합니다(SAFETY OFF).  
  
 FAILOVER  
 수동으로 주 서버에서 미러 서버로 장애 조치를 수행합니다. FAILOVER는 주 서버에서만 지정할 수 있습니다. 이 옵션은 SAFETY가 기본값인 FULL로 설정되어 있는 경우에만 유효합니다.  
  
 장애 조치 옵션을 사용 하려면 **마스터** 데이터베이스 컨텍스트로 합니다.  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS  
 주 서버에서 동기화되지 않은 상태 또는 자동 장애 조치가 수행되지 않는 경우 동기화된 상태의 데이터베이스에 대해 오류가 발생한 경우 데이터베이스 서비스를 미러 데이터베이스에 강제 실행합니다.  
  
 주 서버가 더 이상 실행되지 않는 경우에만 서비스를 강제 실행하는 것이 좋습니다. 그렇지 않은 경우 일부 클라이언트가 새로운 주 데이터베이스가 아닌 원래 주 데이터베이스에 계속 액세스할 수 있습니다.  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS는 다음 조건이 모두 충족된 경우 미러 서버에서만 사용할 수 있습니다.  
  
-   주 서버가 다운되었습니다.  
  
-   WITNESS가 OFF로 설정되어 있거나 미러링 모니터가 미러 서버에 연결되어 있습니다.  
  
 데이터베이스로 서비스를 즉시 복원하기 위해 일부 데이터가 손실되는 위험을 감수하려는 경우에만 서비스를 강제 실행하십시오.  
  
 서비스를 강제로 실행하면 세션이 일시 중지되며 원래 주 데이터베이스의 모든 데이터가 임시로 보존됩니다. 원래 주 데이터베이스가 작동하고 새로운 주 서버와 통신할 수 있게 되면 데이터베이스 관리자가 서비스를 재개할 수 있습니다. 세션이 재개되면 보내지 않은 로그 레코드와 해당 업데이트는 손실됩니다.  
  
 OFF  
 데이터베이스 미러링 세션을 제거하고 데이터베이스에서 미러링을 제거합니다. OFF는 어느 파트너에나 지정할 수 있습니다. 미러링 제거의 영향에 대 한 참조 정보를 참조 하십시오. [데이터베이스 미러링 제거 &#40; SQL Server &#41; ](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
 RESUME  
 일시 중지된 데이터베이스 미러링 세션을 재개합니다. RESUME은 주 서버에서만 지정할 수 있습니다.  
  
 SAFETY { FULL | OFF }  
 트랜잭션 보안의 수준을 설정합니다. SAFETY는 주 서버에서만 지정할 수 있습니다.  
  
 기본값은 FULL입니다. Full 보안을 사용 하면 데이터베이스 미러링 세션이 동기적으로 실행 (에서 *보호 우선 모드*). 보안을 OFF로 설정, 데이터베이스 미러링 세션이 비동기적으로 실행 (에서 *성능 우선 모드*).  
  
 보호 우선 모드의 동작은 부분적으로 미러링 모니터 서버에 따라 다음과 같이 달라집니다.  
  
-   SAFETY를 FULL로 설정하고 세션에 대한 미러링 모니터를 설정하면 세션은 자동 장애 조치(Failover) 있는 보호 우선 모드로 실행됩니다. 주 서버가 손실되면 데이터베이스가 동기화되고 미러 서버 인스턴스 및 미러링 모니터 서버가 서로 연결되어 있는 경우(쿼럼이 있는 경우) 세션이 자동으로 장애 조치됩니다. 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
     세션에 대해 미러링 모니터가 설정되어 있지만 현재 연결되어 있지 않은 경우, 미러 서버가 없으면 주 서버의 작동이 중단됩니다.  
  
-   SAFETY를 FULL로 설정하고 WITNESS를 OFF로 설정하면 세션이 자동 장애 조치(Failover) 없는 보호 우선 모드로 실행됩니다. 미러 서버 인스턴스의 작동이 중단되더라도 주 서버 인스턴스는 아무런 영향을 받지 않습니다. 주 서버 인스턴스의 작동이 중단되면 미러 서버 인스턴스에서 서비스를 강제 실행할 수 있습니다(데이터 손실 가능).  
  
 SAFETY를 OFF로 설정하면 세션은 성능 우선 모드로 실행되며 자동 장애 조치와 수동 장애 조치가 지원되지 않습니다. 그러나 미러 서버에서 발생한 문제가 주 서버에 영향을 주지 않으므로 WITNESS를 OFF로 설정하거나 미러링 모니터가 현재 미러에 연결되어 있으면 주 서버 인스턴스의 작동이 중단될 경우 필요에 따라 미러 서버 인스턴스에서 서비스를 강제 실행할 수 있습니다(데이터 손실 가능). 서비스 강제 실행에 대한 자세한 내용은 이 섹션의 앞부분에 나오는 "FORCE_SERVICE_ALLOW_DATA_LOSS"를 참조하십시오.  
  
> [!IMPORTANT]  
>  성능 우선 모드는 미러링 모니터 사용을 고려한 모드가 아닙니다. 그러나 SAFETY를 OFF로 설정할 때마다 WITNESS를 OFF로 설정하는 것이 좋습니다.  
  
 SUSPEND  
 데이터베이스 미러링 세션을 일시 중지합니다.  
  
 SUSPEND는 어느 파트너에나 지정할 수 있습니다.  
  
 제한 시간 *정수*  
 제한 시간(초)을 지정합니다. 제한 시간은 서버 인스턴스가 미러링 세션 내의 다른 인스턴스로부터 PING 메시지를 받기까지 기다리는 최대 시간으로 이 시간이 경과하면 해당 인스턴스의 연결이 끊어진 것으로 간주합니다.  
  
 TIMEOUT 옵션은 주 서버에서만 지정할 수 있습니다. 이 옵션을 지정하지 않으면 기본적으로 제한 시간은 10초로 설정됩니다. 5 이상을 지정하면 제한 시간은 지정한 초 수로 설정됩니다. 0에서 4까지의 수로 지정하면 제한 시간은 자동으로 5초로 설정됩니다.  
  
> [!IMPORTANT]  
>  제한 시간을 10초 이상으로 유지하는 것이 좋습니다. 10초 미만의 값을 설정하면 로드가 많은 시스템에서 PING을 누락하여 잘못된 실패를 선언할 수 있습니다.  
  
 자세한 내용은 [Possible Failures During Database Mirroring](../../database-engine/database-mirroring/possible-failures-during-database-mirroring.md)을 참조하세요.  
  
 미러링 모니터 \<witness_option >  
 데이터베이스 미러링 모니터를 정의하는 데이터베이스 속성을 제어합니다. SET WITNESS 절은 데이터베이스 복사본 양쪽 모두에 영향을 주지만 SET WITNESS는 주 서버에서만 지정할 수 있습니다. 쿼럼;의 보안 설정에 관계 없이 데이터베이스를 실행 하는 데 필요한는 미러링 모니터 서버는 세션을 설정 하는 경우 자세한 내용은 참조 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향 &#40; 데이터베이스 미러링 &#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)합니다.  
  
 미러링 모니터와 장애 조치 파트너는 별도의 컴퓨터에 있는 것이 좋습니다. 미러링 모니터 서버에 대 한 정보를 참조 하십시오. [Database Mirroring Witness](../../database-engine/database-mirroring/database-mirroring-witness.md)합니다.  
  
 SET WITNESS 문을 실행하려면 주 서버 인스턴스와 미러링 모니터 서버 인스턴스의 끝점에 대한 STATE가 STARTED로 설정되어 있어야 합니다. 또한 미러링 모니터 서버 인스턴스의 데이터베이스 미러링 끝점 ROLE이 WITNESS 또는 ALL로 설정되어 있어야 합니다. 끝점을 지정 하는 방법에 대 한 정보를 참조 하세요. [데이터베이스 미러링 끝점 &#40; SQL Server &#41; ](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
 서버 인스턴스에 대한 데이터베이스 미러링 끝점의 역할 및 상태를 확인하려면 해당 인스턴스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하십시오.  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
> [!NOTE]  
>  미러링 모니터에서는 데이터베이스 속성을 설정할 수 없습니다.  
  
 **\<witness_option >:: =**  
  
> [!NOTE]  
>  하나의 \<witness_option > SET WITNESS 절 당 허용 됩니다.  
  
 **'** *witness_server* **'**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 데이터베이스 미러링 세션에 대한 미러링 모니터 서버로 작동하도록 지정합니다. SET WITNESS 문은 주 서버에서만 지정할 수 있습니다.  
  
 SET witness에서 **='***witness_server***'** 문, 구문의 *witness_server* 의 구문은 동일  *partner_server*합니다.  
  
 OFF  
 데이터베이스 미러링 세션에서 미러링 모니터를 제거합니다. 미러링 모니터를 OFF로 설정하면 자동 장애 조치가 해제됩니다. 데이터베이스가 FULL SAFETY로 설정되어 있고 미러링 모니터가 OFF인 경우 미러 서버에 오류가 발생하면 주 서버는 데이터베이스를 사용할 수 없도록 합니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-database-mirroring-session-with-a-witness"></a>1. 미러링 모니터가 있는 데이터베이스 미러링 세션 만들기  
 미러링 모니터가 있는 데이터베이스 미러링을 설정하려면 보안을 구성하고 미러 데이터베이스를 준비해야 하며 ALTER DATABASE를 사용하여 파트너를 설정해야 합니다. 전체 설치 프로세스의 예제를 보려면 [데이터베이스 미러링 설정 &#40; SQL Server &#41; ](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
### <a name="b-manually-failing-over-a-database-mirroring-session"></a>2. 데이터베이스 미러링 세션의 수동 장애 조치  
 수동 장애 조치는 데이터베이스 미러링 파트너 중 어느 쪽에서든 시작할 수 있습니다. 장애 조치를 수행하기 전에 현재 주 서버로 생각하고 있는 서버가 실제로 주 서버가 맞는지 확인하십시오. 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스인 경우 현재 주 서버라고 생각하는 서버 인스턴스에서 다음 쿼리를 실행합니다.  
  
```  
SELECT db.name, m.mirroring_role_desc   
FROM sys.database_mirroring m   
JOIN sys.databases db  
ON db.database_id = m.database_id  
WHERE db.name = N'AdventureWorks2012';   
GO  
```  
  
 서버 인스턴스가 실제 주 서버이면 `mirroring_role_desc` 값은 `Principal`입니다. 서버 인스턴스가 미러 서버인 경우 `SELECT` 문은 `Mirror`를 반환합니다.  
  
 다음 예에서는 서버를 현재 주 서버로 간주합니다.  
  
1.  데이터베이스 미러링 파트너로의 수동 장애 조치를 수행합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER FAILOVER;  
    GO  
    ```  
  
2.  새 미러에서 장애 조치의 결과를 확인하려면 다음 쿼리를 수행합니다.  
  
    ```  
    SELECT db.name, m.mirroring_role_desc   
    FROM sys.database_mirroring m   
    JOIN sys.databases db  
    ON db.database_id = m.database_id  
    WHERE db.name = N'AdventureWorks2012';   
    GO  
    ```  
  
     `mirroring_role_desc`의 현재 값은 이제 `Mirror`입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)  
  
  
