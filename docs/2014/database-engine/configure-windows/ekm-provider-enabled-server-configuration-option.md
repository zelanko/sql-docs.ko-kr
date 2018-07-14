---
title: EKM provider enabled 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- external encryption provider
helpviewer_keywords:
- EKM provider enabled option
ms.assetid: da58ed50-3a13-4172-9065-960559d8f383
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b1fc278d0f2b5a7f848118576d66e5577ec1a882
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226263"
---
# <a name="ekm-provider-enabled-server-configuration-option"></a>EKM provider enabled 서버 구성 옵션
  `EKM provider enabled` 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 Extensible Key Management 장치 지원을 제어합니다. 기본적으로 이 옵션은 해제되어 있습니다.  
  
 이 기능을 사용하거나 사용하지 않도록 설정하려면 다음 `sp_configure` 명령 중 하나를 실행하십시오.  
  
```  
/* Enable the external encryption provider option */  
sp_configure 'EKM provider enabled', 1  
/* Disable the external encryption provider option */  
sp_configure 'EKM provider enabled', 0  
```  
  
> [!NOTE]  
>  이 옵션은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
