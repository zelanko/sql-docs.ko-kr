---
title: sp_upgrade_log_shipping (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_upgrade_log_shipping
- sp_upgrade_log_shipping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_upgrade_log_shipping
ms.assetid: ee01092f-9caf-4e88-888b-ec7b84223705
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e96326c97dde209f37104e66e562b66e96c8acd3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82809105"
---
# <a name="sp_upgrade_log_shipping-transact-sql"></a>sp_upgrade_log_shipping(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 전달과 관련 된 메타 데이터를 업그레이드 하기 위해 sp_upgrade_log_shipping 저장 프로시저는 자동으로 호출 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_upgrade_log_shipping  
```  
  
## <a name="arguments"></a>인수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(기타)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 이 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 중에 로그 전달과 관련된 메타데이터 업그레이드를 위해 자동으로 호출됩니다. 업그레이드 중 메타데이터 문제가 발생하지 않으면 이 프로시저를 명시적으로 실행할 필요가 없습니다.  
  
 sp_upgrade_log_shipping은 주 서버 또는 모니터 서버에 있는 master 데이터베이스에서 실행해야 합니다.  
  
## <a name="permissions"></a>권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
