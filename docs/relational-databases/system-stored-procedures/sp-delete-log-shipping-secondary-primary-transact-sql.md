---
title: sp_delete_log_shipping_secondary_primary (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_secondary_primary_TSQL
- sp_delete_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_secondary_primary
ms.assetid: 507fc744-73d9-4cb7-8d2a-bcff88841c6a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f389e6fa58feba189955c3ac8f654a906f61588f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009143"
---
# <a name="spdeletelogshippingsecondaryprimary-transact-sql"></a>sp_delete_log_shipping_secondary_primary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 보조 서버에서 지정된 주 서버에 대한 정보를 제거하고 보조 서버에서 복사 및 복원 작업을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server'  
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>인수  
`[ @primary_server = ] 'primary_server'` 기본 인스턴스 이름을 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성에서 합니다. *primary_server* 됩니다 **sysname** NULL 일 수 없습니다.  
  
`[ @primary_database = ] 'primary_database'` 주 서버에서 데이터베이스의 이름이입니다. *primary_database* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 **sp_delete_log_shipping_secondary_primary** 에서 실행 해야 합니다 **마스터** 보조 서버의 데이터베이스. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  보조 ID에 대한 복사 및 복원 작업을 삭제합니다.  
  
2.  항목을 삭제 **log_shipping_secondary**합니다.  
  
3.  호출 **sp_delete_log_shipping_alert_job** 모니터 서버에 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
