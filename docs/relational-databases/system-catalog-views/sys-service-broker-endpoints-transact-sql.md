---
title: sys. service_broker_endpoints (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 33d94bf5a709c2581c6ee99a1e019f4eebcabe0d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132964"
---
# <a name="sysservice_broker_endpoints-transact-sql"></a>sys.service_broker_endpoints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 카탈로그 뷰에는 각 Service Broker 엔드포인트에 대한 행이 포함되어 있습니다. 이 뷰의 모든 행에는 TCP 구성 메타 데이터를 포함 하는 **tcp_endpoints** 뷰에 동일한 **endpoint_id** 의 해당 행이 있습니다. TCP는 Service Broker에 유일하게 허용되는 프로토콜입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<상속 된 열>**|**--**|[&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)에서 열을 상속 합니다.|  
|**is_message_forwarding_enabled**|**bit**|메시지 전달을 위해 엔드포인트를 지원합니다. 처음에는 **0** (사용 안 함)으로 설정 됩니다. NULL을 허용하지 않습니다.|  
|**message_forwarding_size**|**int**|전달 되는 메시지에 사용할 수 있는 **tempdb** 공간의 최대 크기 (mb)입니다. 처음에는 **10**으로 설정 됩니다. NULL을 허용하지 않습니다.|  
|**connection_auth**|**tinyint**|이 엔드포인트에 연결하는 데 필요한 연결 인증 유형. 다음 중 하나입니다.<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -NEGOTIATE<br /><br /> **4** -인증서<br /><br /> **5** -NTLM, 인증서<br /><br /> **6** -KERBEROS, 인증서<br /><br /> **7** -협상, 인증서<br /><br /> **8** -인증서, NTLM<br /><br /> **9** -인증서, KERBEROS<br /><br /> **10** -인증서, 협상<br /><br /> NULL을 허용하지 않습니다.|  
|**connection_auth_desc**|**nvarchar (60)**|이 엔드포인트에 연결하는 데 필요한 연결 인증 유형에 대한 설명이며 다음 중 하나입니다.<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> 인증서<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE<br /><br /> NULL을 허용합니다.|  
|**certificate_id**|**int**|인증에 사용된 인증서 ID<br /><br /> 0 = Windows 인증 사용 중|  
|**encryption_algorithm**|**tinyint**|암호화 알고리즘입니다. 설명 및 해당 DDL 옵션에 사용할 수 있는 값은 다음과 같습니다.<br /><br /> **0** : 없음. 해당 DDL 옵션: 사용 안 함<br /><br /> **1** : RC4. 해당 DDL 옵션: {필수 &#124; 알고리즘 RC4}.<br /><br /> **2** : AES. 해당 DDL 옵션: 필수 알고리즘 AES.<br /><br /> **3** : 없음, RC4. 해당 DDL 옵션: {지원 되는 &#124; 알고리즘 RC4}.<br /><br /> **4** : 없음, AES. 해당 DDL 옵션: 지원 되는 알고리즘 AES.<br /><br /> **5** : RC4, AES. 해당 DDL 옵션: 필수 알고리즘 RC4 AES.<br /><br /> **6** : AES, RC4. 해당 DDL 옵션: 필수 알고리즘 AES RC4.<br /><br /> **7** : 없음, RC4, AES. 해당 DDL 옵션: 지원 되는 알고리즘 RC4 AES.<br /><br /> **8** : 없음, AES, RC4. 해당 DDL 옵션: 지원 되는 알고리즘 AES RC4.<br /><br /> NULL을 허용하지 않습니다.|  
|**encryption_algorithm_desc**|**nvarchar (60)**|암호화 알고리즘 설명입니다. 가능한 값과 해당 DDL 옵션은 다음과 같습니다.<br /><br /> 없음: 사용 안 함<br /><br /> RC4: {필수 &#124; 필요한 알고리즘 RC4}<br /><br /> AES: 필수 알고리즘 AES<br /><br /> 없음, RC4: {지원 되는 &#124; 지원 되는 알고리즘 RC4}<br /><br /> 없음, AES: 지원 되는 알고리즘 AES<br /><br /> RC4, AES: 필수 알고리즘 RC4 AES<br /><br /> AES, RC4: 필수 알고리즘 AES RC4<br /><br /> 없음, RC4, AES: 지원 되는 알고리즘 RC4 AES<br /><br /> 없음, AES, RC4: 지원 되는 알고리즘 AES RC4<br /><br /> NULL을 허용합니다.|  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. 
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
