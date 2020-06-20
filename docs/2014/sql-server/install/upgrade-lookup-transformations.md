---
title: 조회 변환 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 74430ab1bed232b8d510a8c28a8a690d88d1f6ba
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85041651"
---
# <a name="upgrade-lookup-transformations"></a>조회 변환 업그레이드
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 로 업그레이드하는 경우 새로운 조회 변환 기능을 활용하도록 패키지를 수정하는 것이 좋습니다. 새로운 조회 변환에서는 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]에서 사용할 수 있는 캐싱 유형 및 데이터 출력 옵션을 지원합니다. 캐싱 및 데이터 출력에 대한 자세한 내용은 [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md)을 참조하십시오.  
  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]에서 사용할 수 있는 캐싱 유형으로는 전체 캐싱, 부분 캐싱 및 캐싱 안 함이 있습니다. [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]에서는 이러한 캐싱 유형 중 하나를 사용하도록 조회 변환을 구성할 수 있습니다. 부분 캐싱을 구현 하거나 캐싱을 하지 않는 방법에 대 한 자세한 내용은 [캐시 없음 또는 부분 캐시 모드로 조회 구현](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)을 참조 하세요. 전체 캐싱을 구현 하는 방법에 대 한 자세한 내용은 [캐시 연결 관리자를 사용 하 여 전체 캐시 모드에서 조회 변환 구현](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md) 및 [OLE DB 연결 관리자를 사용 하 여 전체 캐시 모드에서 조회 변환 구현](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)을 참조 하세요.  
  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]에서는 조회 변환에 입력, 출력 및 오류 출력 옵션을 사용할 수 있습니다. 참조 데이터 세트에 일치하는 항목이 있는 입력의 행은 출력에 의해 처리됩니다. 일치하는 항목이 없는 입력의 행은 오류로 처리되어 오류 출력으로 리디렉션될 수 있습니다. [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]에서는 조회 변환에 일치 항목 출력과 불일치 항목 출력이라는 두 가지 유형의 출력이 있습니다.  
  
 기본적으로 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 만든 조회 변환을 실행하면 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 에서 일치하는 항목이 없는 행을 오류로 간주하고 오류 출력으로 리디렉션할 수 있습니다. 또한 이러한 행을 오류가 아닌 것으로 간주하고 불일치 항목 출력으로 리디렉션할 수도 있습니다.  
  
 자세한 내용은 [조회 변환 편집기 &#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [조회 변환](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
