---
title: 업그레이드 하면 전체 텍스트 검색에서 전역, 단어 분리기 및 필터를 기본적으로 사용 하는 인스턴스 수준을 사용 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0b6cea7ab63351fad25f0205a614e364328171a9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036822"
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
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
