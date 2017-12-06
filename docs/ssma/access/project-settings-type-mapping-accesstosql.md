---
title: "프로젝트 설정 (형식 매핑) (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
caps.latest.revision: "16"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d82b431499de3986f0358074ad96e4acc69fb41
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-type-mapping-accesstosql"></a>프로젝트 설정 (형식 매핑) (AccessToSQL)
프로젝트 유형 매핑 설정 SSMA 프로젝트에 대 한 기본 형식 매핑을 설정할 수 있습니다. 또한 개별 데이터베이스 개체에 대 한 형식 매핑을 지정할 수 있습니다. 자세한 내용은 참조 [매핑 소스 및 대상 데이터 형식](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)합니다.  
  
형식 매핑은에서 사용할 수는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자:  
  
-   사용 하 여는 **프로젝트 설정** 현재 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 형식 매핑 설정에 액세스 하려면는 **도구** 메뉴 선택 **프로젝트 설정**, 클릭 하 고 **형식 매핑** 왼쪽된 창에서.  
  
-   사용 하 여 **기본 프로젝트 설정** 모든 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 형식 매핑 설정에 액세스 하려면는 **도구** 메뉴 선택 **기본 프로젝트 설정**, 설정을 볼 /에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭다운 하 고 클릭 **형식 매핑** 왼쪽된 창에서.  
  
## <a name="options"></a>옵션  
**원본 형식**  
매핑할 Access 데이터 형식입니다.  
  
**대상 유형**  
대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 지정 된 Access 데이터 형식에 대 한 SQL Azure 데이터 형식입니다.  
  
다음 표에서 원본 및 대상 데이터 형식 간의 기본 매핑을 보여 줍니다.  
  
|Access 데이터 형식|SQL Server 데이터 형식|  
|--------------------|------------------------|  
|**이진 [\*... \*]**|**varbinary [\*]**|  
|**boolean**|**bit**|  
|**바이트**|**tinyint**|  
|**통화**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**긴**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**메모**|**nvarchar(max)**|  
|**메모** Access 97-|**varchar(max)**|  
|**단일**|**real**|  
|**text[\*.. \*]**|**nvarchar [\*]**|  
|**text[\*.. \*]** Access 97-|**varchar [\*]**|  
  
**추가**  
데이터 형식 매핑 목록에 추가 하려면 클릭 합니다.  
  
**편집**  
데이터 형식 매핑 목록에서 편집 하려면 클릭 합니다.  
  
**제거**  
매핑 목록에서 선택한 데이터 형식 매핑을 제거 하려면 클릭 합니다.  
  
**기본값으로 다시 설정**  
모든 데이터 형식 매핑을 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[원본 및 대상 데이터 형식 매핑](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[사용자 인터페이스 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
