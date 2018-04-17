---
title: sys.external_libraries (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_libraries catalog view
author: jeannt
ms.author: jeannt
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d8fa8a4d41cff452379c420b712f13b2d4415a74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


패키지 라이브러리와 관련 된 외부 런타임 Python 또는 R 등의 관리를 지원 합니다.

## <a name="sysexternallibraries"></a>sys.external_libraries

카탈로그 뷰 sys.external_libraries 데이터베이스에 업로드 된 각 외부 라이브러리에 대 한 행을 나열 합니다.

|열 이름 |데이터 형식 | Description|
|------|------|------|
|external_library_id |int | 외부 라이브러리 개체의 ID입니다. |
|name |sysname |외부 라이브러리의 이름입니다. 소유자 당 데이터베이스 내에서 고유 합니다.|
|principal_id |int |이 외부 라이브러리를 담당 하는 보안 주체의 ID입니다. |
|language | sysname | 언어 또는 외부 라이브러리를 지 원하는 런타임의 이름입니다. 유효한 값은 'R'입니다. 추가 런타임 나중에 추가할 수 있습니다.|
|범위 |int |공용 범위;에 대 한 0 개인 범위에 대 한 1 |  
|scope_desc |varchar(7) |패키지 공개 또는 개인 인지를 나타냅니다.|


## <a name="see-also"></a>참고 항목  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server R Services에 대 한 패키지 관리](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
