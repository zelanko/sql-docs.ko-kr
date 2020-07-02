---
title: sys. sp_drop_trusted_assembly (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_drop_trusted_assembly_TSQL
- sp_drop_trusted_assembly
- sys.sp_drop_trusted_assembly_TSQL
- sys.sp_drop_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_drop_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4dbeed2c84db6a94237df6878fba688c6ed08a66
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85625948"
---
# <a name="syssp_drop_trusted_assembly-transact-sql"></a>sys.sp_drop_trusted_assembly(Transact-SQL)  
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

서버에 있는 신뢰할 수 있는 어셈블리 목록에서 어셈블리를 삭제 합니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>구문
```  
sp_drop_trusted_assembly 
    [ @hash = ] 'value'
```  

## <a name="arguments"></a>인수

[ @hash =] '*value*'  
서버에 대 한 신뢰할 수 있는 어셈블리 목록에서 삭제할 어셈블리의 SHA2_512 해시 값입니다. 어셈블리가 서명 되지 않았거나 데이터베이스가 신뢰할 수 있는 것으로 표시 되지 않은 경우에도 clr strict security를 사용 하도록 설정 하면 신뢰할 수 있는 어셈블리가 로드 될 수 있습니다.

## <a name="remarks"></a>설명  

이 프로시저는 [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)에서 어셈블리를 제거 합니다.

## <a name="permissions"></a>사용 권한

`sysadmin`고정 서버 역할 또는 권한의 멤버 자격이 필요 `CONTROL SERVER` 합니다.

## <a name="examples"></a>예제  

다음 예에서는 서버에 대 한 신뢰할 수 있는 어셈블리 목록에서 어셈블리 해시를 삭제 합니다.  

```  
EXEC sp_drop_trusted_assembly 
0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC; 
```  

## <a name="see-also"></a>참고 항목  
  [sp_add_trusted_assembly](sys-sp-add-trusted-assembly-transact-sql.md) [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) [DROP assembly &#40;transact-sql&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

