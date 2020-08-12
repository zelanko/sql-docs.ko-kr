---
title: 데이터 차이 보기
description: 두 데이터베이스를 비교한 다음 데이터베이스 개체가 어떻게 다른지 확인하는 방법을 알아봅니다. 개체 내의 레코드를 보는 방법과 보기를 필터링하는 방법을 확인합니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.datacompare.f1
ms.assetid: f88d3350-2eaf-44cc-96a8-84008b6cd071
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 750909ea5344d5972ffdc8a2db418d8c482231f5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895759"
---
# <a name="how-to-view-data-differences"></a>방법: 데이터 차이 보기

두 데이터베이스의 데이터를 비교한 후에는 사용자가 비교한 각 ‘데이터베이스 개체’ 및 해당 상태가 표시됩니다. 또한 상태별로 그룹화된 각 개체 내에서 레코드에 대한 결과를 볼 수도 있습니다.  
  
차이를 확인한 후에는 서로 다르거나, 누락되었거나, 새로 추가된 개체 또는 레코드의 일부 또는 전체가 *원본*과 일치하도록 *대상*을 업데이트할 수 있습니다.  
  
### <a name="to-view-data-differences"></a>데이터 차이를 보려면  
  
1.  원본 및 대상의 데이터를 비교합니다.  
  
2.  (선택 사항) 다음 중 하나 또는 모두를 수행합니다.  
  
    -   기본적으로 상태에 관계없이 모든 개체에 대한 결과가 표시됩니다. 특정 상태의 개체만 표시하려면 **필터** 목록에서 옵션을 클릭합니다.  
  
    -   특정 개체 내의 레코드에 대한 결과를 보려면 기본 결과 창에서 개체를 클릭한 후 [레코드 뷰] 창에서 탭을 클릭합니다. 각 탭에는 특정 상태(서로 다름, 원본에만 있음, 대상에만 있음 및 동일함)의 개체 내에 있는 모든 레코드가 표시됩니다. 데이터는 레코드 및 열을 기준으로 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
[방법: 스키마 비교를 사용하여 서로 다른 데이터베이스 정의 비교](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
