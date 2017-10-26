---
title: "HDFS 파일 대상 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 02a2ecf62d91110bfd7e8a1429d5e1b835e4244e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="hdfs-file-destination"></a>HDFS 파일 대상
  SSIS 패키지는 HDFS 파일 대상 구성 요소를 통해 HDFS 파일에 데이터를 쓸 수 있습니다. 지원되는 파일 형식은 텍스트, Avro 및 ORC입니다.  
  
 HDFS 파일 대상을 구성하려면 데이터 흐름 디자이너에서 HDFS 파일 원본을 끌어서 놓은 다음 구성 요소를 두 번 클릭하여 편집기를 엽니다.  
  
 ![HDFS 파일 대상 편집기](../../integration-services/data-flow/media/hdfs-file-dest.png "HDFS 파일 대상 편집기")  
  
## <a name="options"></a>옵션  
 **Hadoop 파일 대상 편집기** 대화 상자의 **일반** 탭에서 다음 옵션을 구성합니다.  
  
|필드|Description|  
|-----------|-----------------|  
|**Hadoop 연결**|기존 Hadoop 연결 관리자를 지정하거나 새 연결 관리자를 만듭니다. 이 연결 관리자는 HDFS 파일이 호스트되는 위치를 나타냅니다.|  
|**파일 경로**|HDFS 파일의 이름을 지정합니다.|  
|**파일 형식**|HDFS 파일의 형식을 지정합니다. 사용할 수 있는 옵션은 텍스트, Avro, ORC입니다.|  
|**열 구분 기호 문자**|텍스트 형식을 선택하는 경우 열 구분 기호 문자를 지정합니다.|  
|**첫 번째 데이터 행의 열 이름**|텍스트 형식을 선택하는 경우 파일의 첫 행에 열 이름을 포함할지 여부를 지정합니다.|  
  
 이러한 옵션을 구성한 후 **열** 탭을 선택하여 데이터 흐름에서 원본 열을 대상 열에 매핑합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Hadoop 연결 관리자](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS 파일 원본](../../integration-services/data-flow/hdfs-file-source.md)  
  
  

