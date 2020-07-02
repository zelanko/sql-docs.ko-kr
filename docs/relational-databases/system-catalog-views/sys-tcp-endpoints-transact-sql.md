---
title: sys. tcp_endpoints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.tcp_endpoints
- sys.tcp_endpoints_TSQL
- tcp_endpoints
- tcp_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tcp_endpoints catalog view
ms.assetid: 43cc3afa-cced-4463-8e97-fbfdaf2e4fa8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: aa7c9997a8044181c5d60d1efd19c057fc433814
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754445"
---
# <a name="systcp_endpoints-transact-sql"></a>sys.tcp_endpoints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  시스템 내의 각 TCP 엔드포인트당 한 개의 행을 포함합니다. **Sys. tcp_endpoints** 에서 설명 하는 끝점은 연결 권한을 부여 하 고 취소 하는 개체를 제공 합니다. 포트 및 IP 주소와 관련해서 표시되는 정보는 프로토콜을 구성하는 데 사용되지 않으며 실제 프로토콜 구성과 일치하지 않을 수도 있습니다. 프로토콜을 보고 구성하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용합니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**상속 된 열<>**||는 [sys. 끝점](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)에서 열을 상속 합니다.|  
|**port**|int|엔드포인트가 수신 중인 포트 번호입니다. Null을 허용하지 않습니다.|  
|**is_dynamic_port**|bit|1 = 포트 번호가 동적으로 할당되었는지 여부를 나타냅니다.<br /><br /> Null을 허용하지 않습니다.|  
|**ip_address**|**nvarchar (45)**|LISTENER_IP 절에서 지정한 수신기 IP 주소입니다. Null을 허용합니다.|  
  
## <a name="remarks"></a>설명  
 다음 쿼리를 실행하여 엔드포인트 및 연결에 대한 정보를 수집합니다. 현재 연결이 없거나 TCP 연결이 없는 엔드포인트는 NULL 값으로 표시됩니다. **WHERE** 절을 추가 `WHERE des.session_id = @@SPID` 하 여 현재 연결에 대 한 정보를 반환 합니다.  
  
```  
SELECT des.login_name, des.host_name, program_name,  dec.net_transport, des.login_time,   
e.name AS endpoint_name, e.protocol_desc, e.state_desc, e.is_admin_endpoint,   
t.port, t.is_dynamic_port, dec.local_net_address, dec.local_tcp_port   
FROM sys.endpoints AS e  
LEFT JOIN sys.tcp_endpoints AS t  
   ON e.endpoint_id = t.endpoint_id  
LEFT JOIN sys.dm_exec_sessions AS des  
   ON e.endpoint_id = des.endpoint_id  
LEFT JOIN sys.dm_exec_connections AS dec  
   ON des.session_id = dec.session_id;  
```  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [엔드포인트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
