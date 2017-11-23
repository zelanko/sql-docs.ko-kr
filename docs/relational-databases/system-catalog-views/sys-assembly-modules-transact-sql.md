---
title: sys.assembly_modules (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.assembly_modules
- sys.assembly_modules_TSQL
- assembly_modules
- assembly_modules_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.assembly_modules catalog view
ms.assetid: 5f9e644e-8065-49a2-b53d-db7df98f70d8
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26866a8c8977b4fd707230d59b617b4594725d32
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysassemblymodules-transact-sql"></a>sys.assembly_modules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  CLR(공용 언어 런타임) 어셈블리가 정의한 각 함수, 프로시저 또는 트리거당 한 개의 행을 반환합니다. 이 카탈로그 뷰는 CLR 저장 프로시저, CLR 트리거 또는 CLR 함수를 각각의 기본 구현에 매핑합니다. TA, AF, PC, FS 및 FT 유형의 개체는 하나의 연결된 어셈블리 모듈을 가집니다. 개체 및 어셈블리 간의 연결을 찾기 위해 이 카탈로그 뷰를 다른 카탈로그 뷰에 조인할 수 있습니다. 예를 들어 CLR 저장 프로시저를 만들 때 표시 됩니다 한 행에 **sys.objects**이며 다음 중 하나에 행 **sys.procedures** (에서 상속 되 **sys.objects**), 및 한 행과만 **sys.assembly_modules**합니다. 저장된 프로시저 자체에 메타 데이터에 의해 표현 됩니다 **sys.objects** 및 **sys.procedures**합니다. 프로시저의 기본 CLR 구현에 대 한 참조가 발견 되 **sys.assembly_modules**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|SQL 개체의 식별 번호입니다. 데이터베이스 내에서 고유합니다.|  
|**assembly_id**|**int**|이 모듈이 생성된 어셈블리의 ID입니다.|  
|**assembly_class**|**sysname**|이 모듈을 정의하는 어셈블리 내부의 클래스 이름입니다.|  
|**assembly_method**|**sysname**|내에서 메서드의 이름에서 **assembly_class** 이 모듈을 정의 하는 합니다.<br /><br /> AF(집계 함수)에 대해 NULL입니다.|  
|**null_on_null_input**|**bit**|모든 NULL 입력에 대해 NULL 출력을 만들기 위해 선언된 모듈입니다.|  
|**execute_as_principal_id**|**int**|CLR 함수, 저장 프로시저 또는 트리거의 EXECUTE AS 절이 지정한 대로 컨텍스트 실행이 발생하는 데이터베이스 보안 주체의 ID입니다.<br /><br /> NULL = EXECUTE AS CALLER. 기본값입니다.<br /><br /> 지정한 데이터베이스 보안 주체의 ID = EXECUTE AS SELF, EXECUTE AS *user_name*, 또는 EXECUTE AS *login_name*합니다.<br /><br /> -2 = EXECUTE AS OWNER|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
