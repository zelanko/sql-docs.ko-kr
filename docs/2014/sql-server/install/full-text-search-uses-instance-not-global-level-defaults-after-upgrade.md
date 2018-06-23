---
title: 기본적으로 인스턴스 수준, 전역이 아니라 단어 분리기와 필터를 사용 하도록 전체 텍스트 검색 업그레이드 하면 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d1e4bfcaf022207afd7822740af104d6b9dbff2e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082617"
---
# <a name="upgrading-will-cause-full-text-search-to-use-instance-level-not-global-word-breakers-and-filters-by-default"></a>업그레이드하면 기본적으로 전체 텍스트 Search에서 전역 수준이 아닌 인스턴스 수준의 단어 분리기와 필터를 사용하게 됩니다.
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 새 단어 분리기와 필터를 인스턴스 수준에서 등록할 수 있습니다.  
  
## <a name="component"></a>구성 요소  
 전체 텍스트 검색  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 새 단어 분리기와 필터를 인스턴스 수준에서 등록할 수 있으므로 인스턴스 간에 기능과 보안이 분리됩니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드한 후 `sp_fulltext_service`를 사용하여 구성 요소를 로드할 수 있도록 서비스 속성 및 `load_os_resources`를 설정합니다. 다음을 실행해야 합니다.  
  
 `sp_fulltext_service 'load_os_resources', 1`  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  