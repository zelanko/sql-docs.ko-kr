---
title: 하드웨어 구성-Analytics Platform System | Microsoft Docs
description: Analytics Platform System (APS) 어플라이언스 하드웨어 비즈니스 요구 사항에 따라 적절 한 양의 처리 및 저장소를 구매할 수 있도록 확장 가능한 단위를 사용 하 여 설계 됩니다. 6 또는 페타바이트 단위의 데이터 테라바이트에서 Parallel Data Warehouse에 대 한 저장소를 확장 하는 어플라이언스입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f3e1759dcde0dd792ce5179de08e9add1ef355e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960890"
---
# <a name="hardware-configurations---analytics-platform-system"></a>하드웨어 구성-Analytics Platform System
Analytics Platform System (APS) 하드웨어는 비즈니스 요구 사항에 따라 적절 한 양의 처리 및 저장소를 구매할 수 있도록 확장 가능한 단위를 사용 하 여 설계 됩니다. 어플라이언스에 대 한 SQL Server 데이터 Wareouse PDW (병렬) 테라바이트에서 6 또는 페타바이트 단위의 데이터 저장소를 확장합니다.  
  
## <a name="contents"></a>내용  
  
-   [1 랙 구성](#section1)  
  
-   [다중 랙 구성](#section2)  

  
## <a name="section1"></a>1 랙 구성  
첫 번째 랙 어플라이언스에서 PDW를 실행 하는 데 필요한 구성 요소를 포함 합니다. 최소 어플라이언스 구성 랙, 네트워크 및 기본 배율 단위입니다. 이러한 다이어그램 어플라이언스의 첫 번째 랙을 구성할 수 있는 방법을 보여 줍니다. 하드웨어 공급 업체에 따라 첫 번째 랙의 2 자에서 9 계산 노드 간에 사용할 수 있습니다.  
  
### <a name="first-rack-configurations---dell"></a>먼저 구성-DELL를 랙  
DELL 어플라이언스에 대 한 최소 구성에 3 개의 계산 노드가 있습니다. 총 계산 노드 9의 첫 번째 랙에 최대 2 명의 데이터 배율 단위를 추가할 수 있습니다.  
  
![첫 번째 랙 구성 Dell](media/first-rack-configurations-dell.png "Dell 첫 번째 랙 구성")  
  
### <a name="first-rack-configurations---hpe"></a>먼저 구성-HPE 랙  
HPE 어플라이언스의 최소 구성을 계산 노드 2에 있습니다. 총 8 개의 계산 노드로 구성의 첫 번째 랙을 최대 3 명의 데이터 배율 단위를 추가할 수 있습니다.  
  
![HPE HPE에 대 한 구성을 먼저 랙](media/first-rack-configurations-hpe.png "HPE 구성을 먼저 랙")  
  
## <a name="section2"></a>다중 랙 구성  
PDW에 용량을 추가 하려면 네트워킹, 적절 한 기능을 제공 하는 데 필요한 추가 랙 & 네트워크 구성 요소와 함께 데이터 배율 단위를 추가 하 고 인프라를 랙 키를 누릅니다. 각 추가 랙 & 네트워크에는 수동 호스트가 필요 합니다.  
  
각 하드웨어 공급 업체에 어플라이언스의 용량을 지정 된 데이터 배율 단위를 추가할 수 있습니다 수를 지정 합니다. 충분 한 데이터 배율 단위는 20% 되며 성능에 최소한 참조를 추가 하는 것이 좋습니다. 예를 들어 추가 1 데이터 규모 단위를 20 데이터 배율 단위에 이미 있는 어플라이언스에 될 수 있습니다 성능 향상. 비용과 노력이 가치가 net 향상이 됩니다.  
  
### <a name="scale-out-example---hpe"></a>예제-HPE 확장  
이 다이어그램에는 20 개의 계산 노드가 포함 된 3 개의 랙 HP 어플라이언스를 보여 줍니다.  
  
![20 개의 계산 노드를 사용 하 여 HPE 어플라이언스](media/scale-out-hpe.png "20 개의 계산 노드를 사용 하 여 HPE 어플라이언스")  
  
### <a name="scale-out-example---dell-quanta"></a>예제-DELL, Quanta 확장  
이 다이어그램에서는 21 계산 노드를 포함 하는 3 개의 랙 DELL 또는 Quanta 어플라이언스를 보여 줍니다.  
  
![21 계산 노드가 포함 된 어플라이언스 Dell](media/scale-out-dell.png "21 계산 노드를 사용 하 여 Dell 어플라이언스")  
 
