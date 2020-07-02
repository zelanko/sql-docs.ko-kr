---
title: sys. external_library_files (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 69c1b1c0f1ec2c7ab1c6cd17fbf949f0aaf166f2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754481"
---
# <a name="sysexternal_library_files-transact-sql"></a>sys.external_library_files(Transact-SQL)  
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

외부 라이브러리를 구성 하는 각 파일에 대 한 행을 나열 합니다.

|열 이름 |데이터 형식 |Description|
|------|------|-----|
|external_library_id | int |외부 라이브러리 개체의 ID입니다. |
|콘텐츠 |varbinary(max) |외부 라이브러리 파일 아티팩트의 콘텐츠입니다. |
|platform |tinyint |SQL Server 설치 된 호스트 플랫폼의 ID입니다. |
|platform_desc | nvarchar(60) |호스트 플랫폼의 이름입니다. 유효한 값은 ' WINDOWS ', ' LINUX '입니다. |

### <a name="see-also"></a>참고 항목  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)  
