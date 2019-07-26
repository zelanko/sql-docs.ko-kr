---
title: external_library_files (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: d7af0a7fcb639ae3beab6216e77f9b7b95a398da
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471091"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>external_library_files (Transact-sql)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

외부 라이브러리를 구성 하는 각 파일에 대 한 행을 나열 합니다.

|열 이름 |데이터 형식 |설명|
|------|------|-----|
|external_library_id | ssNoversion |외부 라이브러리 개체의 ID입니다. |
|content |varbinary(max) |외부 라이브러리 파일 아티팩트의 콘텐츠입니다. |
|platform.string |TINYINT |SQL Server 설치 된 호스트 플랫폼의 ID입니다. |
|platform_desc | nvarchar(60) |호스트 플랫폼의 이름입니다. 유효한 값은 ' WINDOWS ', ' LINUX '입니다. |

### <a name="see-also"></a>참조  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server Machine Learning 서비스에 대 한 패키지 관리](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
