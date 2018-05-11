---
title: HDFS 파일 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfilesrc.f1
ms.assetid: f8cda200-c389-4a2e-8ee9-5d59b326aac1
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4f3866b56645b9e484f07ac775f4b642defc5d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="hdfs-file-source"></a>HDFS 파일 원본
  SSIS 패키지는 HDFS 파일 원본 구성 요소를 통해 HDFS 파일에서 데이터를 읽을 수 있습니다. 지원되는 파일 형식은 Text 및 Avro입니다. ORC 원본은 지원되지 않습니다.  
  
 HDFS 파일 원본을 구성하려면 데이터 흐름 디자이너에서 HDFS 파일 원본을 끌어서 놓은 다음 구성 요소를 두 번 클릭하여 편집기를 엽니다.  
  
 ![HDFS 파일 원본 편집기](../../integration-services/data-flow/media/hdfs-file-source.png "HDFS 파일 원본 편집기")  
  
## <a name="options"></a>변수  
 **Hadoop 파일 원본 편집기** 대화 상자의 **일반** 탭에서 다음 옵션을 구성합니다.  
  
|필드|Description|  
|-----------|-----------------|  
|**Hadoop 연결**|기존 Hadoop 연결 관리자를 지정하거나 새 연결 관리자를 만듭니다. 이 연결 관리자는 HDFS 파일이 호스트되는 위치를 나타냅니다.|  
|**파일 경로**|HDFS 파일의 이름을 지정합니다.|  
|**파일 형식**|HDFS 파일의 형식을 지정합니다. 사용할 수 있는 옵션은 Text 또는 Avro입니다. ORC 원본은 지원되지 않습니다.|  
|**열 구분 기호 문자**|텍스트 형식을 선택하는 경우 열 구분 기호 문자를 지정합니다.|  
|**첫 번째 데이터 행의 열 이름**|텍스트 형식을 선택하는 경우 파일의 첫 행에 열 이름을 포함할지 여부를 지정합니다.|  
  
 이러한 옵션을 구성한 후 **열** 탭을 선택하여 데이터 흐름에서 원본 열을 대상 열에 매핑합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Hadoop 연결 관리자](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS 파일 대상](../../integration-services/data-flow/hdfs-file-destination.md)  
  
  
