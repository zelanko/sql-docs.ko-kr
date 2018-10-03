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
manager: craigg
ms.openlocfilehash: 052681d249d3c93e54c23ebcf2b42cadf5724f2a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855111"
---
# <a name="project-settings-type-mapping-accesstosql"></a>프로젝트 설정 (형식 매핑) (AccessToSQL)
형식 매핑 프로젝트 설정 SSMA 프로젝트에 대 한 기본 형식 매핑을 설정할 수 있습니다. 또한 개별 데이터베이스 개체에 대 한 형식 매핑을 지정할 수 있습니다. 자세한 내용은 [매핑 원본 및 대상 데이터 형식](mapping-source-and-target-data-types-accesstosql.md)합니다.  
  
형식 매핑에서 사용할 수는 **프로젝트 설정** 하 고 **기본 프로젝트 설정** 대화 상자:  
  
-   사용 된 **프로젝트 설정** 현재 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 형식 매핑을 설정에 액세스할 수는 **도구** 메뉴에서 **프로젝트 설정**를 클릭 하 고 **형식 매핑** 왼쪽된 창에서.  
  
-   사용 된 **기본 프로젝트 설정** 모든 프로젝트에 대 한 구성 옵션을 설정 하려면 대화 상자. 형식 매핑을 설정에 액세스 하는 **도구** 메뉴에서 **기본 프로젝트 설정**, 설정을 볼 /에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택  **마이그레이션 대상 버전** 드롭다운을 클릭 한 다음 **형식 매핑** 왼쪽된 창에서.  
  
## <a name="options"></a>변수  
**원본 형식**  
매핑할 Access 데이터 형식입니다.  
  
**대상 유형**  
대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 지정 된 Access 데이터 형식에 대 한 SQL Azure 데이터 형식입니다.  
  
다음 표에서 원본 및 대상 데이터 형식 간의 기본 매핑을 보여 줍니다.  
  
|Access 데이터 형식|SQL Server 데이터 형식|  
|--------------------|------------------------|  
|**이진 [\*... \*]**|**varbinary[\*]**|  
|**boolean**|**bit**|  
|**byte**|**tinyint**|  
|**currency**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**Long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**memo**|**nvarchar(max)**|  
|**메모** -Access 97|**varchar(max)**|  
|**single**|**real**|  
|**text[\*..\*]**|**nvarchar[\*]**|  
|**텍스트 [\*... \*]** -Access 97|**varchar[\*]**|  
  
**추가**  
데이터 형식 매핑 목록에 추가 하려면 클릭 합니다.  
  
**편집**  
매핑 목록에 있는 데이터 형식을 편집 하려면 클릭 합니다.  
  
**제거**  
매핑 목록에서 선택한 데이터 형식 매핑을 제거 하려면 클릭 합니다.  
  
**기본값으로 다시 설정**  
모든 데이터 형식 매핑을 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="see-also"></a>관련 항목  
[원본 및 대상 데이터 형식 매핑](mapping-source-and-target-data-types-accesstosql.md)  
[사용자 인터페이스 Reference(Access)](http://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
