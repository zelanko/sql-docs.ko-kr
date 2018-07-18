---
title: sys.external_libraries (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 110f514c4688536decfd29c412ce310746cd972e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001195"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


Python 또는 R 등의 외부 런타임 관련 패키지 라이브러리의 관리를 지원 합니다.

## <a name="sysexternallibraries"></a>sys.external_libraries

카탈로그 뷰 sys.external_libraries 데이터베이스에 업로드 된 각 외부 라이브러리에 대 한 행을 나열 합니다.

|열 이름 |데이터 형식 | Description|
|------|------|------|
|external_library_id |ssNoversion | 외부 라이브러리 개체의 ID입니다. |
|NAME |sysname |외부 라이브러리의 이름입니다. 소유자 당 데이터베이스 내에서 고유 합니다.|
|principal_id |ssNoversion |이 외부 라이브러리를 소유한 보안 주체의 ID입니다. |
|language | sysname | 외부 라이브러리를 지 원하는 런타임 언어의 이름입니다. 유효한 값은 'R'입니다. 추가 런타임 나중에 추가할 수 있습니다.|
|범위 |ssNoversion |공용 범위 0 전용 범위 1 |  
|scope_desc |varchar(7) |패키지를 공용 또는 개인 인지를 나타냅니다.|


## <a name="see-also"></a>참고자료  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server R Services에 대 한 패키지 관리](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
