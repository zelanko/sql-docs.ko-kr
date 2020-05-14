---
title: Server의 Database 요소(DTA)
description: dta 유틸리티에서 서버에 대한 Database 요소는 특정 서버에서 튜닝할 데이터베이스를 지정합니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: d416f6f57d70674a8f9a7b484f7da9c87b18342c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831598"
---
# <a name="database-element-for-server-dta"></a>Server의 Database 요소(DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

특정 서버에서 튜닝할 데이터베이스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|발생 빈도|**Server** 요소마다 한 번 이상 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|부모 요소|[Server 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|자식 요소|[Database의 Name 요소&#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Database의 Schema 요소&#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>설명  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **DatabaseDetailsTypecomplexType** 입니다. 이 **Database** 요소와 **Configuration** 요소가 루트 부모인 요소를 혼동하지 마십시오. 자세한 내용은 [Configuration의 Database 요소&#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 **Database** 요소의 사용 예제를 보려면 [Server 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
