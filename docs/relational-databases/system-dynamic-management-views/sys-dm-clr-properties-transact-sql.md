---
title: sys.dm_clr_properties (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs: TSQL
helpviewer_keywords: sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb5c73dafd26f9ddd4da885b77c8649df13c3d2d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  호스팅된 CLR의 버전 및 상태를 포함하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR(공용 언어 런타임) 통합과 관련된 각 속성에 대해 행을 반환합니다. 호스팅된 CLR은를 실행 하 여 초기화는 [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md), [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md), 또는 [DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md) 문, 또는 모든 CLR 루틴, 형식 또는 트리거를 실행 하 여 합니다. **sys.dm_clr_properties** 보기에는 서버에서 사용자 CLR 코드 실행을 사용 하는지 여부를 지정 하지 않습니다. 사용자 CLR 코드 실행을 사용 하 여 사용할지는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 함께 저장 프로시저는 [사용 하도록 설정 하는 clr](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) 옵션이 1로 설정 합니다.  
  
 **sys.dm_clr_properties** 뷰에 **이름** 및 **값** 열입니다. 이 뷰의 각 행은 호스팅된 CLR의 속성에 대한 세부 정보를 제공합니다. 이 뷰를 사용하여 CLR 설치 디렉터리, CLR 버전, 호스팅된 CLR의 현재 상태와 같은 호스팅된 CLR에 대한 정보를 수집할 수 있습니다. 이 뷰를 사용하면 서버 컴퓨터에 CLR을 설치할 때 발생하는 문제로 인해 CLR 통합 코드가 작동하지 않고 있는지 확인할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (128)**|속성의 이름입니다.|  
|**값**|**nvarchar (128)**|속성의 값입니다.|  
  
## <a name="properties"></a>속성  
 **디렉터리** 속성은 서버에서.NET Framework를 설치 된 디렉터리를 나타냅니다. 서버 컴퓨터에 여러 .NET Framework 설치가 있을 수 있으며 이 속성 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 설치를 식별합니다.  
  
 **버전** .NET Framework의 버전을 나타내는 속성과 서버에서 CLR을 호스트 합니다.  
  
 **sys.dm_clr_properties** 동적 관리 뷰는에 대 한 다음 6 개 값을 반환할 수 있습니다는 **상태** 속성의 상태를 반영 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호스팅된 CLR 합니다. 반환할 수 있습니다.  
  
-   Mscoree is not loaded.  
  
-   Mscoree is loaded.  
  
-   Locked CLR version with mscoree.  
  
-   CLR is initialized.  
  
-   CLR initialization permanently failed.  
  
-   CLR is stopped.  
  
 **Mscoree가 로드 되지 않았습니다.** 및 **Mscoree가 로드** 상태 서버 시작 시 호스팅된 CLR 초기화의 진행 상황을 표시 및 표시 될 가능성은 거의 없습니다.  
  
 **mscoree와 잠긴 CLR 버전** 상태로 나타날 수 있는 호스팅된 CLR 되 고 사용 되지 않으며, 따라서 초기화 되지 않은 아직 되었습니다. 호스팅된 CLR 초기화 되는 처음으로 DDL 문 (같은 [CREATE assembly&#40; Transact SQL &#41; ](../../t-sql/statements/create-assembly-transact-sql.md)) 관리 되는 데이터베이스 개체가 실행 되는지 또는 합니다.  
  
 **CLR이 초기화** 상태는 호스팅된 CLR 성공적으로 초기화 되었음을 나타냅니다. 사용자 CLR 코드 실행이 설정되었는지 여부는 나타내지 않습니다. 사용자 CLR 코드의 실행이 처음 사용 하 고 다음 사용 하 여 사용 하지 않도록 설정 된 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 저장된 프로시저, 상태 값 계속 됩니다 **CLR이 초기화 되**합니다.  
  
 **CLR 초기화 하지 못했습니다 영구적으로** 상태는 호스팅된 CLR 나타냅니다 초기화 하지 못했습니다. 이는 메모리 부족 때문이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 CLR 간의 호스팅 핸드셰이크에서 오류가 발생했기 때문일 수도 있습니다. 이 경우 오류 메시지 6512 또는 6513이 발생합니다.  
  
 **CLR 중지 된 상태** 은 경우에 표시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 종료 합니다.  
  
## <a name="remarks"></a>주의  
 속성 및 값이이 보기의 나중 버전의에서 변경 될 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR 통합 기능의 향상 된 기능으로 인해 합니다.  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 대 한 VIEW SERVER STATE 권한이 필요 합니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 프리미엄 계층 데이터베이스에서 VIEW DATABASE STATE 권한이 필요 합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 표준 및 기본 계층 필요는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 관리자 계정.  
  
## <a name="examples"></a>예  
 다음 예에서는 호스팅된 CLR에 대한 정보를 검색합니다.  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [공용 언어 런타임 관련 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
