---
title: DbStorageLocation 요소 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cdee1fc2d62f63eb70e5aecd47c32693a9fbd155
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173923"
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|""|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[데이터베이스](database-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `DbStorageLocation` 데이터베이스 속성을 기존 UNC 폴더 경로나 빈 문자열로 설정 해야 합니다. 빈 문자열은 기본 서버 데이터 폴더입니다. 이 폴더가 없는 경우 `Create`, `Attach` 또는 `Alter` 명령을 실행하면 오류가 발생합니다.  
  
 또한는 `DbStorageLocation` 데이터베이스 속성이 서버 데이터 폴더나 해당 하위 폴더 중 하나를 가리키도록 설정할 수 없습니다. 위치가 서버 데이터 폴더나 그 하위 폴더 중 하나를 가리키는 경우 `Create`, `Attach` 또는 `Alter` 명령을 실행하면 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Analysis Services 데이터베이스 연결 및 분리](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
