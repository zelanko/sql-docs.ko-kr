---
title: sp_syscollector_set_warehouse_instance_name (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_warehouse_instance_name_TSQL
- sp_syscollector_set_warehouse_instance_name
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_warehouse_instance_name
ms.assetid: 5320fcd4-bed1-468f-b784-a5e10fcfaeb6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6e21096971b9a0891d2c51c5fce34c119b454f0b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68010592"
---
# <a name="sp_syscollector_set_warehouse_instance_name-transact-sql"></a>sp_syscollector_set_warehouse_instance_name(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  관리 데이터 웨어하우스에 연결하는 데 사용되는 연결 문자열의 인스턴스 이름을 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_set_warehouse_instance_name [ @instance_name = ] 'instance_name'  
```  
  
## <a name="arguments"></a>인수  
 [ @instance_name = ] '*instance_name*'  
 인스턴스 이름입니다. *instance_name* 는 **sysname** 이며 NULL 인 경우 로컬 인스턴스에 대 한 기본값입니다.  
  
> **참고:**  _instance_name_ 은 *computerName*\\*instanceName*형식의 컴퓨터 이름과 인스턴스 이름으로 구성 된 정규화 된 인스턴스 이름 이어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 이 데이터 수집기 차원의 구성을 변경하기 전에 데이터 수집기를 해제해야 합니다. 데이터 수집기를 사용하는 경우 이 프로시저가 실패합니다.  
  
 현재 인스턴스 이름을 보려면 [syscollector_config_store](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md) 시스템 뷰를 쿼리 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 이 예에서는 원격 서버에서 관리 데이터 웨어하우스 인스턴스를 사용하도록 데이터 수집기를 구성하는 방법을 보여 줍니다. 이 예에서 원격 서버의 이름은 `RemoteSERVER`이며 데이터베이스는 기본 인스턴스에 설치되어 있습니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_set_warehouse_instance_name N'RemoteSERVER'; -- the default instance is assumed on the remote server  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;데이터 수집기 저장 프로시저](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_config_store&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)  
  
  
