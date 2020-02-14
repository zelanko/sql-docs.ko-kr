---
title: Hadoop 파일 시스템 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e97ae33bcccee338be576138ca335bd6298e0128
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294068"
---
# <a name="hadoop-file-system-task"></a>Hadoop 파일 시스템 태스크

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Hadoop 파일 시스템 태스크에서는 SSIS 패키지가 Hadoop 클러스터에서/클러스터로/클러스터 내에서 파일을 복사할 수 있습니다.  
  
 Hadoop 파일 시스템 태스크를 추가하려면 태스크를 디자이너로 끌어서 놓습니다. 그런 다음 태스크를 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집**을 클릭하여 **Hadoop 파일 시스템 태스크 편집기** 대화 상자를 엽니다.  
  
 ![Hadoop 파일 시스템 태스크 편집기](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Hadoop 파일 시스템 태스크 편집기")  
  
## <a name="options"></a>옵션  
 **Hadoop 파일 시스템 태스크 편집기** 대화 상자에서 다음 옵션을 구성합니다.  
  
|필드|Description|  
|-----------|-----------------|  
|**Hadoop 연결**|기존 Hadoop 연결 관리자를 지정하거나 새 연결 관리자를 만듭니다. 이 연결 관리자는 대상 파일이 호스트되는 위치를 나타냅니다.|  
|**Hadoop 파일 경로**|HDFS의 파일 또는 디렉터리 경로를 지정합니다.|  
|**Hadoop 파일 형식**|HDFS 파일 시스템 개체가 파일인지 아니면 디렉터리인지를 지정합니다.|  
|**대상 덮어쓰기**|대상 파일이 이미 있는 경우 덮어쓸지 여부를 지정합니다.|  
|**연산**|작업을 지정합니다. 사용할 수 있는 작업은 **CopyToHDFS**, **CopyFromHDFS**및 **CopyWithinHDFS**입니다.|  
|**로컬 파일 연결**|기존 파일 연결 관리자를 지정하거나 새 파일 연결 관리자를 만듭니다. 이 연결 관리자는 원본 파일이 호스트되는 위치를 나타냅니다.|  
|**재귀**|모든 하위 폴더를 재귀적으로 복사할지 여부를 지정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Hadoop 연결 관리자](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
