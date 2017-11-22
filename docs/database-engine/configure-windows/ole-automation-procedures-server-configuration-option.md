---
title: "Ole Automation Procedures 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e82c541515d90053a727c3c7fa0f9d820e218e42
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Ole Automation Procedures 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **Ole Automation Procedures** 옵션을 사용하여 OLE 자동화 개체가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 내에서 인스턴스화될 수 있는지 여부를 지정할 수 있습니다. 이 옵션은 정책 기반 관리 또는 **sp_configure** 저장 프로시저를 사용하여 구성할 수도 있습니다. 자세한 내용은 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)을 참조하세요.  
  
 **Ole Automation Procedures** 옵션을 다음 값으로 설정할 수 있습니다.  
  
 0  
 OLE Automation Procedures가 해제되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 인스턴스에 대한 기본값입니다.  
  
 1  
 OLE Automation Procedures가 설정되어 있습니다.  
  
 OLE Automation Procedures가 설정되어 있는 경우 **sp_OACreate** 를 호출하면 OLE 공유 실행 환경이 시작됩니다.  
  
 **Ole Automation Procedures** 옵션의 현재 값은 **sp_configure** 시스템 저장 프로시저를 사용하여 보고 변경할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 OLE Automation procedures의 현재 설정을 보는 방법을 보여 줍니다.  
  
```  
EXEC sp_configure 'Ole Automation Procedures';  
GO  
```  
  
 다음 예에서는 OLE Automation procedures를 설정하는 방법을 보여 줍니다.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Ole Automation Procedures', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
