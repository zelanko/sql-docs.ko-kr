---
title: Distributed Replay 설치 복구 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca42f1dda184bf5cd99cad7d34f5ae9fce79478b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092955"
---
# <a name="repair-a-distributed-replay-installation"></a>Distributed Replay 설치 복구
  Distributed Replay 구성 요소(컨트롤러 또는 서비스)를 복구하면 다음 작업이 수행됩니다.  
  
1.  관련된 모든 파일이 디스크에 다시 설치되어 기존 파일이 대체됩니다.  
  
2.  해당 서비스 계정이 제거되었으면 Windows 서비스 계정을 다시 만듭니다.  
  
 복구 작업으로 구성 요소를 추가하거나 제거할 수 없습니다. 를 추가 하거나 구성 요소를 제거 하려면 선택 또는 선택 취소 기능 트리에서 해당 구성 요소에는 **기능 선택** 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 합니다.  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>실패한 Distributed Replay 설치를 복구하려면  
  
1.  **시작** 메뉴에서 클릭 **제어판**를 차례로 클릭 한 다음 **프로그램 추가 / 제거**합니다.  
  
2.  선택 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에 **제거 또는 변경 프로그램** 창에서를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 대화 상자에서 클릭 **복구**.  
  
3.  단계를 수행 합니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 마법사 및는 **기능 선택** 페이지를 복구 하 고 클릭 하려는 Distributed Replay 구성 요소를 선택 합니다 **다음.** .  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 마법사를 완료하여 선택한 Distributed Replay 기능을 복구합니다.  
  
  
