---
title: 하드웨어 구성-분석 플랫폼 시스템 | Microsoft Docs
description: Analytics Platform System (APS) 어플라이언스 하드웨어의 비즈니스 요구 사항에 따라 적절 한 양의 처리 및 저장소를 구매할 수 있도록 확장 가능한 단위와 구성 됩니다. 6 페타바이트 규모의 데이터에 수 테라바이트에 달하는에서 병렬 데이터 웨어하우스에 대 한 저장소를 확장 하는 어플라이언스 됩니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5677298e1924959c83cd95b86845e37eab7340e9
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544725"
---
# <a name="hardware-configurations---analytics-platform-system"></a>하드웨어 구성-분석 플랫폼 시스템
Analytics Platform System (APS) 하드웨어의 비즈니스 요구 사항에 따라 적절 한 양의 처리 및 저장소를 구매할 수 있도록 확장 가능한 단위와 구성 됩니다. 어플라이언스는 저장소에 대 한 SQL Server 병렬 데이터 Wareouse (PDW) 수 테라바이트에 달하는에서 6 페타바이트 규모의 데이터를 조정합니다.  
  
## <a name="contents"></a>내용  
  
-   [1 랙 구성](#section1)  
  
-   [다중 랙 구성](#section2)  

  
## <a name="section1"></a>1 랙 구성  
첫 번째 랙 기기에서 PDW를 실행 하는 데 필요한 구성 요소를 포함 합니다. 최소 어플라이언스 구성 랙 및 네트워크 외에 기본 배율 단위입니다. 이러한 다이어그램에는 어플라이언스의 첫 번째 랙을 구성할 수 있는 방법을 보여 줍니다. 하드웨어 공급 업체에 따라 첫 번째 랙에서 계산 노드 2에서 9까지 가질 수 있습니다.  
  
### <a name="first-rack-configurations---dell"></a>먼저 구성-DELL를 랙  
DELL 어플라이언스의 최소 구성을 계산 노드 3에 있습니다. 총 계산 노드 9의 첫 번째 랙에 최대 2 데이터 배율 단위를 추가할 수 있습니다.  
  
![Dell 첫 번째 랙 구성](media/first-rack-configurations-dell.png "Dell 첫 번째 랙 구성")  
  
### <a name="first-rack-configurations---hpe"></a>먼저 구성-HPE 랙  
HPE 어플라이언스의 최소 구성을 계산 노드 2에 있습니다. 총 계산 노드가 8 개인의 첫 번째 랙에 최대 3 데이터 배율 단위를 추가할 수 있습니다.  
  
![HPE HPE에 대 한 구성을 먼저 랙](media/first-rack-configurations-hpe.png "HPE는 먼저 구성 랙")  
  
## <a name="section2"></a>다중 랙 구성  
PDW에 대 용량을 추가 하려면 네트워킹, 적절 한 전원을 제공 하는 데 필요한 추가 랙 & 네트워크 구성 요소와 함께 데이터 배율 단위를 추가할 수 있으며 인프라 랙 키를 누릅니다. 각 추가 랙 & 네트워크에는 수동 호스트가 필요 합니다.  
  
각 하드웨어 공급 업체 어플라이언스의 용량을 제공 데이터 확장 단위를 추가할 수 있습니다 수를 지정 합니다. 보려면 성능에서 20 %uplift 이상 충분 한 데이터 배율 단위를 추가 하는 것이 좋습니다. 예를 들어 추가 데이터 눈금을 한 개 단위를 20 데이터 배율 단위에 이미 있는 어플라이언스에 될 수 있습니다 오히려 성능이 향상 됩니다. 향상 비용과 노력이 가치가 수 없습니다.  
  
### <a name="scale-out-example---hpe"></a>예-HPE 확장  
이 다이어그램에서는 20 개의 계산 노드가 포함 된 3 랙 HP 기기를 보여 줍니다.  
  
![20 개의 계산 노드가 HPE 기기](media/scale-out-hpe.png "20 개의 계산 노드가 있는 HPE 어플라이언스")  
  
### <a name="scale-out-example--dell-quanta"></a>예 – DELL 퀀텀 확장  
이 다이어그램에서는 21 계산 노드를 포함 하는 3 랙 DELL 또는 Quanta 어플라이언스를 보여 줍니다.  
  
![21 계산 노드가 있는 Dell 기기](media/scale-out-dell.png "21 계산 노드가 있는 Dell 어플라이언스")  
 
