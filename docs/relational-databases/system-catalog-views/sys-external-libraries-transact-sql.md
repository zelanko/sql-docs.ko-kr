---
title: sys.external_libraries (거래-SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 11/04/2019
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b1bfc00b403fa76f692db78593ed4c0e6b53ce8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664427"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries(Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

R, Python 및 Java와 같은 외부 런타임과 관련된 패키지 라이브러리 관리를 지원합니다.

> [!NOTE]
> SQL Server 2017에서는 R 언어 및 Windows 플랫폼이 지원됩니다. Windows 및 Linux 플랫폼의 R, Python 및 Java는 SQL Server 2019 이상에서 지원됩니다.

## <a name="sysexternal_libraries"></a>sys.external_libraries

카탈로그 보기 sys.external_libraries 데이터베이스에 업로드된 각 외부 라이브러리에 대한 행을 나열합니다.

|열 이름 |데이터 형식 | 설명|
|------|------|------|
|external_library_id |int | 외부 라이브러리 개체의 ID입니다. |
|name |sysname |외부 라이브러리의 이름입니다. 소유자당 데이터베이스 내에서 고유합니다.|
|principal_id |int |이 외부 라이브러리를 소유하는 보안 주체의 ID입니다. |
|언어 | sysname | 외부 라이브러리를 지원하는 언어 또는 런타임의 이름입니다. 유효한 값은 'R', '파이썬', 'Java'입니다. 나중에 추가 런타임이 추가될 수 있습니다.|
|scope |int |공용 범위에 대한 0; 개인 범위에 대해 1 |  
|scope_desc |바르차르 (7) |패키지가 공개 또는 비공개인지 여부를 나타냅니다.|

## <a name="see-also"></a>참고 항목  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [SQL Server에 새로운 R 패키지 설치](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [SQL Server에 새로운 Python 패키지 설치](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  