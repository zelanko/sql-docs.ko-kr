---
title: TABLE_PRIVILEGES (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- TABLE_PRIVILEGES_TSQL
- TABLE_PRIVILEGES
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.TABLE_PRIVILEGES view
- TABLE_PRIVILEGES view
ms.assetid: 70269d26-b085-4a98-8a9f-b4742c2848bd
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6331c75ff2e3df7980f774d33927e494021b30d
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659993"
---
# <a name="tableprivileges-transact-sql"></a>TABLE_PRIVILEGES(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 현재 사용자에게 부여된 각 테이블 권한 또는 현재 사용자가 부여한 각 테이블 권한당 한 개의 행을 반환합니다.  
  
 이러한 뷰에서 정보를 검색할의 정규화 된 이름을 지정 **INFORMATION_SCHEMA. * * * view_name*합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**GRANTOR**|**nvarchar(** 128 **)**|권한을 부여한 사용자입니다.|  
|**피부 여자에 게**|**nvarchar(** 128 **)**|권한을 부여 받은 사용자입니다.|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|테이블 한정자입니다.|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|테이블이 포함된 스키마의 이름입니다.<br /><br /> **\*\* 중요 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다.|  
|**PRIVILEGE_TYPE**|**varchar (** 10 **)**|권한의 유형입니다.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|피부여자가 다른 사람에게 사용 권한을 부여할 수 있는지 여부를 지정합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [정보 스키마 뷰 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [sys.server_permissions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
  
