---
title: sp_enumdsn (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: stevestein
ms.author: sstein
ms.openlocfilehash: d84d366483cd5a887eb299b0f8d9208998e835c1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124586"
---
# <a name="sp_enumdsn-transact-sql"></a>sp_enumdsn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 계정으로 실행 중인 서버에 대해 정의된 모든 ODBC 및 OLE DB 데이터 원본 이름의 목록을 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**데이터 원본 이름**|**sysname**|데이터 원본의 이름입니다.|  
|**설명**|**varchar(255)**|데이터 원본에 대한 설명입니다.|  
|**Type**|**int**|데이터 원본의 유형입니다.<br /><br /> **1** = ODBC DSN<br /><br /> **3** = OLE DB 데이터 원본|  
|**공급자 이름**|**varchar(255)**|OLE DB Provider의 이름입니다. ODBC DSN에 대한 값은 NULL입니다.|  
  
## <a name="remarks"></a>설명  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에는 사용자 컨텍스트가 있습니다. 사용자 컨텍스트는 사용자에 대한 ODBC 데이터 원본의 정의를 포함하는 레지스트리 항목의 집합입니다. 사용자 컨텍스트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행 중인 사용자 이름에 의해 제공됩니다.  
  
 예를 들어 서버가 시스템 계정 사용자 컨텍스트로 실행 중인 경우 반환된 DSN(데이터 원본 이름)은 모두 시스템 계정과 연결된 시스템 DSN입니다. 서버가 프라이빗 사용자 계정으로 실행 중인 경우에는 해당 사용자의 프라이빗 계정에 대해 정의된 DSN만 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_enumdsn**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_dsninfo &#40;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
