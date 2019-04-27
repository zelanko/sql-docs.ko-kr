---
title: sys.external_libraries (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
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
ms.openlocfilehash: d56d0c69b9e3bae87dda9b55d241a1c040210ca9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637472"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

R, Python 및 Java와 같은 외부 런타임 관련 패키지 라이브러리의 관리를 지원 합니다.

> [!NOTE]
> SQL Server 2017에서는 R 언어 및 Windows 플랫폼이 지원됩니다. Windows 및 Linux 플랫폼의 R, Python 및 Java는 SQL Server 2019 CTP 2.4에서 지원됩니다.

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