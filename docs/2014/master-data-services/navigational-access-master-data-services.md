---
title: 탐색 액세스 권한(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- navigational access [Master Data Services]
- security [Master Data Services], navigational access
ms.assetid: 3403b7b0-44e2-48c3-a1b7-9c4612b874b8
caps.latest.revision: 4
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: da85747e9fe4a35eb4e86bb0fa07f677b35ea5c8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169080"
---
# <a name="navigational-access-master-data-services"></a>탐색 액세스 권한(Master Data Services)
  탐색 액세스 권한은 **모델** 탭에 지정된 모델 개체 보안에 적용됩니다.  
  
 탐색 액세스 권한은 보안 할당 수준보다 높은 수준의 액세스 권한입니다.  
  
 이 예에서는 사용 권한이 엔터티에 할당되므로 탐색 액세스 권한은 모델 수준에서 부여됩니다.  
  
 ![mds_conc_inheritance_model](../../2014/master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
 **엔터티**  
  
 엔터티, 엔터티의 리프 멤버 또는 엔터티의 통합 멤버에 사용 권한을 할당할 경우 탐색 액세스 권한을 통해 모든 멤버의 이름 및 코드를 읽거나 업데이트할 수 있습니다. 모델 이름을 읽을 수도 있습니다.  
  
 **특성**  
  
 특성에 사용 권한을 할당할 경우 탐색 액세스 권한을 통해 엔터티에 있는 모든 멤버의 이름 및 코드를 읽거나 업데이트할 수 있습니다. 모델 이름을 읽을 수도 있습니다.  
  
 **컬렉션**  
  
 컬렉션에 사용 권한을 할당할 경우 이름, 코드, 설명 및 소유자 ID를 읽거나 업데이트할 수 있습니다. 모델 이름을 읽을 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [사용 권한이 결정 되는 방법 &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)  
  
  
