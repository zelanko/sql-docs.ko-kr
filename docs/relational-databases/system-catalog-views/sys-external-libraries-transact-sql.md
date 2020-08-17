---
description: sys.external_libraries(Transact-SQL)
title: sys. external_libraries (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 6dcc1b8f7cddc785203dc2430c2f1a4dce4b4d39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377579"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries(Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

는 R, Python 및 Java와 같은 외부 런타임과 관련 된 패키지 라이브러리의 관리를 지원 합니다.

> [!NOTE]
> SQL Server 2017에서는 R 언어 및 Windows 플랫폼이 지원됩니다. Windows 및 Linux 플랫폼의 R, Python 및 Java는 SQL Server 2019 이상에서 지원됩니다. Azure SQL Managed Instance에서 R 및 Python이 지원 됩니다.

## <a name="sysexternal_libraries"></a>sys.external_libraries

카탈로그 뷰 sys. external_libraries는 데이터베이스에 업로드 된 각 외부 라이브러리의 행을 나열 합니다.

|열 이름 |데이터 형식 | Description|
|------|------|------|
|external_library_id |int | 외부 라이브러리 개체의 ID입니다. |
|name |sysname |외부 라이브러리의 이름입니다. 는 소유자 당 데이터베이스 내에서 고유 합니다.|
|principal_id |int |이 외부 라이브러리를 소유 하는 보안 주체의 ID입니다. |
|language | sysname | 외부 라이브러리를 지 원하는 언어나 런타임의 이름입니다. 유효한 값은 ' R ', ' Python ' 및 ' Java '입니다. 추가 런타임은 나중에 추가 될 수 있습니다.|
|scope |int |public 범위에 대해 0입니다. 1 전용 범위 |  
|scope_desc |varchar (7) |패키지가 공용 인지 아니면 전용인 지를 나타냅니다.|

## <a name="see-also"></a>참고 항목  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [새 R 패키지 설치](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [새 Python 패키지 설치](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  
