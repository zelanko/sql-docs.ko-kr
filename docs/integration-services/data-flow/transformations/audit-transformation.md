---
title: "감사 변환 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.audittrans.f1
- sql13.dts.designer.audittransformation.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
caps.latest.revision: "46"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa1ed88a75603d7a943dfb05089c0a79092507ef
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="audit-transformation"></a>감사 변환
  감사 변환을 사용하면 패키지가 실행되는 환경에 대한 데이터를 패키지의 데이터 흐름에 포함할 수 있습니다. 예를 들어 패키지, 컴퓨터 및 운영자의 이름을 데이터 흐름에 추가할 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 는 이 정보를 제공하는 시스템 변수를 포함합니다.  
  
## <a name="system-variables"></a>시스템 변수  
 다음 표에서는 감사 변환에 사용할 수 있는 시스템 변수를 설명합니다.  
  
|시스템 변수|인덱스|Description|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|패키지의 실행 인스턴스를 식별하는 GUID입니다.|  
|**PackageID**|1.|패키지의 고유 식별자입니다.|  
|**PackageName**|2|패키지 이름.|  
|**VersionID**|3|패키지 버전입니다.|  
|**ExecutionStartTime**|4|패키지 실행 시작 시간입니다.|  
|**MachineName**|5|컴퓨터 이름|  
|**UserName**|6|패키지를 시작한 사용자의 로그인 이름입니다.|  
|**TaskName**|7|감사 변환이 연결된 데이터 흐름 태스크 이름입니다.|  
|**TaskId**|8|데이터 흐름 태스크의 고유 식별자입니다.|  
  
## <a name="configuration-of-the-audit-transformation"></a>감사 변환 구성  
 변환 출력에 추가할 새 출력 열의 이름을 지정한 다음 해당 시스템 변수를 출력 열에 매핑하여 감사 변환을 구성합니다. 단일 시스템 변수를 여러 개의 열에 매핑할 수 있습니다.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="audit-transformation-editor"></a>감사 변환 편집기
  감사 변환을 사용하면 패키지가 실행되는 환경에 대한 데이터를 패키지의 데이터 흐름에 포함할 수 있습니다. 예를 들어 패키지, 컴퓨터 및 운영자의 이름을 데이터 흐름에 추가할 수 있습니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에는 이 정보를 제공하는 시스템 변수가 포함되어 있습니다.  
  
### <a name="options"></a>옵션  
 **출력 열 이름**  
 감사 정보를 포함할 새 출력 열의 이름을 입력합니다.  
  
 **감사 유형**  
 감사 정보를 제공할 사용 가능한 시스템 변수를 선택합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**실행 인스턴스 GUID**|패키지의 실행 인스턴스를 고유하게 식별하는 GUID를 삽입합니다.|  
|**패키지 ID**|패키지를 고유하게 식별하는 GUID를 삽입합니다.|  
|**패키지 이름**|패키지 이름을 삽입합니다.|  
|**버전 ID**|패키지 버전을 고유하게 식별하는 GUID를 삽입합니다.|  
|**실행 시작 시간**|패키지 실행이 시작된 시간을 삽입합니다.|  
|**컴퓨터 이름**|패키지가 시작된 컴퓨터 이름을 삽입합니다.|  
|**사용자 이름**|패키지를 시작한 사용자의 로그인 이름을 삽입합니다.|  
|**태스크 이름**|감사 변환이 연결된 데이터 흐름 태스크의 이름을 삽입합니다.|  
|**태스크 ID**|감사 변환이 연결된 데이터 흐름 태스크를 고유하게 식별하는 GUID를 삽입합니다.|  
  
  
