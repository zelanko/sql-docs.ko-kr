---
title: REFERENTIAL_CONSTRAINTS (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- REFERENTIAL_CONSTRAINTS
- REFERENTIAL_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS view
- REFERENTIAL_CONSTRAINTS view
ms.assetid: 5d358f18-0a85-4b55-af4b-98d5f4cd1020
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 750850c9e01720b5f345f720e3a9f13db8fcd9f0
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669512"
---
# <a name="referential_constraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 각 FOREIGN KEY 제약 조건당 하나의 행을 반환합니다. 이 정보 스키마 뷰는 현재 사용자가 사용 권한을 갖고 있는 개체에 대한 정보를 반환합니다.  
  
 이러한 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다 **.** _view_name_.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|제약 조건 한정자입니다.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|제약 조건이 포함된 스키마의 이름입니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** INFORMATION_SCHEMA 뷰를 사용 하 여 개체의 스키마를 확인 하지 마십시오. INFORMATION_SCHEMA 뷰는 개체의 메타 데이터 하위 집합만을 나타냅니다. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**CONSTRAINT_NAME**|**sysname**|제약 조건 이름입니다.|  
|**UNIQUE_CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|UNIQUE 제약 조건의 한정자입니다.|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|UNIQUE 상수가 포함된 스키마의 이름입니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** INFORMATION_SCHEMA 뷰를 사용 하 여 개체의 스키마를 확인 하지 마십시오. INFORMATION_SCHEMA 뷰는 개체의 메타 데이터 하위 집합만을 나타냅니다. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|UNIQUE 제약 조건입니다.|  
|**MATCH_OPTION**|**varchar (** 7 **)**|참조 제약 일치 조건이며 항상 SIMPLE을 반환합니다. 이는 일치 조건을 정의하지 않음을 의미합니다. 다음 중 하나가 TRUE인 경우에 조건이 일치하는 것으로 간주됩니다.<br /><br /> 외래 키 열에서 적어도 하나의 값이 NULL인 경우<br /><br /> 외래 키 열의 모든 값이 NULL이 아니며 기본 키 테이블에 키가 일치하는 행이 있는 경우|  
|**UPDATE_RULE**|**varchar (** 11 **)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 현재 제약 조건에서 정의한 참조 무결성을 위반하는 경우에 수행되는 동작입니다. 다음 중 하나를 반환합니다. <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> 현재 제약 조건의 ON UPDATE에 대해 NO ACTION이 지정된 경우에는 제약 조건에서 참조되는 기본 키 업데이트가 외래 키로 전파되지 않습니다. 적어도 하나의 외래 키가 같은 값을 포함하여 기본 키의 해당 업데이트가 참조 무결성을 위반하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 부모 테이블 및 참조하는 테이블에 대해 어떠한 변경 사항도 적용하지 않습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 발생합니다.<br /><br /> 현재 제약 조건의 ON UPDATE에 대해 CASCADE가 지정된 경우에는 기본 키 값에 대한 모든 변경 사항이 자동으로 외래 키 값으로 전파됩니다.|  
|**DELETE_RULE**|**varchar (** 11 **)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 현재 제약 조건에서 정의한 참조 무결성을 위반하는 경우에 수행되는 동작입니다. 다음 중 하나를 반환합니다. <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> 현재 제약 조건의 ON DELETE에 대해 NO ACTION이 지정된 경우에는 제약 조건에서 참조되는 기본 키에 대한 삭제가 외래 키로 전파되지 않습니다. 적어도 하나의 외래 키가 같은 값을 포함하여 기본 키의 해당 삭제가 참조 무결성을 위반하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 부모 테이블 및 참조하는 테이블에 대해 어떠한 변경 사항도 적용하지 않습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 발생합니다.<br /><br /> 현재 제약 조건의 ON DELETE에 대해 CASCADE가 지정된 경우에는 기본 키 값에 대한 모든 변경 사항이 자동으로 외래 키 값으로 전파됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Transact-sql&#41;&#40;정보 스키마 뷰](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys. 개체 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [foreign_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
