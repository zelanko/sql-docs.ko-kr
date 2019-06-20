---
title: sys.external_languages (TRANSACT-SQL)-SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_languages
- external_languages_TSQL
- sys.external_languages
- sys.external_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_languages catalog view
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1cef52f066a07032240d17f88297b02ba3f7e5fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65995121"
---
# <a name="sysexternallanguages-transact-sql"></a>sys.external_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 카탈로그 뷰에 데이터베이스에서 외부 언어의 목록을 제공합니다. **R** 및 **Python**은 예약된 이름이며 해당 특정 이름을 사용하여 외부 언어를 만들 수 없습니다.

## <a name="sysexternallanguages"></a>sys.external_languages

카탈로그 뷰 sys.external_languages 데이터베이스에서 외부 각 언어에 대 한 행을 나열합니다.

|열 이름 |데이터 형식 | Description|
|------|------|------|
|external_language_id |ssNoversion | 외부 언어의 ID|
|language |sysname |외부 언어의 이름입니다. 데이터베이스 내에서 고유합니다. R 및 Python은 각 인스턴스에 대해 예약 된 이름|
|create_date |Datetime2 |생성의 날짜 및 시간|
|principal_id |ssNoversion |이 외부 라이브러리를 소유한 보안 주체의 ID|

## <a name="see-also"></a>참고자료  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [외부 언어 만들기](../../t-sql/statements/create-external-language-transact-sql.md) 
