---
title: sys.external_library_files (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.external_library_files catalog view
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: a3196218bbb886544a77c2fd1184c806591b16e6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

외부 라이브러리를 구성 하는 각 파일에 대 한 행을 나열 합니다.

|열 이름 |데이터 형식 |Description|
|------|------|-----|
|external_library_id | int |외부 라이브러리 개체의 ID입니다. |
|content |varbinary(max) |외부 라이브러리 파일 아티팩트의 내용입니다. |
|플랫폼 |tinyint |SQL Server를 설치 하 고 호스트 플랫폼의 ID입니다. |
|platform_desc | nvarchar(60) |호스트 플랫폼의 이름입니다. 유효한 값은 'WINDOWS', 'LINUX'. |

### <a name="see-also"></a>참고 항목  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server 컴퓨터 학습 서비스에 대 한 패키지 관리](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
