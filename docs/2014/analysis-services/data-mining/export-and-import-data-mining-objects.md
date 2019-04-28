---
title: 데이터 마이닝 개체 내보내기 및 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- exporting mining models
- exporting mining structures
- mining structures [Analysis Services], creating
- mining structures [DMX], exporting
- mining models [Analysis Services], migration
ms.assetid: 10a83b13-2640-4ff5-80c8-a35e1d692908
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9621a7ed2f7e1dcc26a46a71d59e4febac974d38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722446"
---
# <a name="export-and-import-data-mining-objects"></a>데이터 마이닝 개체 내보내기 및 가져오기
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 솔루션 백업, 복원 및 마이그레이션 기능 이외에도 SQL Server 데이터 마이닝을 통해 DMX(Data Mining Extensions)를 사용하여 서로 다른 서버 간에 데이터 마이닝 구조 및 모델을 빠르게 전송할 수 있습니다.  
  
 데이터 마이닝 솔루션에 다차원 데이터베이스 대신 관계형 데이터가 사용된 경우, 데이터베이스 복원을 사용하거나 전체 솔루션을 배포하는 방법보다 `EXPORT` 및 `IMPORT`를 사용하여 모델을 전송하는 방법이 훨씬 손쉽고 빠릅니다.  
  
 이 섹션에서는 DMX 문을 사용하여 데이터 마이닝 구조 및 모델을 전송하는 방법을 간략하게 설명합니다. 자세한 구문 및 예제는 [EXPORT&#40;DMX&#41;](/sql/dmx/export-dmx) 및 [IMPORT&#40;DMX&#41;](/sql/dmx/import-dmx)를 참조하세요.  
  
> [!NOTE]  
>  Microsoft SQL Server Analysis Services 데이터베이스에서 개체를 내보내거나 가져오려면 데이터베이스 관리자 또는 서버 관리자 권한이 필요합니다.  
  
## <a name="exporting-data-mining-structures"></a>데이터 마이닝 구조 내보내기  
 EXPORT 문을 사용하여 마이닝 구조를 내보내면 모든 관련 모델이 자동으로 내보내집니다. 내보낼 개체를 제어하려면 각 개체의 이름을 지정해야 합니다.  
  
 마이닝 구조를 내보낼 때 기본 동작에 따라 마이닝 구조가 처리되어 결과가 캐시된 경우, 구조의 기반이 되는 데이터에 대한 요약이 정의에 포함됩니다. 이러한 요약을 제거하려면 `Process Clear Structure` 작업을 수행하여 마이닝 구조에 연결된 캐시를 지워야 합니다. 자세한 내용은 [Process a Mining Structure](process-a-mining-structure.md)를 참조하세요.  
  
### <a name="exporting-data-mining-models"></a>데이터 마이닝 모델 내보내기  
 `WITH DEPENDENCIES` 키워드를 사용하면 마이닝 모델 및 해당 구조와 함께 데이터 원본 및 데이터 원본 뷰 정의를 내보낼 수 있습니다.  
  
 해당 종속성을 내보내지 않고 마이닝 모델을 내보내면 EXPORT 문에서 마이닝 모델의 정의 및 해당 마이닝 구조를 내보내지만 데이터 원본의 정의는 내보내지 않습니다. 따라서 모델을 가져온 후 모델을 즉시 찾아볼 수 있지만 대상 서버에서 마이닝 모델을 다시 처리하거나 기본 데이터에 대해 쿼리를 실행하려면 대상 서버에 해당 데이터 원본을 만들어야 합니다.  
  
## <a name="importing-data-mining-structures-and-models"></a>데이터 마이닝 구조 및 모델 가져오기  
 데이터 마이닝 개체를 가져오면 IMPORT 문을 실행할 때 연결되어 있는 서버 및 데이터베이스로 개체를 가져오게 됩니다. 서버에 없는 데이터베이스가 가져오기 파일에 포함된 경우 해당 데이터베이스가 만들어집니다.  
  
 `Restore` 명령을 사용하여 마이닝 구조 또는 마이닝 모델을 가져올 수도 있습니다. 이러한 모델이나 구조를 내보낸 데이터베이스와 같은 이름의 데이터베이스에 해당 모델이나 구조가 복원됩니다. 자세한 내용은 [Restore Options](../multidimensional-models/restore-options.md)을(를) 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 서버에 이름이 같은 모델이나 구조가 이미 있으면 해당 서버로 모델이나 구조를 가져올 수 없습니다. 또한 데이터 마이닝 개체를 내보낸 다음 내보내기 파일에서 해당 개체의 이름을 수정할 수 없습니다. 따라서 이름이 충돌할 것으로 예상되는 경우 대상 서버에서 데이터 마이닝 개체를 삭제하거나 정의를 내보내기 전에 데이터 마이닝 개체의 이름을 바꿔야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 솔루션 및 개체 관리](management-of-data-mining-solutions-and-objects.md)  
  
  
