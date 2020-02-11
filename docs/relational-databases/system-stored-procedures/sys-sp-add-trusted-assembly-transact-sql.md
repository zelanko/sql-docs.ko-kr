---
title: sys. sp_add_trusted_assembly (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb34a814780a46c12c65948bd0b552effaacda4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72452877"
---
# <a name="syssp_add_trusted_assembly-transact-sql"></a>sys.sp_add_trusted_assembly(Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md.md)]

서버에 대 한 신뢰할 수 있는 어셈블리 목록에 어셈블리를 추가 합니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>구문
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>설명  

이 프로시저는 [trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)에 어셈블리를 추가 합니다.

## <a name="arguments"></a>인수

[ @hash = ] '*value*'  
서버에 대 한 신뢰할 수 있는 어셈블리 목록에 추가할 어셈블리의 SHA2_512 해시 값입니다. 어셈블리가 서명 되지 않았거나 데이터베이스가 신뢰할 수 있는 것으로 표시 되지 않은 경우에도 [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md) 을 사용 하도록 설정 하면 신뢰할 수 있는 어셈블리가 로드 될 수 있습니다.

[ @description = ] '*description*'  
어셈블리에 대 한 선택적 사용자 정의 설명입니다. 신뢰할 수 있는 어셈블리의 단순한 이름, 버전 번호, 문화권, 공개 키 및 아키텍처를 인코딩하는 정식 이름을 사용 하는 것이 좋습니다. 이 값은 CLR (공용 언어 런타임) 쪽에서 어셈블리를 고유 하 게 식별 하며,이 값은 sys. 어셈블리의 clr_name 값과 동일 합니다. 

## <a name="permissions"></a>사용 권한

`sysadmin` 고정 서버 역할 또는 `CONTROL SERVER` 권한의 멤버 자격이 필요 합니다.

## <a name="examples"></a>예  

다음 예제에서는 라는 `pointudt` 어셈블리를 서버에 대 한 신뢰할 수 있는 어셈블리 목록에 추가 합니다. 이러한 값은 [sys. 어셈블리](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)에서 사용할 수 있습니다.     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>참고 항목  
  [sys. sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

