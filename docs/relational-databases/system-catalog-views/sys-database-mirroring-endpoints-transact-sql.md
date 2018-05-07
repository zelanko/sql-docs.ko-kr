---
title: sys.database_mirroring_endpoints (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 614a57100ffa8e66b1f03757355605409ac5848f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdatabasemirroringendpoints-transact-sql"></a>sys.database_mirroring_endpoints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터베이스 미러링 끝점에 대해 한 행을 포함합니다.  
  
> [!NOTE]  
>  데이터베이스 미러링 끝점이 모두 간의 데이터베이스 미러링 파트너 및 미러링 모니터 서버와 세션 및 Always On 가용성 그룹의 주 복제본과 보조 복제본 간의 세션을 지원 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<열을 상속 >**|—|열을 상속 **sys.endpoints** (자세한 내용은 참조 [sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)).|  
|**role**|**tinyint**|미러링 역할. 다음 중 하나입니다.<br /><br /> **0** = 없음<br /><br /> **1** = partner<br /><br /> **2** = 미러링 모니터<br /><br /> **3** = all<br /><br /> 참고:이 값은 데이터베이스 미러링과 관련이 있습니다.|  
|**role_desc**|**nvarchar(60)**|미러링 역할 설명. 다음 중 하나입니다.<br /><br /> **NONE**<br /><br /> **파트너**<br /><br /> **미러링 모니터 서버**<br /><br /> **ALL**<br /><br /> 참고:이 값은 데이터베이스 미러링과 관련이 있습니다.|  
|**is_encryption_enabled**|**bit**|**1** 암호화는 사용 됨을 의미 합니다.<br /><br /> **0** 암호화는 사용 되지 않는지를 의미 합니다.|  
|**connection_auth**|**tinyint**|이 끝점에 연결하는 데 필요한 연결 인증 유형. 다음 중 하나입니다.<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -협상<br /><br /> **4** -인증서<br /><br /> **5** -NTLM, CERTIFICATE<br /><br /> **6** -KERBEROS, CERTIFICATE<br /><br /> **7** -NEGOTIATE, CERTIFICATE<br /><br /> **8** -CERTIFICATE, NTLM<br /><br /> **9** -CERTIFICATE, KERBEROS<br /><br /> **10** -CERTIFICATE, NEGOTIATE|  
|**connection_auth_desc**|**Nvarchar (60)**|이 끝점에 연결하는 데 필요한 인증 유형 설명. 다음 중 하나입니다.<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE|  
|**certificate_id**|**int**|인증에 사용된 인증서 ID<br /><br /> 0 = Windows 인증 사용 중|  
|**encryption_algorithm**|**tinyint**|암호화 알고리즘. 다음 중 하나입니다.<br /><br /> **0** -NONE<br /><br /> **1** -RC4<br /><br /> **2** – AES<br /><br /> **3** -NONE, RC4<br /><br /> **4** -NONE, AES<br /><br /> **5** -RC4, AES<br /><br /> **6** – AES, RC4<br /><br /> **7** -NONE, RC4, AES<br /><br /> **8** -NONE, AES, RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|암호화 알고리즘에 대한 설명. 다음 중 하나입니다.<br /><br /> 없음<br /><br /> RC4<br /><br /> AES<br /><br /> NONE, RC4<br /><br /> NONE, AES<br /><br /> RC4, AES<br /><br /> AES, RC4<br /><br /> NONE, RC4, AES<br /><br /> NONE, AES, RC4|  
  
## <a name="remarks"></a>주의  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [가용성 복제본 추가 또는 수정 시 끝점 URL 지정 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.database_mirroring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [데이터베이스 미러링 끝점 & #40; SQL Server & #41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
