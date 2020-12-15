---
description: VIEWS(Transact-SQL)
title: VIEWS (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEWS_TSQL
- VIEWS
dev_langs:
- TSQL
helpviewer_keywords:
- VIEWS view
- INFORMATION_SCHEMA.VIEWS view
ms.assetid: 6119bc94-0b22-45d4-a34b-967afd810a9d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c2e09f62858865c9ae1420efff17b0a3a0de9736
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482428"
---
# <a name="views-transact-sql"></a>VIEWS(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 각 뷰당 하나의 행을 반환합니다.  
  
 이러한 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다 **.** _view_name_.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|뷰 한정자입니다.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|뷰가 포함된 스키마의 이름입니다.<br /><br /> **&#42;&#42; 중요 한 것**  은 개체의 스키마를 찾는 신뢰할 수 있는 방법 으로만 &#42;&#42;하 여 개체의 카탈로그 뷰를 쿼리 하는 것입니다.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|뷰 이름입니다.|  
|**VIEW_DEFINITION**|**nvarchar (** 4000 **)**|정의 길이가 **nvarchar (** 4000 **)** 보다 큰 경우이 열은 NULL입니다. 그렇지 않으면 이 열은 뷰 정의 텍스트입니다.|  
|**CHECK_OPTION**|**varchar (** 7 **)**|WITH CHECK OPTION의 유형입니다. 원래 뷰를 WITH CHECK OPTION으로 만든 경우에는 CASCADE입니다. 그렇지 않으면 NONE이 반환됩니다.|  
|**IS_UPDATABLE**|**varchar (** 2 **)**|뷰를 업데이트할 수 있는지 여부를 지정합니다. 항상 NO를 반환합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](../../t-sql/language-reference.md)   
 [Transact-sql&#41;&#40;정보 스키마 뷰 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
