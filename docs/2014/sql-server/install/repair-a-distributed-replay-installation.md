---
title: Distributed Replay 설치를 복구 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8adf917831b33c1603b3c0c4a1e7b678900cf7dd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36171893"
---
# <a name="repair-a-distributed-replay-installation"></a>Distributed Replay 설치 복구
  Distributed Replay 구성 요소(컨트롤러 또는 서비스)를 복구하면 다음 작업이 수행됩니다.  
  
1.  관련된 모든 파일이 디스크에 다시 설치되어 기존 파일이 대체됩니다.  
  
2.  해당 서비스 계정이 제거되었으면 Windows 서비스 계정을 다시 만듭니다.  
  
 복구 작업으로 구성 요소를 추가하거나 제거할 수 없습니다. 를 추가 하거나 구성 요소를 제거 하려면 선택 하거나 선택 취소할 기능 트리에서 해당 구성 요소에는 **기능 선택** 페이지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 합니다.  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>실패한 Distributed Replay 설치를 복구하려면  
  
1.  **시작** 메뉴를 클릭 하 여 **제어판**, 두 번 클릭 하 고 **프로그램 추가 / 제거**합니다.  
  
2.  선택 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에 **제거 또는 변경 프로그램** 창, 한 다음는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 대화 상자를 클릭 **복구**합니다.  
  
3.  단계에 따라는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 마법사, 및는 **기능 선택** 페이지에서 Distributed Replay 구성 요소를 복구 하 고 클릭 하려는 **다음.** 합니다.  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 마법사를 완료하여 선택한 Distributed Replay 기능을 복구합니다.  
  
  