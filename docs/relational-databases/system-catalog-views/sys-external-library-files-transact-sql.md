---
title: sys.external_library_files (거래-SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/24/2019
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2f1bbdc3936dc6295b9ecc51b937e50cae20670
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664236"
---
# <a name="sysexternal_library_files-transact-sql"></a>sys.external_library_files(Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

외부 라이브러리를 구성하는 각 파일에 대한 행을 나열합니다.

|열 이름 |데이터 형식 |설명|
|------|------|-----|
|external_library_id | int |외부 라이브러리 개체의 ID입니다. |
|content |varbinary(max) |외부 라이브러리 파일 아티팩트의 콘텐츠입니다. |
|platform |tinyint |SQL Server가 설치된 호스트 플랫폼의 ID입니다. |
|platform_desc | nvarchar(60) |호스트 플랫폼의 이름입니다. 유효한 값은 '윈도우', '리눅스'입니다. |

### <a name="see-also"></a>참고 항목  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)  

