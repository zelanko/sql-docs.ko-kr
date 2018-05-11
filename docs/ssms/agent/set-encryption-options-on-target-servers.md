---
title: 대상 서버의 암호화 옵션 설정 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 40e37404acd0fd59db0362c53b084b313a5a48e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="set-encryption-options-on-target-servers"></a>대상 서버의 암호화 옵션 설정
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

마스터 서버와 대상 서버 중 일부 또는 모두 간의 SSL(Secure Sockets Layer) 암호화 통신을 위해 인증서를 사용할 수는 없지만 마스터 서버와 대상 서버 간의 채널을 암호화하려는 경우 대상 서버에서 필요한 보안 수준을 사용하도록 구성합니다.  
  
특정 마스터 서버/대상 서버 통신 채널에 필요한 적절한 보안 수준을 구성하려면 대상 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 레지스트리 하위 키 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\**\<*instance_name*>**\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** 를 다음 값 중 하나로 설정합니다. \<*instance_name*>의 값은 **MSSQL.***n*입니다. 예를 들어 **MSSQL.1** 또는 **MSSQL.3**입니다.  
  
|값|Description|  
|---------|---------------|  
|**0**|이 대상 서버와 마스터 서버 간에 암호화를 사용하지 않습니다. 대상 서버와 마스터 서버 간의 채널이 다른 방법으로 보호되는 경우에만 이 옵션을 선택합니다.|  
|**1**|이 대상 서버와 마스터 서버 간에만 암호화를 사용하지만 인증서 확인은 필요하지 않습니다.|  
|**2**|이 대상 서버와 마스터 서버 간에 전체 SSL 암호화와 인증서 확인을 사용합니다. 이 설정이 기본값입니다. 다른 값을 선택할 구체적인 이유가 없으면 이 설정을 변경하지 않는 것이 좋습니다.|  
  
**1** 또는 **2** 를 지정하는 경우 마스터 서버와 대상 서버에서 모두 SSL을 사용해야 합니다. **2** 를 지정하는 경우 마스터 서버에 제대로 서명된 인증서도 있어야 합니다.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>참고 항목  
[방법: 데이터베이스 엔진에 암호화 연결 사용(SQL Server 구성 관리자)](http://msdn.microsoft.com/en-us/e1e55519-97ec-4404-81ef-881da3b42006)  
  
