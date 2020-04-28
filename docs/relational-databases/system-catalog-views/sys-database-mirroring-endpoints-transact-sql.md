---
title: sys. database_mirroring_endpoints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bcbe9d23bab18e47b69f82812f604a94d4c5ce9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68022775"
---
# <a name="sysdatabase_mirroring_endpoints-transact-sql"></a>sys.database_mirroring_endpoints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ph x="1" /&gt; 인스턴스의 데이터베이스 미러링 엔드포인트에 대해 한 행을 포함합니다.  
  
> [!NOTE]  
>  데이터베이스 미러링 끝점은 데이터베이스 미러링 파트너와 미러링 모니터 서버 간의 세션을 모두 지원 하며, Always On 가용성 그룹의 주 복제본과 보조 복제본 간의 세션을 모두 지원 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<상속 된 열>**|-|는 **sys.debug** 에서 열을 상속 합니다. 자세한 내용은 [&#41;&#40;transact-sql ](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)을 참조 하세요.|  
|**role**|**tinyint**|미러링 역할. 다음 중 하나입니다.<br /><br /> **0** = 없음<br /><br /> **1** = 파트너<br /><br /> **2** = 미러링 모니터<br /><br /> **3** = 모두<br /><br /> 참고:이 값은 데이터베이스 미러링과만 관련이 있습니다.|  
|**role_desc**|**nvarchar(60)**|미러링 역할 설명. 다음 중 하나입니다.<br /><br /> **없음을**<br /><br /> **당사자**<br /><br /> **감시**<br /><br /> **ALL**<br /><br /> 참고:이 값은 데이터베이스 미러링과만 관련이 있습니다.|  
|**is_encryption_enabled**|**bit**|**1** 은 암호화가 사용 됨을 의미 합니다.<br /><br /> **0** 은 암호화가 사용 되지 않음을 의미 합니다.|  
|**connection_auth**|**tinyint**|이 엔드포인트에 연결하는 데 필요한 연결 인증 유형. 다음 중 하나입니다.<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -NEGOTIATE<br /><br /> **4** -인증서<br /><br /> **5** -NTLM, 인증서<br /><br /> **6** -KERBEROS, 인증서<br /><br /> **7** -협상, 인증서<br /><br /> **8** -인증서, NTLM<br /><br /> **9** -인증서, KERBEROS<br /><br /> **10** -인증서, 협상|  
|**connection_auth_desc**|**nvarchar (60)**|이 엔드포인트에 연결하는 데 필요한 인증 유형 설명. 다음 중 하나입니다.<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> 인증서<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE|  
|**certificate_id**|**int**|인증에 사용된 인증서 ID<br /><br /> 0 = Windows 인증 사용 중|  
|**encryption_algorithm**|**tinyint**|암호화 알고리즘. 다음 중 하나입니다.<br /><br /> **0** -없음<br /><br /> **1** -RC4<br /><br /> **2** -AES<br /><br /> **3** -없음, RC4<br /><br /> **4** -없음, AES<br /><br /> **5** -RC4, AES<br /><br /> **6** -AES, RC4<br /><br /> **7** -없음, RC4, AES<br /><br /> **8** -없음, AES, RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|암호화 알고리즘에 대한 설명. 다음 중 하나입니다.<br /><br /> 없음<br /><br /> RC4<br /><br /> AES<br /><br /> NONE, RC4<br /><br /> NONE, AES<br /><br /> RC4, AES<br /><br /> AES, RC4<br /><br /> NONE, RC4, AES<br /><br /> NONE, AES, RC4|  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [가용성 복제본 &#40;SQL Server를 추가 하거나 수정할 때 끝점 URL을 지정&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [availability_replicas &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [database_mirroring &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [database_mirroring_witnesses &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [데이터베이스 미러링 끝점은 SQL Server을 &#40;&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
