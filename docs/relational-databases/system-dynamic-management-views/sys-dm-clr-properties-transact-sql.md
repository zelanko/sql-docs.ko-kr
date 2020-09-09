---
description: sys.dm_clr_properties(Transact-SQL)
title: sys. dm_clr_properties (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7f966cbb5570eb1efb2068d7796ccecb4463750
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551305"
---
# <a name="sysdm_clr_properties-transact-sql"></a>sys.dm_clr_properties(Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  호스팅된 CLR의 버전 및 상태를 포함하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR(공용 언어 런타임) 통합과 관련된 각 속성에 대해 행을 반환합니다. 호스팅된 CLR은 [CREATE assembly](../../t-sql/statements/create-assembly-transact-sql.md), [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md)또는 [DROP assembly](../../t-sql/statements/drop-assembly-transact-sql.md) 문을 실행 하거나 CLR 루틴, 형식 또는 트리거를 실행 하 여 초기화 됩니다. **Dm_clr_properties** 뷰에서는 사용자 clr 코드 실행이 서버에서 사용 하도록 설정 되었는지 여부를 지정 하지 않습니다. [Clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) 옵션이 1로 설정 된 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 저장 프로시저를 사용 하 여 사용자 CLR 코드를 실행할 수 있습니다.  
  
 **Dm_clr_properties** 뷰는 **name** 및 **value** 열을 포함 합니다. 이 뷰의 각 행은 호스팅된 CLR의 속성에 대한 세부 정보를 제공합니다. 이 뷰를 사용하여 CLR 설치 디렉터리, CLR 버전, 호스팅된 CLR의 현재 상태와 같은 호스팅된 CLR에 대한 정보를 수집할 수 있습니다. 이 뷰를 사용하면 서버 컴퓨터에 CLR을 설치할 때 발생하는 문제로 인해 CLR 통합 코드가 작동하지 않고 있는지 확인할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|속성의 이름입니다.|  
|**value**|**nvarchar(128)**|속성의 값입니다.|  
  
## <a name="properties"></a>속성  
 **Directory** 속성은 서버에서 .NET Framework가 설치 된 디렉터리를 나타냅니다. 서버 컴퓨터에 여러 .NET Framework 설치가 있을 수 있으며 이 속성 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 설치를 식별합니다.  
  
 **Version** 속성은 서버에서 .NET Framework 및 호스팅된 CLR의 버전을 나타냅니다.  
  
 **Dm_clr_properties** 동적 관리 뷰는 호스트 된 clr의 상태를 반영 하는 **상태** 속성에 대해 6 개의 다른 값을 반환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 관련 토폴로지는 다음과 같습니다.  
  
-   Mscoree is not loaded.  
  
-   Mscoree is loaded.  
  
-   Locked CLR version with mscoree.  
  
-   CLR is initialized.  
  
-   CLR initialization permanently failed.  
  
-   CLR is stopped.  
  
 **Mscoree.dll이 로드 되지** 않고 **mscoree.dll이 로드** 됨 상태는 서버 시작 시 호스팅된 CLR 초기화의 진행 상태를 표시 하며 볼 수 없습니다.  
  
 호스팅된 clr 버전이 사용 되 고 있지 않아 아직 초기화 되지 않은 상태에서 **문제가 있는 clr 버전이** 표시 될 수 있습니다. 호스트 된 CLR은 DDL 문 (예: [CREATE ASSEMBLY &#40;transact-sql&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) 또는 관리 되는 데이터베이스 개체가 실행 될 때 초기화 됩니다.  
  
 **Clr이 초기화** 됨 상태는 호스팅된 clr이 성공적으로 초기화 되었음을 나타냅니다. 사용자 CLR 코드 실행이 설정되었는지 여부는 나타내지 않습니다. 사용자 CLR 코드 실행이 먼저 활성화 된 다음 sp_configure 저장 프로시저를 사용 하 여 비활성화 된 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 상태 값은 여전히 **CLR이 초기화**됩니다.  
  
 **Clr 초기화가 영구적으로 실패** 상태는 호스팅된 CLR 초기화에 실패 했음을 나타냅니다. 이는 메모리 부족 때문이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 CLR 간의 호스팅 핸드셰이크에서 오류가 발생했기 때문일 수도 있습니다. 이 경우 오류 메시지 6512 또는 6513이 발생합니다.  
  
 **CLR이 중지 됨 상태** 는가 종료 되는 동안에만 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="remarks"></a>설명  
 CLR 통합 기능의 향상 된 기능으로 인해이 뷰의 속성 및 값이의 이후 버전에서 변경 될 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions"></a>사용 권한  
  
에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="examples"></a>예제  
 다음 예에서는 호스팅된 CLR에 대한 정보를 검색합니다.  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [공용 언어 런타임 관련 동적 관리 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
