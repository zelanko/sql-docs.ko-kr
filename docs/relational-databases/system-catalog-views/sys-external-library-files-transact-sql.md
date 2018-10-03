---
title: sys.external_library_files (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_library_files catalog view
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9666b58132feb79876c4e8074dc530440c05b2c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828061"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

외부 라이브러리를 구성 하는 각 파일에 대 한 행을 나열 합니다.

|열 이름 |데이터 형식 |Description|
|------|------|-----|
|external_library_id | ssNoversion |외부 라이브러리 개체의 ID입니다. |
|content |varbinary(max) |외부 라이브러리 파일 아티팩트의 콘텐츠입니다. |
|플랫폼 |TINYINT |SQL Server가 설치 된 호스트 플랫폼의 ID입니다. |
|platform_desc | nvarchar(60) |호스트 플랫폼의 이름입니다. 유효한 값은 'WINDOWS', 'LINUX'. |

### <a name="see-also"></a>참고자료  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server Machine Learning 서비스에 대 한 패키지 관리](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
