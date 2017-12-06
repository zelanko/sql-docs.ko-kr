---
title: "프로젝트 설정 (형식 매핑) (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea1b35e6943e89236aee72e7b0c31c545e100f88
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-type-mapping-sybasetosql"></a>프로젝트 설정 (형식 매핑) (SybaseToSQL)
형식 매핑 페이지는 **프로젝트 설정** 대화 상자 SSMA Sybase 적응형 Server Enterprise (ASE) 데이터 형식으로 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
형식 매핑 페이지는에서 사용할 수는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자.  
  
-   에 모든 향후 SSMA 프로젝트에 대 한 형식 매핑을 설정을 지정 하려면는 **도구** 메뉴 선택 **기본 프로젝트 설정**, 설정을 보거나에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭 다운 한 후 선택 **형식 매핑** 왼쪽 창의 맨 아래에 있습니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 선택 **프로젝트 설정**, 선택한 후 **유형 매핑** 왼쪽 창의 맨 아래에 있습니다.  
  
## <a name="options"></a>옵션  
**원본 형식**  
매핑된 ASE 데이터 형식입니다.  
  
**대상 유형**  
대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 지정된 ASE 데이터 형식에 대 한 데이터 형식입니다.  
  
Sybase 형식 매핑에 대 한 기본 SSMA는 다음 섹션의 표를 참조 하십시오.  
  
**추가**  
데이터 형식 매핑 목록에 추가 하려면 클릭 합니다.  
  
**편집**  
선택한 데이터 형식 매핑 목록에서 편집 하려면 클릭 합니다.  
  
**제거**  
매핑 목록에서 선택한 데이터 형식 매핑을 제거 하려면 클릭 합니다.  
  
**기본값으로 다시 설정**  
형식 매핑 목록 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="default-type-mapping"></a>기본 형식 매핑  
다음 표에서 기본 형식 매핑이 ASE 사이 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
|ASE 데이터 형식|SQL Server 데이터 형식|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**이진 [\*... 8000]**|**이진 [\*]**|  
|**이진 [8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**다양 한 문자**|**varchar**|  
|**다양 한 char [\*... 8000]**|**varchar [\*]**|  
|**다양 한 char [8001..\*]**|**varchar(max)**|  
|**char[\*.. 8000]**|**char[\*]**|  
|**char [8001..\*;]**|**varchar(max)**|  
|**문자**|**char**|  
|**다양 한 문자**|**varchar**|  
|**다양 한 문자 [\*... 8000]**|**varchar [\*]**|  
|**다양 한 문자 [8001..\*]**|**varchar(max)**|  
|**문자 [\*... 8000]**|**char[\*]**|  
|**문자 [8001..\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**년 12 월**|**decimal**|  
|**dec[\*.. \*]**|**10 진수 [\*]**|  
|**dec[\*.. \*][\*.. \*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**10 진수 [\*... \*]**|**10 진수 [\*]**|  
|**10 진수 [\*... \*][\*.. \*]**|**decimal[\*][\*]**|  
|**배정밀도**|**float [53]**|  
|**float**|**float [53]**|  
|**float [\*... 15]**|**float [24]**|  
|**float [16..\*]**|**float [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar [255]**|  
|**money**|**money**|  
|**국가별 문자**|**nchar**|  
|**national char [\*... 4000]**|**nchar [\*]**|  
|**다양 한 국가별 문자**|**nvarchar**|  
|**다양 한 national char [\*... 4000]**|**nvarchar [\*]**|  
|**다양 한 national char [4001..\*]**|**nvarchar(max)**|  
|**national char [4001..\*]**|**nvarchar(max)**|  
|**국가별 문자**|**nchar**|  
|**국가별 문자 [\*... 4000]**|**nchar [\*]**|  
|**국가별 문자 [4001..\*]**|**nvarchar(max)**|  
|**다양 한 국가별 문자**|**nvarchar**|  
|**다양 한 국가별 문자 [\*... 4000]**|**nvarchar [\*]**|  
|**다양 한 국가별 문자 [4001..\*]**|**nvarchar(max)**|  
|**national varchar**|**nvarchar**|  
|**national varchar [\*... 4000]**|**nvarchar [\*]**|  
|**national varchar [4001..\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar 다양 한**|**nvarchar**|  
|**nchar 다양 한 [\*... 4000]**|**nvarchar [\*]**|  
|**nchar 다양 한 [4001..\*]**|**nvarchar(max)**|  
|**nchar [\*... 4000]**|**nchar [\*]**|  
|**nchar [4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**숫자 [\*... \*]**|**숫자 [\*]**|  
|**숫자 [\*... \*][\*.. \*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [\*... 4000]**|**nvarchar [\*]**|  
|**nvarchar [4001..\*]**|**nvarchar(max)**|  
|**real**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar [128]**|  
|**sysname [\*... \*]**|**nvarchar [255]**|  
|**text**|**text**|  
|**time**|**시간 [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**다양 한 unichar**|**nvarchar**|  
|**다양 한 unichar [\*... 4000]**|**nvarchar [\*]**|  
|**다양 한 unichar [4001..\*]**|**nvarchar(max)**|  
|**unichar [\*... 4000]**|**nchar [\*]**|  
|**unichar [4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [\*... 4000]**|**nvarchar [\*]**|  
|**univarchar [4001..\*]**|**nvarchar(max)**|  
|**부호 없는 bigint**|**숫자 [20] [0]**|  
|**부호 없는 int**|**bigint**|  
|**부호 없는 smallint**|**int**|  
|**부호 없는 tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [\*... 8000]**|**varbinary [\*]**|  
|**varbinary [8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar [\*... 8000]**|**varchar [\*]**|  
|**varchar [8001..\*]**|**varchar(max)**|  
  
