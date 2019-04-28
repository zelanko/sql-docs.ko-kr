---
title: 이전 버전의 SQL Server 데이터 마이닝 솔루션에 배포 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [Analysis Services]
- holdout [data mining]
- deploy [Analysis Services]
- time series [Analysis Services]
- deploying [Analysis Services - data mining]
- synchronization [Analysis Services]
- deployment [Analysis Services]
ms.assetid: 2715c245-f206-43af-8bf5-e6bd2585477a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1f5333d67e40d4abc10134f339e39a41c83fbcc1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722795"
---
# <a name="deploy-a-data-mining-solution-to-previous-versions-of-sql-server"></a>데이터 마이닝 솔루션을 이전 버전의 SQL Server에 배포
  이 섹션에서는 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 인스턴스에서 만든 데이터 마이닝 모델이나 데이터 마이닝 구조를 SQL Server 2005 Analysis Services를 사용하는 데이터베이스에 배포하려고 하거나 SQL Server 2005에서 만든 모델을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스에 배포할 때 발생할 수 있는 알려진 호환성 문제에 대해 설명합니다.  
  
 SQL Server 2000 Analysis Services 인스턴스로의 배포는 지원되지 않습니다.  
  
 [시계열 모델 배포](#bkmk_TimeSeries)  
  
 [홀드아웃이 있는 모델 배포](#bkmk_Holdout)  
  
 [필터가 있는 모델 배포](#bkmk_Filter)  
  
 [데이터베이스 백업에서 복원](#bkmk_Backup)  
  
 [데이터베이스 동기화 사용](#bkmk_Synch)  
  
##  <a name="bkmk_TimeSeries"></a> 시계열 모델 배포  
 SQL Server 2008에서는 보조 알고리즘인 ARIMA가 추가되어 Microsoft 시계열 알고리즘이 향상되었습니다. 시계열 알고리즘의 변경 사항에 대한 자세한 내용은 [Microsoft 시계열 알고리즘](microsoft-time-series-algorithm.md)을 참조하세요.  
  
 따라서 새 ARIMA 알고리즘을 사용하는 시계열 마이닝 모델이 SQL Server 2005 Analysis Services 인스턴스에 배포될 경우 다르게 동작할 수 있습니다.  
  
 예측에서 ARTXP 및 ARIMA 모델의 혼합 사용을 제어하기 위해 PREDICTION_SMOOTHING 매개 변수를 명시적으로 설정한 경우 이 모델을 SQL Server 2005 인스턴스에 배포하면 Analysis Services에서 매개 변수가 유효하지 않다는 오류 메시지가 나타납니다. 이 오류를 방지하려면 PREDICTION_SMOOTHING 매개 변수를 삭제하고 모델을 순수한 ARTXP 모델로 변환해야 합니다.  
  
 반대로 SQL Server 2005 Analysis Services를 사용하여 만든 시계열 모델을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스에 배포한 경우 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 마이닝 모델을 열면 먼저 정의 파일이 새 형식으로 변환되고 두 개의 새 매개 변수가 기본적으로 모든 시계열 모델에 추가됩니다. FORECAST_METHOD 매개 변수와 PREDICTION_SMOOTHING 매개 변수는 각각 기본값인 MIXED와 0.5를 사용하여 추가됩니다. 그러나 모델을 다시 처리할 때까지 모델에서는 계속 ARTXP만 예측에 사용합니다. 모델을 다시 처리하면 ARIMA와 ARTXP를 둘 다 사용하도록 모델이 변경됩니다.  
  
 따라서 모델을 변경하지 않으려면 모델을 탐색만 해야 하고 처리하면 안 됩니다. 또는 FORECAST_METHOD 또는 PREDICTION_SMOOTHING 매개 변수를 명시적으로 설정할 수도 있습니다.  
  
 혼합 모델을 구성하는 방법에 대한 자세한 내용은 [Microsoft 시계열 알고리즘 기술 참조](microsoft-time-series-algorithm-technical-reference.md)를 참조하세요.  
  
 모델의 데이터 원본에 사용되는 공급자가 SQL Client Data Provider 10이면 데이터 원본 정의도 수정하여 이전 버전의 SQL Server Native Client를 지정해야 합니다. 그렇지 않으면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서 공급자가 등록되지 않았다는 오류가 생성됩니다.  
  
##  <a name="bkmk_Holdout"></a> 홀드아웃이 있는 모델 배포  
 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 를 사용하여 데이터 마이닝 모델의 테스트에 사용되는 홀드아웃 파티션이 포함된 마이닝 구조를 만들면 이 마이닝 구조를 SQL Server 2005 인스턴스에 배포할 수 있지만 파티션 정보는 손실됩니다.  
  
 SQL Server 2005 Analysis Services에서 마이닝 구조를 열면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서 오류가 발생하고 홀드아웃 파티션이 제거된 구조가 다시 생성됩니다.  
  
 구조를 다시 작성 후 홀드 아웃 파티션의 크기를 사용할 수 없는 속성 창의; 그러나 값 \<ddl100_100:HoldoutMaxPercent > 30\</ddl100_100:HoldoutMaxPercent >)은 ASSL 스크립트 파일에 있는 수 있습니다.  
  
##  <a name="bkmk_Filter"></a> 필터가 있는 모델 배포  
 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 를 사용하여 마이닝 모델에 필터를 적용하는 경우 SQL Server 2005 인스턴스에 모델을 배포할 수 있지만 필터는 적용되지 않습니다.  
  
 마이닝 모델을 열면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 오류가 발생하고 필터가 제거된 모델이 다시 생성됩니다.  
  
##  <a name="bkmk_Backup"></a> 데이터베이스 백업에서 복원  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 만든 데이터베이스 백업은 SQL Server 2005 인스턴스로 복원할 수 없습니다. 그럴 경우 SQL Server Management Studio에서 오류가 발생합니다.  
  
 SQL Server 2005 Analysis Services 데이터베이스의 백업을 만들고 이 백업을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스로 복원하면 모든 시계열 모델이 이전 섹션에서 설명한 대로 수정됩니다.  
  
##  <a name="bkmk_Synch"></a> 데이터베이스 동기화 사용  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 SQL Server 2005로의 데이터베이스 동기화는 지원되지 않습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스를 동기화하려고 하면 서버에서 오류를 반환하고 데이터베이스 동기화가 실패합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 이전 버전과의 호환성](../analysis-services-backward-compatibility.md)  
  
  
