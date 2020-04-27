---
title: sys. external_language_files (Transact-sql)-SQL Server | Microsoft Docs
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
ms.openlocfilehash: 0d1325311ef0b708f5a3abd5f4494e099863efc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65995091"
---
# <a name="sysexternal_language_files-transact-sql"></a>sys. external_language_files (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 카탈로그 뷰는 데이터베이스에 있는 외부 언어 확장 파일의 목록을 제공 합니다. **R** 및 **Python**은 예약된 이름이며 해당 특정 이름을 사용하여 외부 언어를 만들 수 없습니다.

File_spec에서 외부 언어가 생성 되 면 확장 자체와 해당 속성이이 뷰에 나열 됩니다. 이 보기에는 OS 당 언어 당 하나의 항목이 포함 됩니다.

## <a name="sysexternal_languages"></a>sys.external_languages

카탈로그 뷰 sys. external_language_files는 데이터베이스의 각 외부 언어 확장에 대 한 행을 나열 합니다. 매개 변수

|열 이름 |데이터 형식 | 설명|
|------|------|------|
|external_language_id |int | 외부 언어의 ID입니다.|
|콘텐츠|varbinary(max) |외부 언어 확장 파일의 콘텐츠|
|file_name|nvarchar (266)|언어 확장 파일의 이름입니다.|
|platform|tinyint|SQL Server 설치 된 호스트 플랫폼의 ID|
|platform_desc |nvarchar(60)|호스트 플랫폼의 이름입니다. 유효한 값은 ' WINDOWS ', ' LINUX '입니다.|
|매개 변수|nvarchar(4000)|외부 언어 prameters|
|environment_variables |nvarchar(4000)|외부 언어 환경 변수|

## <a name="see-also"></a>참조  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [외부 언어 만들기](../../t-sql/statements/create-external-language-transact-sql.md)  
