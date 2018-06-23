---
title: Updategram 보안 고려 사항 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- security [SQLXML], updategrams
- updategrams [SQLXML], security
ms.assetid: 00dc6cf4-a2e8-4cca-bdd6-d5122102a82d
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ad8e74b3f5a2e2f6175b7fb95a4da94420440975
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088338"
---
# <a name="updategram-security-considerations-sqlxml-40"></a>Updategram 보안 고려 사항(SQLXML 4.0)
  다음은 Updategram을 사용하기 위한 보안 지침입니다.  
  
-   Updategram을 사용하여 데이터를 업데이트할 때는 기본 매핑을 사용하지 마십시오. 기본 매핑을 사용하면 Updategram의 요소 이름이 테이블 이름에 매핑되고 특성 이름이 열에 매핑됩니다. 이렇게 되면 데이터베이스의 데이터베이스 테이블 및 열 정보가 노출되어 보안상 위험할 수 있습니다. 대신 Updategram의 요소 및 특성을 데이터베이스 테이블 및 열에 매핑하는 별도의 매핑 스키마를 지정하면 Updategram 요소 및 특성 이름이 임의적이 될 수 있고 이러한 이름과 데이터베이스 테이블 및 열 간의 필요한 매핑이 스키마에 따라 수행됩니다. 따라서 데이터베이스 정보가 Updategram에 노출되지 않습니다.  
  
-   사용자가 Updategram을 만들고 실행하는 것을 허용하지 않습니다. ASP 유형 응용 프로그램에서 동적으로 Updategram을 만들면 데이터베이스의 데이터가 위험에 노출될 수 있으므로 Updategram이 서버에 템플릿으로 상주하도록 하는 것이 좋습니다. 사용자가 템플릿으로 제공된 Updategram을 통해서만 데이터에 액세스할 수 있게 하면 이러한 위험을 제거할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLXML 4.0에서 updategram을 사용하여 데이터 수정](../updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
  
  