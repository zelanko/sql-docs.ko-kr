---
title: external_libraries (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
ms.openlocfilehash: 78923a0eb1404c1437c6e1144888261e542ebc5a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471107"
---
# <a name="sysexternallibraries-transact-sql"></a>external_libraries (Transact-sql)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

는 R, Python 및 Java와 같은 외부 런타임과 관련 된 패키지 라이브러리의 관리를 지원 합니다.

> [!NOTE]
> SQL Server 2017에서는 R 언어 및 Windows 플랫폼이 지원됩니다. Windows 및 Linux 플랫폼의 R, Python 및 Java는 SQL Server 2019 CTP 2.4에서 지원됩니다.

## <a name="sysexternallibraries"></a>sys.external_libraries

카탈로그 뷰 external_libraries는 데이터베이스에 업로드 된 각 외부 라이브러리의 행을 나열 합니다.

|열 이름 |데이터 형식 | 설명|
|------|------|------|
|external_library_id |ssNoversion | 외부 라이브러리 개체의 ID입니다. |
|name |sysname |외부 라이브러리의 이름입니다. 는 소유자 당 데이터베이스 내에서 고유 합니다.|
|principal_id |ssNoversion |이 외부 라이브러리를 소유 하는 보안 주체의 ID입니다. |
|language | sysname | 외부 라이브러리를 지 원하는 언어나 런타임의 이름입니다. 유효한 값은 ' R ', ' Python ' 및 ' Java '입니다. 추가 런타임은 나중에 추가 될 수 있습니다.|
|범위 |ssNoversion |public 범위에 대해 0입니다. 1 전용 범위 |  
|scope_desc |varchar(7) |패키지가 공용 인지 아니면 전용인 지를 나타냅니다.|

## <a name="see-also"></a>참조  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [SQL Server에 새로운 R 패키지 설치](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [SQL Server에 새로운 Python 패키지 설치](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  