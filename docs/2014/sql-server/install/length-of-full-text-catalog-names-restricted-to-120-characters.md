---
title: 전체 텍스트 카탈로그 이름의 길이 120 자로 제한 됩니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text catalogs names
ms.assetid: 50633373-83f6-4ed9-99b9-71f92479a14f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f11c8b5a0698c83846f1570946a551f82a09ab48
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183356"
---
# <a name="length-of-full-text-catalog-names-restricted-to-120-characters"></a>전체 텍스트 카탈로그 이름의 길이는 120자로 제한됩니다.
  이전 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 128자였던 전체 텍스트 카탈로그 이름 길이가 모두 120자로 제한됩니다.  
  
## <a name="description"></a>Description  
 이 변경 사항은 기존 카탈로그 이름에는 영향을 주지 않지만 이름이 120자보다 긴 전체 텍스트 카탈로그를 만드는 스크립트를 실행하면 오류가 발생하게 합니다. 카탈로그 이름은 카탈로그에 해당하는 논리적 파일 이름을 생성하는 데 사용됩니다.  
  
## <a name="corrective-action"></a>수정 동작  
 카탈로그 이름을 120자로 제한하도록 전체 텍스트 카탈로그를 만드는 모든 스크립트를 수정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  