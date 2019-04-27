---
title: Ole Automation Procedures 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f00c238dfb32089261c51936b3937b0657c58b08
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62782031"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Ole Automation Procedures 서버 구성 옵션
  `Ole Automation Procedures` 옵션을 사용하여 OLE Automation 개체가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 내에서 인스턴스화될 수 있는지 여부를 지정할 수 있습니다. 이 옵션은 정책 기반 관리 또는 **sp_configure** 저장 프로시저를 사용하여 구성할 수도 있습니다. 자세한 내용은 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)을 참조하세요.  
  
 `Ole Automation Procedures` 옵션을 다음 값으로 설정할 수 있습니다.  
  
 0  
 OLE Automation Procedures가 해제되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 인스턴스에 대한 기본값입니다.  
  
 1  
 OLE Automation Procedures가 설정되어 있습니다.  
  
 OLE Automation Procedures가 설정되어 있는 경우 **sp_OACreate** 를 호출하면 OLE 공유 실행 환경이 시작됩니다.  
  
 현재 값을 `Ole Automation Procedures` 옵션 확인 및 사용 하 여 변경할 수는 **sp_configure** 시스템 저장 프로시저입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
