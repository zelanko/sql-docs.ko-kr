---
title: sys.service_broker_endpoints (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_broker_endpoints_TSQL
- service_broker_endpoints
- service_broker_endpoints_TSQL
- sys.service_broker_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_broker_endpoints catalog view
ms.assetid: 6979ec9b-0043-411e-aafb-0226fa26c5ba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f93ac0b4a11e10d3db952fd850f4c83668a97d3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855262"
---
# <a name="sysservicebrokerendpoints-transact-sql"></a>sys.service_broker_endpoints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 카탈로그 뷰에는 각 Service Broker 엔드포인트에 대한 행이 포함되어 있습니다. 이 뷰의 모든 행에 대해 해당 행이 동일한 **endpoint_id** 에 **sys.tcp_endpoints** TCP 구성 메타 데이터를 포함 하는 보기입니다. TCP는 Service Broker에 유일하게 허용되는 프로토콜입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<열을 상속 >**|**--**|열을 상속 [sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)합니다.|  
|**is_message_forwarding_enabled**|**bit**|메시지 전달을 위해 엔드포인트를 지원합니다. 처음으로 설정 됩니다 **0** (사용 안 함). NULL을 허용하지 않습니다.|  
|**message_forwarding_size**|**int**|최대 메가바이트 **tempdb** 공간 전달할 메시지에 사용할 수 있습니다. 처음으로 설정 됩니다 **10**합니다. NULL을 허용하지 않습니다.|  
|**connection_auth**|**tinyint**|이 엔드포인트에 연결하는 데 필요한 연결 인증 유형. 다음 중 하나입니다.<br /><br /> **1** - NTLM<br /><br /> **2** - KERBEROS<br /><br /> **3** -협상<br /><br /> **4** - CERTIFICATE<br /><br /> **5** - NTLM, CERTIFICATE<br /><br /> **6** - KERBEROS, CERTIFICATE<br /><br /> **7** -NEGOTIATE, CERTIFICATE<br /><br /> **8** - CERTIFICATE, NTLM<br /><br /> **9** -CERTIFICATE, KERBEROS<br /><br /> **10** -CERTIFICATE, NEGOTIATE<br /><br /> NULL을 허용하지 않습니다.|  
|**connection_auth_desc**|**nvarchar(60)**|이 엔드포인트에 연결하는 데 필요한 연결 인증 유형에 대한 설명이며 다음 중 하나입니다.<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE<br /><br /> NULL을 허용합니다.|  
|**certificate_id**|**int**|인증에 사용된 인증서 ID<br /><br /> 0 = Windows 인증 사용 중|  
|**encryption_algorithm**|**tinyint**|암호화 알고리즘입니다. 다음은 해당 설명과 해당 DDL 옵션을 사용 하 여 가능한 값입니다.<br /><br /> **0** : NONE. 해당 DDL 옵션: 사용 안 함.<br /><br /> **1** :  RC4. 해당 DDL 옵션: {0} 필요한 &#124; 필요한 알고리즘 RC4}.<br /><br /> **2** : AES입니다. 해당 DDL 옵션: 필요한 알고리즘 AES 사용 합니다.<br /><br /> **3** : -NONE, RC4입니다. 해당 DDL 옵션: {지원 되는 &#124; 지원 되는 알고리즘 RC4}.<br /><br /> **4** : -NONE, AES입니다. 해당 DDL 옵션: 지원 되는 알고리즘 AES입니다.<br /><br /> **5** : RC4, AES. 해당 DDL 옵션: 필요한 알고리즘 RC4 AES입니다.<br /><br /> **6** : AES, RC4. 해당 DDL 옵션: 필요한 알고리즘 AES RC4입니다.<br /><br /> **7** : -NONE, RC4, AES입니다. 해당 DDL 옵션: 지원 되는 알고리즘 RC4 AES입니다.<br /><br /> **8** : -NONE, AES, RC4입니다. 해당 DDL 옵션: 지원 되는 알고리즘 AES RC4입니다.<br /><br /> NULL을 허용하지 않습니다.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|암호화 알고리즘에 대 한 설명입니다. 가능한 값 및 해당 DDL 옵션은 다음과 같습니다.<br /><br /> NONE: 사용 안 함<br /><br /> RC4: {0} 필요한 &#124; 필요한 알고리즘 RC4}<br /><br /> AES: 필요한 알고리즘 AES<br /><br /> -NONE, RC4: {지원 &#124; 지원 되는 알고리즘 RC4}<br /><br /> -NONE, AES: 지원 되는 알고리즘 AES<br /><br /> RC4, AES: 필요한 알고리즘 RC4 AES<br /><br /> AES, RC4: 필요한 알고리즘 AES RC4<br /><br /> -NONE, RC4, AES: 지원 되는 알고리즘 RC4 AES<br /><br /> -NONE, AES, RC4: 지원 되는 알고리즘 AES RC4<br /><br /> NULL을 허용합니다.|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
