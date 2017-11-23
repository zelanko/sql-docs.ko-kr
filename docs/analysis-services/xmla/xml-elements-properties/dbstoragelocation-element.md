---
title: "DbStorageLocation 요소 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cf7859b90400b1dc6962e16c4d2c4e43f5290b75
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dbstoragelocation-element"></a>DbStorageLocation 요소
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 가 모든 데이터베이스 데이터 및 메타데이터 파일을 만들고 관리할 폴더를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Database>  
...  
   <ddl100_100:DbStorageLocation>...</ddl100_100:DbStorageLocation>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|""|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[데이터베이스](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **DbStorageLocation** 데이터베이스 속성을 기존 UNC 폴더 경로나 빈 문자열로 설정해야 합니다. 빈 문자열은 기본 서버 데이터 폴더입니다. 이 폴더가 없는 경우 **Create**, **Attach**또는 **Alter** 명령을 실행하면 오류가 발생합니다.  
  
 또한 **DbStorageLocation** 데이터베이스 속성이 서버 데이터 폴더 또는 그 하위 폴더 중 하나를 가리키도록 설정할 수 없습니다. 위치가 서버 데이터 폴더나 그 하위 폴더 중 하나를 가리키는 경우 **Create**, **Attach**또는 **Alter** 명령을 실행하면 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Analysis Services 데이터베이스 연결 및 분리](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
