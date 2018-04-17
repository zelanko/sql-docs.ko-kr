---
title: sp_enumdsn (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 471fa93ccd1c9e48f0baa1fa270a7a7db7b7d4af
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spenumdsn-transact-sql"></a>sp_enumdsn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 계정으로 실행 중인 서버에 대해 정의된 모든 ODBC 및 OLE DB 데이터 원본 이름의 목록을 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**데이터 원본 이름**|**sysname**|데이터 원본의 이름입니다.|  
|**설명**|**varchar(255)**|데이터 원본에 대한 설명입니다.|  
|**형식**|**int**|데이터 원본의 유형입니다.<br /><br /> **1** ODBC DSN =<br /><br /> **3** = OLE DB 데이터 원본|  
|**공급자 이름**|**varchar(255)**|OLE DB Provider의 이름입니다. ODBC DSN에 대한 값은 NULL입니다.|  
  
## <a name="remarks"></a>주의  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에는 사용자 컨텍스트가 있습니다. 사용자 컨텍스트는 사용자에 대한 ODBC 데이터 원본의 정의를 포함하는 레지스트리 항목의 집합입니다. 사용자 컨텍스트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행 중인 사용자 이름에 의해 제공됩니다.  
  
 예를 들어 서버가 시스템 계정 사용자 컨텍스트로 실행 중인 경우 반환된 DSN(데이터 원본 이름)은 모두 시스템 계정과 연결된 시스템 DSN입니다. 서버가 개인 사용자 계정으로 실행 중인 경우에는 해당 사용자의 개인 계정에 대해 정의된 DSN만 반환됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_enumdsn**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_dsninfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
