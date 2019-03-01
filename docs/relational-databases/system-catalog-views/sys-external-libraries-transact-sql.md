---
title: sys.external_libraries (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3a2f83d703566ae5a60fd027ff7f186205a0c404
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017539"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

R, Python 및 Java와 같은 외부 런타임 관련 패키지 라이브러리의 관리를 지원 합니다.

> [!NOTE]
> SQL Server 2017에서는 R 언어 및 Windows 플랫폼 지원 됩니다. SQL Server 2019 CTP 2.3에서 R, Python 및 Java Windows 플랫폼에서 지원 됩니다. Linux에 대 한 지원은 이후 릴리스에 예정 되어 있습니다.

## <a name="sysexternallibraries"></a>sys.external_libraries

카탈로그 뷰 sys.external_libraries 데이터베이스에 업로드 된 각 외부 라이브러리에 대 한 행을 나열 합니다.

|열 이름 |데이터 형식 | Description|
|------|------|------|
|external_library_id |ssNoversion | 외부 라이브러리 개체의 ID입니다. |
|NAME |sysname |외부 라이브러리의 이름입니다. 소유자 당 데이터베이스 내에서 고유 합니다.|
|principal_id |ssNoversion |이 외부 라이브러리를 소유한 보안 주체의 ID입니다. |
|language | sysname | 외부 라이브러리를 지 원하는 런타임 언어의 이름입니다. 유효한 값은 'R', 'Python' 및 'Java'입니다. 추가 런타임 나중에 추가할 수 있습니다.|
|범위 |ssNoversion |공용 범위 0 전용 범위 1 |  
|scope_desc |varchar(7) |패키지를 공용 또는 개인 인지를 나타냅니다.|

## <a name="see-also"></a>참고자료  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [SQL Server에 새로운 R 패키지 설치](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [SQL Server에 새로운 Python 패키지 설치](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  