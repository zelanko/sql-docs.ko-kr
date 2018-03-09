---
title: "Hadoop 하이브 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hadoophivetask.f1
ms.assetid: 10ff37c0-9f3f-442a-889b-c351afbdc74c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66e0ac41dbc9015be94ec18180a5c8fa3932efe9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="hadoop-hive-task"></a>Hadoop 하이브 태스크
  Hadoop 하이브 태스크를 사용하여 Hadoop 클러스터에서 하이브 스크립트를 실행합니다.  
  
 Hadoop 하이브 태스크를 추가하려면 태스크를 디자이너로 끌어서 놓습니다. 그런 다음 태스크를 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집**을 클릭하여 **Hadoop 하이브 태스크 편집기** 대화 상자를 엽니다.  
  
 ![Hadoop 하이브 태스크 편집기](../../integration-services/control-flow/media/hadoop-hive-task.png "Hadoop 하이브 태스크 편집기")  
  
## <a name="options"></a>변수  
 **Hadoop 하이브 태스크 편집기** 대화 상자에서 다음 옵션을 구성합니다.  
  
|필드|Description|  
|-----------|-----------------|  
|**Hadoop 연결**|기존 Hadoop 연결 관리자를 지정하거나 새 연결 관리자를 만듭니다. 이 연결 관리자는 WebHCat 서비스가 호스트되는 위치를 나타냅니다.|  
|**SourceType**|쿼리의 원본 유형을 지정합니다. 사용 가능한 값은 **ScriptFile** 및 **DirectInput**입니다.|  
|**InlineScript**|**SourceType** 의 값이 **DirectInput**일 때 하이브 스크립트를 지정합니다.|  
|**HadoopScriptFilePath**|**SourceType** 의 값이 **ScriptFile**일 때 Hadoop의 스크립트 파일 경로를 지정합니다.|  
|**TimeoutInMinutes**|제한 시간 값을 분 단위로 지정합니다. Hadoop 작업은 제한 시간이 경과할 때까지 완료되지 않은 경우 중지됩니다. Hadoop 작업이 비동기적으로 실행되도록 예약하려면 값으로 0을 지정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Hadoop 연결 관리자](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
