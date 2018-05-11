---
title: 데이터 원본 뷰 및 데이터 원본에 대 한 변경 내용을 관리 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d1e010dece24c45a863b0c9aaf0770b1580fba4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>데이터 원본 뷰 및 데이터 원본에 대한 변경 내용 관리
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  스키마 생성 마법사는 다시 실행될 때 원래 생성에 사용한 것과 동일한 데이터 원본 및 데이터 원본 뷰를 다시 사용합니다. 사용자가 추가하는 데이터 원본이나 데이터 원본 뷰는 사용되지 않습니다. 처음 생성 후 원래 데이터 원본이나 데이터 원본 뷰를 삭제하는 경우에는 마법사를 처음부터 실행해야 합니다. 마법사의 이전 설정도 모두 삭제됩니다. 삭제된 데이터 원본이나 데이터 원본 뷰에 바인딩된 기본 데이터베이스의 기존 개체는 다음에 스키마 생성 마법사를 실행할 때 사용자가 만든 개체로 처리됩니다.  
  
 생성 시 데이터 원본 뷰에 기본 데이터베이스의 실제 상태가 반영되지 않으면 스키마 생성 마법사가 주제 영역 데이터베이스에 대한 스키마를 생성할 때 오류가 발생할 수 있습니다. 예를 들어 데이터 원본 뷰에서 열 데이터 형식을 **int**로 지정하지만 열 데이터 형식이 실제로 **string**인 경우 스키마 생성 마법사는 데이터 원본 뷰에 일치하도록 외래 키 데이터 형식을 **INT** 로 설정하면 실제 형식이 **string**이기 때문에 관계를 만들 때 실패합니다.  
  
 반면, 데이터 원본 연결 문자열을 이전 생성에서 다른 데이터베이스로 변경하는 경우에는 오류가 발생하지 않습니다. 새 데이터베이스가 사용되고 이전 데이터베이스는 변경되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [증분 생성 이해](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)  
  
  
