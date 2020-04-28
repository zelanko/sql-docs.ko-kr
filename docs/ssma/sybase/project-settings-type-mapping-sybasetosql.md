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
ms.openlocfilehash: d7b16bdf3717fa14f91af41663cbd65365eac52a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028665"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>프로젝트 설정(형식 매핑)(SybaseToSQL)
**프로젝트 설정** 대화 상자의 형식 매핑 페이지에는 Ssma에서 Sybase (Sybase Server Enterprise) 데이터 형식을 데이터 형식으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다.  
  
형식 매핑 페이지는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   모든 향후 SSMA 프로젝트에 대해 형식 매핑 설정을 지정 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 하 고 마이그레이션 **대상 버전** 드롭다운에서 설정 하거나 변경 해야 하는 설정에 대 한 마이그레이션 프로젝트 형식을 선택한 다음 왼쪽 창의 맨 아래에 있는 **형식 매핑** 을 선택 합니다.  
  
-   현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택한 다음 왼쪽 창의 맨 아래에 있는 **형식 매핑** 을 선택 합니다.  
  
## <a name="options"></a>옵션  
**원본 유형**  
매핑된 ASE 데이터 형식입니다.  
  
**대상 유형**  
지정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ASE 데이터 형식에 대 한 대상 데이터 형식입니다.  
  
Sybase 형식 매핑의 기본 SSMA에 대해서는 다음 섹션의 표를 참조 하세요.  
  
**추가**  
매핑 목록에 데이터 형식을 추가 하려면 클릭 합니다.  
  
**편집**  
매핑 목록에서 선택한 데이터 형식을 편집 하려면 클릭 합니다.  
  
**제거**  
선택한 데이터 형식 매핑을 매핑 목록에서 제거 하려면 클릭 합니다.  
  
**기본값으로 다시 설정**  
형식 매핑 목록을 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="default-type-mapping"></a>기본 형식 매핑  
다음 표에서는 ASE와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 간의 기본 형식 매핑을 포함 합니다.  
  
|ASE 데이터 형식|SQL Server 데이터 형식|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binary [\*.. 8000]**|**binary [\*]**|  
|**binary [8001\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**문자 변경 [\*.. 8000]**|**varchar [\*]**|  
|**문자 변경 [8001\*]**|**varchar(max)**|  
|**char [\*.. 8000]**|**char [\*]**|  
|**char [8001 ...\*]**|**varchar(max)**|  
|**자의**|**char**|  
|**character varying**|**varchar**|  
|**문자 변경 [\*.. 8000]**|**varchar [\*]**|  
|**문자 변경 [8001\*]**|**varchar(max)**|  
|**character [\*.. 8000]**|**char [\*]**|  
|**문자 [8001\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**dec**|**decimal**|  
|**dec [\*.. \*]**|**decimal [\*]**|  
|**dec [\*.. \*][\*.. \*]**|**decimal [\*] [\*]**|  
|**decimal**|**decimal**|  
|**decimal [\*.. \*]**|**decimal [\*]**|  
|**decimal [\*.. \*][\*.. \*]**|**decimal [\*] [\*]**|  
|**배정밀도**|**float [53]**|  
|**float**|**float [53]**|  
|**float [\*.. 15**|**float [24]**|  
|**float [16 ...\*]**|**float [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**이상**|**nvarchar [255]**|  
|**money**|**money**|  
|**국가별 문자**|**nchar**|  
|**국가별 문자 [\*.. 4000]**|**nchar [\*]**|  
|**국가별 문자 변경**|**nvarchar**|  
|**국가별 문자는 다양\*한 [.. 4000]**|**nvarchar [\*]**|  
|**국가별 문자 변경 [4001\*]**|**nvarchar(max)**|  
|**국가별 문자 [4001\*]**|**nvarchar(max)**|  
|**국가별 문자**|**nchar**|  
|**국가 문자 [\*.. 4000]**|**nchar [\*]**|  
|**국가 문자 [4001\*]**|**nvarchar(max)**|  
|**국가별 문자 변경**|**nvarchar**|  
|**국가별 문자는 다양\*한 [.. 4000]**|**nvarchar [\*]**|  
|**국가별 문자 변경 [4001\*]**|**nvarchar(max)**|  
|**국가별 varchar**|**nvarchar**|  
|**국가별 varchar [\*.. 4000]**|**nvarchar [\*]**|  
|**국가별 varchar [4001\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar 변경**|**nvarchar**|  
|**nchar 변경 [\*.. 4000]**|**nvarchar [\*]**|  
|**nchar 변경 [4001\*]**|**nvarchar(max)**|  
|**nchar [\*.. 4000]**|**nchar [\*]**|  
|**nchar [4001\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**숫자 [\*.. \*]**|**numeric [\*]**|  
|**숫자 [\*.. \*][\*.. \*]**|**숫자 [\*] [\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [\*.. 4000]**|**nvarchar [\*]**|  
|**nvarchar [4001\*]**|**nvarchar(max)**|  
|**real**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar [128]**|  
|**sysname [\*.. \*]**|**nvarchar [255]**|  
|**text**|**text**|  
|**time**|**시간 [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**unichar 다양**|**nvarchar**|  
|**unichar 다양 한\*[.. 4000]**|**nvarchar [\*]**|  
|**unichar 다양 한 [4001\*]**|**nvarchar(max)**|  
|**unichar [\*.. 4000]**|**nchar [\*]**|  
|**unichar [4001\*]**|**nvarchar(max)**|  
|**외부**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [\*.. 4000]**|**nvarchar [\*]**|  
|**univarchar [4001\*]**|**nvarchar(max)**|  
|**부호 없는 bigint**|**숫자 [20] [0]**|  
|**부호 없는 정수**|**bigint**|  
|**unsigned smallint**|**int**|  
|**unsigned tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [\*.. 8000]**|**varbinary [\*]**|  
|**varbinary [8001\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar [\*.. 8000]**|**varchar [\*]**|  
|**varchar [8001\*]**|**varchar(max)**|  
  
