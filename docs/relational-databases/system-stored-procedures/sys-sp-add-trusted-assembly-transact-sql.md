---
title: sys.sp_add_trusted_assembly (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
caps.latest.revision: ''
author: tmullaney
ms.author: thmullan
manager: craigg
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d71afb0e41469e3b73f65bcb9232733861645476
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysspaddtrustedassembly-transact-sql"></a>sys.sp_add_trusted_assembly (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

서버에 대 한 신뢰할 수 있는 어셈블리의 목록에 어셈블리를 추가합니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>구문
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>주의  

이 절차에서는 어셈블리를 추가 [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)합니다.

## <a name="arguments"></a>인수

[ @hash =] '*값*'  
서버에 대 한 신뢰할 수 있는 어셈블리의 목록에 추가할 어셈블리의 SHA2_512 해시 값입니다. 어셈블리를 로드할 수 때 신뢰할 수 있는 [CLR 엄격한 보안](../../database-engine/configure-windows/clr-strict-security.md) 어셈블리가 서명 되지 않은 경우 또는 데이터베이스 있음으로 표시 되지 않은 경우에 활성화 됩니다.

[ @description =] '*설명*'  
선택적 사용자 정의 설명의 어셈블리입니다. 단순한 이름, 버전 번호, culture, 공개 키 및 신뢰 어셈블리의 아키텍처 등을 인코딩하는 정식 이름을 사용 하는 것이 좋습니다. 이 값은 고유 하 게 공용 언어 런타임 (CLR) 변에 어셈블리를 식별 되며 sys.assemblies clr_name 값과 같습니다. 

## <a name="permissions"></a>Permissions

멤버 자격이 필요는 `sysadmin` 고정된 서버 역할 또는 `CONTROL SERVER` 권한.

## <a name="examples"></a>예  

다음 예에서는 이라는 어셈블리를 추가 `pointudt` 서버에 대 한 신뢰할 수 있는 어셈블리의 목록에 있습니다. 이 값에서 사용할 수 있는 [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)합니다.     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>관련 항목:  
  [sys.sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR 엄격한 보안](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

