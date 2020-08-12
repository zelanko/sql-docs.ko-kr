---
title: 대상 서버의 암호화 옵션 설정
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ee53a4f973537dad629a24bb442e8a1076eebd11
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85644525"
---
# <a name="set-encryption-options-on-target-servers"></a>대상 서버의 암호화 옵션 설정
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

마스터 서버와 대상 서버 중 일부 또는 전부 간의 TLS(전송 계층 보안)(이전에는 SSL(Secure Sockets Layer)이라고 함) 암호화 통신을 위해 인증서를 사용할 수는 없지만 마스터 서버와 대상 서버 간의 채널을 암호화하려는 경우 대상 서버에서 필요한 보안 수준을 사용하도록 구성합니다.  
  
특정 마스터 서버/대상 서버 통신 채널에 필요한 적절한 보안 수준을 구성하려면 대상 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 레지스트리 하위 키 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\** \<*instance_name*> **\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** 를 다음 값 중 하나로 설정합니다. \<*instance_name*> 값이 **MSSQL.** _n_입니다. 예를 들어 **MSSQL.1** 또는 **MSSQL.3**입니다.  
  
|값|Description|  
|---------|---------------|  
|**0**|이 대상 서버와 마스터 서버 간에 암호화를 사용하지 않습니다. 대상 서버와 마스터 서버 간의 채널이 다른 방법으로 보호되는 경우에만 이 옵션을 선택합니다.|  
|**1**|이 대상 서버와 마스터 서버 간에만 암호화를 사용하지만 인증서 확인은 필요하지 않습니다.|  
|**2**|이 대상 서버와 마스터 서버 간에 전체 TLS 암호화와 인증서 확인을 사용합니다. 이 설정은 기본값입니다. 다른 값을 선택할 구체적인 이유가 없으면 이 설정을 변경하지 않는 것이 좋습니다.|  
  
**1** 또는 **2**를 지정하는 경우 마스터 서버와 대상 서버 모두 TLS를 사용해야 합니다. **2** 를 지정하는 경우 마스터 서버에 제대로 서명된 인증서도 있어야 합니다.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>참고 항목  
[방법: 데이터베이스 엔진에 암호화 연결 사용(SQL Server 구성 관리자)](https://msdn.microsoft.com/e1e55519-97ec-4404-81ef-881da3b42006)  
  
