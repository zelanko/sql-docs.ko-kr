---
title: REFERENTIAL_CONSTRAINTS (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 789b63a29e061b11d261d2cfb89165d61b9cab27
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666242"
---
# <a name="referentialconstraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 각 FOREIGN KEY 제약 조건당 하나의 행을 반환합니다. 이 정보 스키마 뷰는 현재 사용자가 사용 권한을 갖고 있는 개체에 대한 정보를 반환합니다.  
  
 이러한 뷰에서 정보를 검색할의 정규화 된 이름을 지정 **INFORMATION_SCHEMA. * * * view_name*합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|제약 조건 한정자입니다.|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|제약 조건이 포함된 스키마의 이름입니다.<br /><br /> **\*\* 중요 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**제약 조건 이름**|**sysname**|제약 조건 이름입니다.|  
|**UNIQUE_CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|UNIQUE 제약 조건의 한정자입니다.|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|UNIQUE 상수가 포함된 스키마의 이름입니다.<br /><br /> **\*\* 중요 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|UNIQUE 제약 조건입니다.|  
|**MATCH_OPTION**|**varchar (** 7 **)**|참조 제약 일치 조건이며 항상 SIMPLE을 반환합니다. 이는 일치 조건을 정의하지 않음을 의미합니다. 다음 중 하나가 TRUE인 경우에 조건이 일치하는 것으로 간주됩니다.<br /><br /> 외래 키 열에서 적어도 하나의 값이 NULL인 경우<br /><br /> 외래 키 열의 모든 값이 NULL이 아니며 기본 키 테이블에 키가 일치하는 행이 있는 경우|  
|**UPDATE_RULE**|**varchar (** 11 **)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 현재 제약 조건에서 정의한 참조 무결성을 위반하는 경우에 수행되는 동작입니다. 다음 중 하나를 반환합니다. <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> 현재 제약 조건의 ON UPDATE에 대해 NO ACTION이 지정된 경우에는 제약 조건에서 참조되는 기본 키 업데이트가 외래 키로 전파되지 않습니다. 적어도 하나의 외래 키가 같은 값을 포함하여 기본 키의 해당 업데이트가 참조 무결성을 위반하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 부모 테이블 및 참조하는 테이블에 대해 어떠한 변경 사항도 적용하지 않습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 발생합니다.<br /><br /> 현재 제약 조건의 ON UPDATE에 대해 CASCADE가 지정된 경우에는 기본 키 값에 대한 모든 변경 사항이 자동으로 외래 키 값으로 전파됩니다.|  
|**DELETE_RULE**|**varchar (** 11 **)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 현재 제약 조건에서 정의한 참조 무결성을 위반하는 경우에 수행되는 동작입니다. 다음 중 하나를 반환합니다. <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> 현재 제약 조건의 ON DELETE에 대해 NO ACTION이 지정된 경우에는 제약 조건에서 참조되는 기본 키에 대한 삭제가 외래 키로 전파되지 않습니다. 적어도 하나의 외래 키가 같은 값을 포함하여 기본 키의 해당 삭제가 참조 무결성을 위반하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 부모 테이블 및 참조하는 테이블에 대해 어떠한 변경 사항도 적용하지 않습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 발생합니다.<br /><br /> 현재 제약 조건의 ON DELETE에 대해 CASCADE가 지정된 경우에는 기본 키 값에 대한 모든 변경 사항이 자동으로 외래 키 값으로 전파됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [정보 스키마 뷰 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.foreign_keys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
