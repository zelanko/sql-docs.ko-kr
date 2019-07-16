---
title: OLE Automation 저장 프로시저 (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], OLE Automation
- OLE Automation [SQL Server], stored procedures
ms.assetid: ff16a833-01fe-4877-8aa6-55b72603ec2e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e85a8d988b2f2f17cb77c08ca2c70da1a76164c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941941"
---
# <a name="ole-automation-stored-procedures-transact-sql"></a>OLE Automation 저장 프로시저(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 내에서 OLE Automation 개체를 사용할 수 있는 다음 시스템 저장 프로시저를 지원합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 서버의 보안 구성 중에 OLE Automation 저장 프로시저가 해제되기 때문에 OLE Automation 저장 프로시저에 대한 액세스를 차단합니다. 시스템 관리자는 sp_configure를 사용하여 OLE Automation 프로시저에 대한 액세스를 가능하게 할 수 있습니다. 자세한 내용은 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)을 참조하세요.  
  
|||  
|-|-|  
|[sp_OACreate](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)|[sp_OAMethod](../../relational-databases/system-stored-procedures/sp-oamethod-transact-sql.md)|  
|[sp_OADestroy](../../relational-databases/system-stored-procedures/sp-oadestroy-transact-sql.md)|[sp_OASetProperty](../../relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql.md)|  
|[sp_OAGetErrorInfo](../../relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql.md)|[sp_OAStop](../../relational-databases/system-stored-procedures/sp-oastop-transact-sql.md)|  
|[sp_OAGetProperty](../../relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql.md)|[개체 계층 구조 구문&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/object-hierarchy-syntax-transact-sql.md)|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Ole Automation Procedures 서버 구성 옵션](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
  
