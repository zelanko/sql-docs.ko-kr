---
title: "데이터 마이닝 모니터링 하려면 SQL Server Profiler를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 655ac93c-5c5c-4565-914b-915327f7d349
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96b5485ebddba8823f262ba6a2229018d82a72fd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>SQL Server 프로파일러를 사용하여 데이터 마이닝 모니터링(Analysis Services - 데이터 마이닝)
  필요한 권한이 있는 경우 SQL Server 프로파일러를 사용하여 SQL Server Analysis Services 인스턴스에 보낸 요청으로 실행된 데이터 마이닝 작업을 모니터링할 수 있습니다. 데이터 마이닝 작업에는 모델 또는 구조의 처리, 예측 또는 내용 쿼리, 새 모델 또는 구조의 작성 등이 포함될 수 있습니다.  
  
 SQL Server Profiler는 모든 작업에 동일한 SQL Server Analysis Services 인스턴스가 사용되는 한 **trace** 를 사용하여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], SQL Server Management Studio, 웹 서비스, Excel용 데이터 마이닝 추가 기능 등의 여러 클라이언트에서 보낸 요청을 모니터링합니다. 모니터링할 각 SQL Server Analysis Services 인스턴스에 대해서는 별도의 추적을 만들어야 합니다. 추적에 대한 일반적인 정보와 SQL Server Profiler를 사용하는 방법은 [SQL Server Profiler를 사용하여 Analysis Services 모니터링](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)을 참조하세요.  
  
 캡처할 이벤트의 유형에 대한 구체적인 지침은 [재생에 대한 프로파일러 추적 만들기&#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)를 참조하세요.  
  
## <a name="using-traces-to-monitor-data-mining"></a>추적을 사용하여 데이터 마이닝 모니터링  
 추적 정보를 캡처할 때는 SQL Server 인스턴스에서 캡처 정보를 파일에 저장할지 아니면 테이블에 저장할지 여부를 지정할 수 있습니다. 데이터를 저장하기 위해 사용하는 방법에 관계없이 SQL Server 프로파일러를 사용하여 추적을 보고 이벤트를 기준으로 필터링할 수 있습니다. 다음 표에서는 데이터 마이닝과 관련된 기본 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 추적의 몇 가지 이벤트 및 하위 클래스를 보여 줍니다.  
  
|EventClass|EventSubclass|Description|  
|----------------|-------------------|-----------------|  
|**Query Begin**<br /><br /> **쿼리 끝**|**0 - MDXQuery**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 저장 프로시저에 대한 모든 호출의 텍스트를 포함합니다.|  
|**Query Begin**<br /><br /> **쿼리 끝**|**1 - DMXQuery**|DMX(Data Mining Extensions) 문의 텍스트와 결과를 포함합니다.|  
|**Progress Report Begin**<br /><br /> **Progress Report End**|**34 - DataMiningProgress**|데이터 마이닝 알고리즘의 진행률에 대한 정보를 제공합니다. 예를 들어 클러스터링 모델을 작성하는 경우 작성 중인 후보 클러스터를 알려 주는 진행률 메시지가 나타납니다.|  
|**Query Begin**<br /><br /> **쿼리 끝**|EXECUTESQL|실행 중인 Transact-SQL 쿼리의 텍스트를 포함합니다.|  
|**Query Begin**<br /><br /> **쿼리 끝**|**2- SQLQuery**|시스템 테이블 형식의 스키마 행 집합에 대한 쿼리의 텍스트를 포함합니다.|  
|**DISCOVER Begin**<br /><br /> **DISCOVER End**|여러 항목|XMLA로 캡슐화된 DMX 함수 호출 또는 DISCOVER 문의 텍스트를 포함합니다.|  
|**오류**|(없음)|서버에서 클라이언트로 보낸 오류의 텍스트를 포함합니다.<br /><br /> **오류(데이터 마이닝):** 이나 **정보(데이터 마이닝):** 가 앞에 오는 오류 메시지는 특별히 DMX 요청에 대한 응답으로 생성됩니다. 그러나 이러한 오류 메시지를 보는 것만으로는 충분하지 않습니다. 파서에서 생성하는 오류 메시지와 같은 다른 오류 메시지도 데이터 마이닝과 관련이 있을 수 있지만 이러한 접두사는 없습니다.|  
  
 추적 로그에 있는 명령 문을 보면 시스템 저장 프로시저에 대한 호출을 포함하여 클라이언트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버로 보낸 복잡한 문의 구문도 볼 수 있습니다. 이 정보를 사용하여 디버깅을 수행하거나 유효한 문을 새 예측 쿼리 또는 모델을 만들기 위한 템플릿으로 사용할 수 있습니다. 추적을 통해 캡처할 수 있는 저장 프로시저 호출의 예는 [클러스터링 모델 쿼리 예제](../../analysis-services/data-mining/clustering-model-query-examples.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 인스턴스 모니터](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [SQL Server 확장 이벤트를 사용하여 Analysis Services 모니터링](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  

