---
title: 하드웨어 구성
description: 사용자의 비즈니스 요구 사항에 따라 적절 한 크기의 처리 및 저장소를 구입할 수 있도록 AP (분석 플랫폼 시스템) 어플라이언스 하드웨어는 확장 가능 단위로 설계 됩니다. 어플라이언스는 병렬 데이터 웨어하우스의 저장소를 몇 테라바이트에서 6 페타바이트의 데이터로 확장 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee16045931da345f06c141597ccd25d19a36dea7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401128"
---
# <a name="hardware-configurations---analytics-platform-system"></a>하드웨어 구성-분석 플랫폼 시스템
분석 플랫폼 시스템 (AP) 하드웨어는 비즈니스 요구 사항에 따라 적절 한 크기의 처리 및 저장소를 구입할 수 있도록 확장 가능 단위로 설계 되었습니다. 어플라이언스는 몇 테라바이트에서 6 페타바이트의 데이터를 통해 SQL Server의 PDW (병렬 데이터 Wareouse)에 대 한 저장소를 확장 합니다.  
  
## <a name="contents"></a>콘텐츠  
  
-   [원 랙 구성](#section1)  
  
-   [멀티 랙 구성](#section2)  

  
## <a name="section1"></a>원 랙 구성  
기기의 첫 번째 랙에는 PDW를 실행 하는 데 필요한 구성 요소가 포함 되어 있습니다. 최소 어플라이언스 구성은 랙 및 네트워크와 기본 배율 단위입니다. 이러한 다이어그램은 어플라이언스의 첫 번째 랙을 구성할 수 있는 방법을 보여 줍니다. 하드웨어 공급 업체에 따라 첫 번째 랙의 계산 노드 2 ~ 9 개를 사용할 수 있습니다.  
  
### <a name="first-rack-configurations---dell"></a>첫 번째 랙 구성-DELL  
DELL 어플라이언스에 대 한 최소 구성에는 3 개의 계산 노드가 있습니다. 총 9 개의 계산 노드를 위해 첫 번째 랙에 최대 2 개의 데이터 배율 단위를 추가할 수 있습니다.  
  
![Dell 최초 랙 구성](media/first-rack-configurations-dell.png "Dell 최초 랙 구성")  
  
### <a name="first-rack-configurations---hpe"></a>첫 번째 랙 구성-HPE  
HPE 어플라이언스에 대 한 최소 구성에는 2 개의 계산 노드가 있습니다. 총 8 개의 계산 노드를 위해 첫 번째 랙에 최대 3 개의 데이터 배율 단위를 추가할 수 있습니다.  
  
![HPE에 대 한 첫 번째 랙 구성 HPE](media/first-rack-configurations-hpe.png "HPE 첫 번째 랙 구성")  
  
## <a name="section2"></a>멀티 랙 구성  
PDW에 용량을 추가 하려면 적절 한 전원, 네트워킹 및 랙 인프라를 제공 하기 위해 필요에 따라 추가 랙 & 네트워크 구성 요소와 함께 데이터 확장 단위를 추가할 수 있습니다. 각 추가 랙 & 네트워크에는 수동 호스트가 필요 합니다.  
  
각 하드웨어 공급 업체는 어플라이언스의 용량에 따라 추가할 수 있는 데이터 확장 단위의 수를 지정 합니다. 최소한 20%의 성능 되며, 전을 보기 위해 충분 한 데이터 배율 단위를 추가 하는 것이 좋습니다. 예를 들어 데이터 배율 단위가 20 개인 어플라이언스에 데이터 배율 단위 하나를 추가 하면 성능이 저하 될 수 있습니다. 네트워크를 활용 하는 것은 비용과 노력이 가치가 없습니다.  
  
### <a name="scale-out-example---hpe"></a>규모 확장 예제-HPE  
이 다이어그램에서는 20 개의 계산 노드가 포함 된 3 개의 랙 HP 어플라이언스를 보여 줍니다.  
  
![20 개의 계산 노드가 있는 HPE 어플라이언스](media/scale-out-hpe.png "20 개의 계산 노드가 있는 HPE 어플라이언스")  
  
### <a name="scale-out-example---dell-quanta"></a>Scale Out 예-DELL, 퀀텀  
이 다이어그램은 21 개의 계산 노드가 포함 된 랙 DELL 또는 퀀텀 어플라이언스 3 개를 보여 줍니다.  
  
![21 개 계산 노드를 포함 하는 Dell 어플라이언스](media/scale-out-dell.png "21 개 계산 노드를 포함 하는 Dell 어플라이언스")  
 
