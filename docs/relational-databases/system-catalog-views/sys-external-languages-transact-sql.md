---
title: sys. external_languages (Transact-sql)-SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
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
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 053a7cdcf21775525b0eb8d46bbbfdf03098e03c
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627279"
---
# <a name="sysexternal_languages-transact-sql"></a>sys. external_languages (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 카탈로그 뷰는 데이터베이스의 외부 언어 목록을 제공 합니다. **R** 및 **Python**은 예약된 이름이며 해당 특정 이름을 사용하여 외부 언어를 만들 수 없습니다.

## <a name="sysexternal_languages"></a>sys.external_languages

카탈로그 뷰 sys. external_languages는 데이터베이스의 각 외부 언어에 대 한 행을 나열 합니다.

|열 이름 |데이터 형식 | Description|
|------|------|------|
|external_language_id |int | 외부 언어의 ID입니다.|
|language |sysname |외부 언어의 이름입니다. 데이터베이스 내에서 고유합니다. R 및 Python은 인스턴스당 예약 된 이름입니다.|
|create_date |datetime2 |만든 날짜 및 시간|
|principal_id |int |이 외부 라이브러리를 소유 하는 보안 주체의 ID입니다.|

## <a name="see-also"></a>참조  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [외부 언어 만들기](../../t-sql/statements/create-external-language-transact-sql.md) 
