---
title: 프로젝트 설정 (형식 매핑) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 148180d95bcbff1626069e72fb66dd9a3ca859c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667923"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>프로젝트 설정(형식 매핑)(SybaseToSQL)
형식 매핑 페이지의 **프로젝트 설정** 대화 상자에는 SSMA Sybase 적응형 Server Enterprise (ASE) 데이터 형식으로 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
형식 매핑 페이지의 수를 **프로젝트 설정** 하 고 **기본 프로젝트 설정** 대화 상자.  
  
-   모든 향후 SSMA 프로젝트에 대 한 형식 매핑 설정을 지정 하는 **도구** 메뉴에서 **기본 프로젝트 설정**는 설정이 필요를 볼 수 있는 마이그레이션 프로젝트 형식을 선택 또는 변경 **마이그레이션 대상 버전** 드롭다운 목록 및 선택한 **형식 매핑** 왼쪽 창의 맨 아래에 있습니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면 합니다 **도구** 메뉴에서 **프로젝트 설정**를 선택한 후 **형식 매핑** 왼쪽 창의 맨 아래에.  
  
## <a name="options"></a>변수  
**원본 형식**  
매핑된 ASE 데이터 형식입니다.  
  
**대상 유형**  
대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정된 ASE 데이터 형식에 대 한 데이터 형식입니다.  
  
Sybase 형식 매핑에 대 한 기본 SSMA는 다음 섹션의 표를 참조 합니다.  
  
**추가**  
데이터 형식 매핑 목록에 추가 하려면 클릭 합니다.  
  
**편집**  
매핑 목록에서 선택한 데이터 형식을 편집 하려면 클릭 합니다.  
  
**제거**  
매핑 목록에서 선택한 데이터 형식 매핑을 제거 하려면 클릭 합니다.  
  
**기본값으로 다시 설정**  
형식 매핑 목록 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="default-type-mapping"></a>기본 형식 매핑  
다음 표에서 ASE 간의 기본 형식 매핑 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
|ASE 데이터 형식|SQL Server 데이터 형식|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**이진 [\*... 8000]**|**binary[\*]**|  
|**binary[8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**다양 한 char [\*... 8000]**|**varchar[\*]**|  
|**char varying[8001..\*]**|**varchar(max)**|  
|**char[\*..8000]**|**char[\*]**|  
|**char[8001..\*;]**|**varchar(max)**|  
|**character**|**char**|  
|**다양 한 문자**|**varchar**|  
|**다양 한 문자 [\*... 8000]**|**varchar[\*]**|  
|**character varying[8001..\*]**|**varchar(max)**|  
|**character[\*..8000]**|**char[\*]**|  
|**character[8001..\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2[3]**|  
|**dec**|**decimal**|  
|**dec[\*..\*]**|**decimal[\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimal[\*..\*]**|**decimal[\*]**|  
|**decimal[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**double precision**|**float[53]**|  
|**float**|**float[53]**|  
|**float[\*..15]**|**float[24]**|  
|**float[16..\*]**|**float[53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar[255]**|  
|**money**|**money**|  
|**national char**|**nchar**|  
|**national char [\*... 4000]**|**nchar[\*]**|  
|**national char varying**|**nvarchar**|  
|**national char varying [\*... 4000]**|**nvarchar[\*]**|  
|**national char varying [4001...\*]**|**nvarchar(max)**|  
|**national char [4001...\*]**|**nvarchar(max)**|  
|**국가별 문자**|**nchar**|  
|**국가별 문자 [\*... 4000]**|**nchar[\*]**|  
|**국가별 문자 [4001...\*]**|**nvarchar(max)**|  
|**국가별 문자 변경**|**nvarchar**|  
|**다양 한 국가별 문자 [\*... 4000]**|**nvarchar[\*]**|  
|**다양 한 국가별 문자 [4001...\*]**|**nvarchar(max)**|  
|**national varchar**|**nvarchar**|  
|**national varchar [\*... 4000]**|**nvarchar[\*]**|  
|**national varchar [4001...\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar 변경**|**nvarchar**|  
|**nchar 다양 한 [\*... 4000]**|**nvarchar[\*]**|  
|**nchar varying[4001..\*]**|**nvarchar(max)**|  
|**nchar[\*..4000]**|**nchar[\*]**|  
|**nchar[4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numeric[\*..\*]**|**numeric[\*]**|  
|**numeric[\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar[\*..4000]**|**nvarchar[\*]**|  
|**nvarchar[4001..\*]**|**nvarchar(max)**|  
|**real**|**float[24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar[128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**time**|**time[3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**다양 한 unichar**|**nvarchar**|  
|**unichar 다양 한 [\*... 4000]**|**nvarchar[\*]**|  
|**unichar varying[4001..\*]**|**nvarchar(max)**|  
|**unichar[\*..4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar[\*..4000]**|**nvarchar[\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**unsigned bigint**|**numeric[20][0]**|  
|**unsigned int**|**bigint**|  
|**unsigned smallint**|**int**|  
|**unsigned tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary[\*..8000]**|**varbinary[\*]**|  
|**varbinary[8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar[\*..8000]**|**varchar[\*]**|  
|**varchar[8001..\*]**|**varchar(max)**|  
  
