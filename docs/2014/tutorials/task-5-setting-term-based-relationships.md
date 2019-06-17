---
title: '태스크 5: 용어 기반 관계 설정 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0e9a6a1a96d208077e70c0cf1835cff6e34650dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489118"
---
# <a name="task-5-setting-term-based-relationships"></a>태스크 5: 용어 기반 관계 설정
  이 태스크에서는 몇 가지 용어 기반 관계에 대 한 값에 대 한 정의 **Supplier Name** 도메인입니다. 용어 기반 관계를 사용하면 도메인에서 값의 일부인 용어를 수정할 수 있습니다. 이를 통해 공통 부분의 맞춤법을 제외하고 동일한 여러 값을 동일한 동의어로 간주할 수 있습니다. 예를 들어 **Inc.** 로 수정할 수 있습니다 **Incorporated**합니다. DQS는 기술 자료 검색, 정리 또는 일치 프로세스에서 이러한 관계를 사용합니다. 참조 [만들 용어 기반 관계](https://msdn.microsoft.com/library/hh510404.aspx) 대 한 자세한 내용은 합니다.  
  
1.  선택 **Supplier Name** 에 **도메인 목록**합니다.  
  
2.  으로 전환 합니다 **용어 기반 관계** 오른쪽 창에서 탭 합니다.  
  
3.  클릭 **새 관계 추가** 테이블에는 관계를 추가 하려면 도구 모음의 단추입니다.  
  
4.  형식 **Co.** 에 대 한 합니다 **값** 필드 및 **회사** 에 대 한 합니다 **수정** 필드입니다.  
  
5.  다음 값에 대해 위의 두 단계를 반복합니다.  
  
    |값|다음으로 수정|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![용어 기반 관계](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "용어 기반 관계")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 6: 동의어 설정](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
