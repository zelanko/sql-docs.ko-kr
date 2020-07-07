---
title: sys.sys언어 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syslanguages
- sys.syslanguages_TSQL
- syslanguages
- syslanguages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syslanguages system table
- sys.syslanguages compatibility view
ms.assetid: f216d1cd-997c-42f0-a737-abbdfcd88383
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 62491475c51fcfc879415bb53f3d5cb08447a427
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012201"
---
# <a name="syssyslanguages-transact-sql"></a>sys.syslanguages(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 언어마다 하나의 행이 포함되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|langid|**smallint**|고유한 언어 ID입니다.|  
|dateformat|**nchar(3)**|날짜 순서입니다(예: DMY).|  
|datefirst|**tinyint**|첫 번째 요일: 월요일의 경우 1, 화요일의 경우 2, 일요일은 7까지입니다.|  
|업그레이드|**int**|시스템에서 사용하도록 예약되었습니다.|  
|name|**sysname**|공식 언어 이름 (예: Français)입니다.|  
|alias|**sysname**|대체 언어 이름입니다(예: 프랑스어).|  
|months|**nvarchar(372)**|1월에서 12월까지의 순서로 쉼표로 구분된 전체 길이의 월 이름 목록이며 각 이름은 20자까지 사용할 수 있습니다.|  
|shortmonths|**nvarchar(132)**|1월에서 12월까지의 순서로 쉼표로 구분된 짧은 길이의 월 이름 목록이며 각 이름은 9자까지 사용할 수 있습니다.|  
|일|**nvarchar(217)**|월요일에서 일요일까지의 순서로 쉼표로 구분된 요일 이름의 목록이며 각 이름은 30자까지 사용할 수 있습니다.|  
|lcid|**int**|해당 언어용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 로캘 ID입니다.|  
|msglangid|**smallint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 메시지 그룹 ID입니다.|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 설치된 언어는 다음과 같습니다.  
  
|영어 이름|Windows LCID|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 메시지 그룹 ID|  
|---------------------|------------------|-----------------------------------------|  
|영어|1033|1033|  
|독일어|1031|1031|  
|프랑스어|1036|1036|  
|일본어|1041|1041|  
|덴마크어|1030|1030|  
|스페인어|3082|3082|  
|이탈리아어|1040|1040|  
|네덜란드어|1043|1043|  
|노르웨이어|2068|2068|  
|포르투갈어|2070|2070|  
|핀란드어|1035|1035|  
|스웨덴어|1053|1053|  
|체코어|1029|1029|  
|헝가리어|1038|1038|  
|폴란드어|1045|1045|  
|루마니아어|1048|1048|  
|크로아티아어|1050|1050|  
|슬로바키아어|1051|1051|  
|슬로베니아어|1060|1060|  
|그리스어|1032|1032|  
|불가리아어|1026|1026|  
|러시아어|1049|1049|  
|터키어|1055|1055|  
|영어(영국)|2057|1033|  
|에스토니아어|1061|1061|  
|라트비아어|1062|1062|  
|리투아니아어|1063|1063|  
|포르투갈어(브라질)|1046|1046|  
|중국어(번체)|1028|1028|  
|한국어|1042|1042|  
|중국어(간체)|2052|2052|  
|아랍어|1025|1025|  
|태국어|1054|1054|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;호환성 뷰](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
