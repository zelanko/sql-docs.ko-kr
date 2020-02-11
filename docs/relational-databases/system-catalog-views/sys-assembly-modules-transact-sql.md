---
title: sys. assembly_modules (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assembly_modules
- sys.assembly_modules_TSQL
- assembly_modules
- assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_modules catalog view
ms.assetid: 5f9e644e-8065-49a2-b53d-db7df98f70d8
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 68e91d6935549bc8dd421361c092c3ad1fb01905
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118168"
---
# <a name="sysassembly_modules-transact-sql"></a>sys.assembly_modules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  CLR(공용 언어 런타임) 어셈블리가 정의한 각 함수, 프로시저 또는 트리거당 한 개의 행을 반환합니다. 이 카탈로그 뷰는 CLR 저장 프로시저, CLR 트리거 또는 CLR 함수를 각각의 기본 구현에 매핑합니다. TA, AF, PC, FS 및 FT 유형의 개체는 하나의 연결된 어셈블리 모듈을 가집니다. 개체 및 어셈블리 간의 연결을 찾기 위해 이 카탈로그 뷰를 다른 카탈로그 뷰에 조인할 수 있습니다. 예를 들어, CLR 저장 프로시저를 만들 때이 프로시저는 **sys. objects**의 한 행, sys. **프로시저** ( **sys. objects**에서 상속 됨) 및 한 행이 **assembly_modules**에 표시 됩니다. 저장 프로시저 자체는 **sys. objects** 및 **sys. 프로시저**의 메타 데이터로 표시 됩니다. 프로시저의 기본 CLR 구현에 대 한 참조는 **sys. assembly_modules**에 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|SQL 개체의 식별 번호입니다. 데이터베이스 내에서 고유합니다.|  
|**assembly_id**|**int**|이 모듈이 생성된 어셈블리의 ID입니다.|  
|**assembly_class**|**sysname**|이 모듈을 정의하는 어셈블리 내부의 클래스 이름입니다.|  
|**assembly_method**|**sysname**|이 모듈을 정의 하는 **assembly_class** 내의 메서드 이름입니다.<br /><br /> AF(집계 함수)에 대해 NULL입니다.|  
|**null_on_null_input**|**bit**|모든 NULL 입력에 대해 NULL 출력을 만들기 위해 선언된 모듈입니다.|  
|**execute_as_principal_id**|**int**|CLR 함수, 저장 프로시저 또는 트리거의 EXECUTE AS 절이 지정한 대로 컨텍스트 실행이 발생하는 데이터베이스 보안 주체의 ID입니다.<br /><br /> NULL = EXECUTE AS CALLER. 이것이 기본값입니다.<br /><br /> 지정 된 데이터베이스 보안 주체 = EXECUTE AS SELF, EXECUTE AS *user_name*또는 execute as *login_name*의 ID입니다.<br /><br /> -2 = EXECUTE AS OWNER|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
