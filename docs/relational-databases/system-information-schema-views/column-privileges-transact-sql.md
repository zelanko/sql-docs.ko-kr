---
title: COLUMN_PRIVILEGES (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMN_PRIVILEGES
- COLUMN_PRIVILEGES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMN_PRIVILEGES view
- INFORMATION_SCHEMA.COLUMN_PRIVILEGES view
ms.assetid: 8ae29a85-2b77-48db-a2b9-a1720287b271
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 703d7cb0b225bf12e7ccd91bdf34251c3044230b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67950849"
---
# <a name="column_privileges-transact-sql"></a>COLUMN_PRIVILEGES(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 현재 사용자에게 부여되었거나 현재 사용자가 부여할 권한이 있는 각 열당 한 개의 행을 반환합니다.  
  
 이러한 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다 **.** _view_name_.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**GRANTOR**|**nvarchar (** 128 **)**|권한을 부여한 사용자입니다.|  
|**GRANTEE**|**nvarchar (** 128 **)**|권한을 부여 받은 사용자입니다.|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|테이블 한정자입니다.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|테이블이 포함된 스키마의 이름입니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** INFORMATION_SCHEMA 뷰를 사용 하 여 개체의 스키마를 확인 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다.|  
|**COLUMN_NAME**|**sysname**|열 이름입니다.|  
|**PRIVILEGE_TYPE**|**varchar (** 10 **)**|권한의 유형입니다.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|피부여자가 다른 사람에게 사용 권한을 부여할 수 있는지 여부를 지정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Transact-sql&#41;&#40;정보 스키마 뷰](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys. 개체 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [database_permissions &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [sys.server_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
  
