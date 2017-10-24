---
title: "데이터베이스 저장소 위치 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], storage location
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fb6c9aa4728cf355d0c974501fc36fd71a233a83
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="database-storage-location"></a>데이터베이스 저장소 위치
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA(데이터베이스 관리자)가 특정 데이터베이스를 서버 데이터 폴더 외부에 두어야 하는 경우가 종종 있습니다. 대개 성능 향상이나 저장소 확장과 같은 비즈니스 요구 사항에 따라 특정 데이터베이스를 서버 데이터 폴더 외부에 둡니다. 이러한 경우 **DBA는** DbStorageLocation [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 속성을 사용하여 데이터베이스 위치를 로컬 디스크나 네트워크 장치에 지정할 수 있습니다.  
  
## <a name="dbstoragelocation-database-property"></a>DbStorageLocation 데이터베이스 속성  
 **DbStorageLocation** 데이터베이스 속성은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 모든 데이터베이스 데이터 및 메타데이터 파일을 만들고 관리할 폴더를 지정합니다. 모든 메타데이터 파일은 **DbStorageLocation** 폴더에 저장되지만 데이터베이스 메타데이터 파일은 예외적으로 서버 데이터 폴더에 저장됩니다. **DbStorageLocation** 데이터베이스 속성 값을 설정할 때 고려해야 할 두 가지 사항을 반드시 고려해야 합니다.  
  
-   **DbStorageLocation** 데이터베이스 속성을 기존 UNC 폴더 경로나 빈 문자열로 설정해야 합니다. 서버 데이터 폴더에 대한 기본값은 빈 문자열입니다. 이 폴더가 없는 경우 **Create**, **Attach**또는 **Alter** 명령을 실행하면 오류가 발생합니다.  
  
-   서버 데이터 폴더나 해당 하위 폴더 중 하나를 가리키도록 **DbStorageLocation** 데이터베이스 속성을 설정할 수 없습니다. 위치가 서버 데이터 폴더나 해당 하위 폴더 중 하나를 가리키는 경우 **Create**, **Attach**또는 **Alter** 명령을 실행하면 오류가 발생합니다.  
  
> [!IMPORTANT]  
>  SAN(저장 영역 네트워크), iSCSI 기반 네트워크 또는 로컬로 연결된 디스크를 사용하도록 UNC 경로를 설정하는 것이 좋습니다. 네트워크 공유나 대기 시간이 긴 원격 저장소 솔루션에 대한 UNC 경로를 사용하면 설치가 지원되지 않습니다.  
  
### <a name="dbstoragelocation-compared-to-storagelocation"></a>DbStorageLocation과 StorageLocation 비교  
 **DbStorageLocation** 은 모든 데이터베이스 데이터 및 메타데이터 파일이 위치할 폴더를 지정하는 반면 **StorageLocation** 은 하나 이상의 큐브 파티션이 위치할 폴더를 지정합니다. **StorageLocation** 은 **DbStorageLocation**과 별개로 설정할 수 있습니다. 이는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA가 예상 결과에 따라 결정하며 두 속성을 함께 사용하는 경우가 많습니다.  
  
## <a name="dbstoragelocation-usage"></a>DbStorageLocation 사용  
 **DbStorageLocation** 데이터베이스 속성은 **Detach** Attach **데이터베이스 명령 시퀀스,**/**Backup** Restore **데이터베이스 명령 시퀀스 또는**/**Synchronize** 데이터베이스 명령에 **Create** 명령의 일부로 사용됩니다. **DbStorageLocation** 데이터베이스 속성을 변경하면 데이터베이스 개체의 구조가 변경됩니다. 따라서 모든 메타데이터를 다시 만들고 데이터를 다시 처리해야 합니다.  
  
> [!IMPORTANT]  
>  **Alter** 명령을 사용하여 데이터베이스 저장소 위치를 변경해서는 안 됩니다. 대신 **Detach**/**Attach** 데이터베이스 명령 시퀀스를 사용하는 것이 좋습니다( [Analysis Services 데이터베이스 이동](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md), [Analysis Services 데이터베이스 연결 및 분리](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)참조).  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Analysis Services 데이터베이스 연결 및 분리](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Analysis Services 데이터베이스 이동](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [DbStorageLocation 요소](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)   
 [요소 &#40; 만들기 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)   
 [Attach 요소](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [요소 &#40; 동기화 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)  
  
  

