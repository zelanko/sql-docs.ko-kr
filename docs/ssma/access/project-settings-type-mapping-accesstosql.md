---
title: 프로젝트 설정 (형식 매핑) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 01154cf477435e9dc5335606d0c11a05aecc492b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68066665"
---
# <a name="project-settings-type-mapping-accesstosql"></a>프로젝트 설정 (형식 매핑) (AccessToSQL)
형식 매핑 프로젝트 설정을 사용 하 여 SSMA 프로젝트에 대 한 기본 형식 매핑을 설정할 수 있습니다. 또한 개별 데이터베이스 개체에 대 한 형식 매핑을 지정할 수 있습니다. 자세한 내용은 [원본 및 대상 데이터 형식 매핑](mapping-source-and-target-data-types-accesstosql.md)을 참조 하세요.  
  
형식 매핑은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   **프로젝트 설정** 대화 상자를 사용 하 여 현재 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. 형식 매핑 설정에 액세스 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택한 다음 왼쪽 창에서 **형식 매핑** 을 클릭 합니다.  
  
-   **기본 프로젝트 설정** 대화 상자를 사용 하 여 모든 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. 형식 매핑 설정에 액세스 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 하 고 마이그레이션 **대상 버전** 드롭다운 메뉴에서 설정을 확인 해야 하는 마이그레이션 프로젝트 형식을 선택한 다음 왼쪽 창에서 **형식 매핑** 을 클릭 합니다.  
  
## <a name="options"></a>옵션  
**원본 유형**  
매핑할 액세스 데이터 형식입니다.  
  
**대상 유형**  
지정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 데이터 형식에 대 한 대상 또는 SQL Azure 데이터 형식입니다.  
  
다음 표에서는 원본 및 대상 데이터 형식 간의 기본 매핑을 보여 줍니다.  
  
|Access 데이터 형식|SQL Server 데이터 형식|  
|--------------------|------------------------|  
|**binary [\*.. \*]**|**varbinary [\*]**|  
|**boolean**|**bit**|  
|**byte**|**tinyint**|  
|**최신**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**eid**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**메모(memo)**|**nvarchar(max)**|  
|**memo** -Access 97|**varchar(max)**|  
|**single**|**real**|  
|**텍스트 [\*.. \*]**|**nvarchar [\*]**|  
|**텍스트 [\*.. ] \*** -액세스 97|**varchar [\*]**|  
  
**추가**  
매핑 목록에 데이터 형식을 추가 하려면 클릭 합니다.  
  
**편집**  
매핑 목록에서 데이터 형식을 편집 하려면 클릭 합니다.  
  
**제거**  
선택한 데이터 형식 매핑을 매핑 목록에서 제거 하려면 클릭 합니다.  
  
**기본값으로 다시 설정**  
모든 데이터 형식 매핑을 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="see-also"></a>참고 항목  
[원본 및 대상 데이터 형식 매핑](mapping-source-and-target-data-types-accesstosql.md)  
[사용자 인터페이스 참조 (액세스)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
