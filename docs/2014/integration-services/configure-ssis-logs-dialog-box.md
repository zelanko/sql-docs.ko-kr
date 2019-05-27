---
title: SSIS 로그 구성 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.configuredtslogs.loggingdetails.f1
- sql12.dts.designer.configuredtslogs.providersandlogs.f1
- sql12.dts.designer.configuredtslogs.containers.f1
helpviewer_keywords:
- Configure SSIS Logs dialog box
ms.assetid: 4b980275-cd9a-4943-8c36-727d51f9a484
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f881435de01c7c21b80bff00b43c2399d0f7d75
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060590"
---
# <a name="configure-ssis-logs-dialog-box"></a>SSIS 로그 구성 대화 상자
  **SSIS 로그 구성** 대화 상자를 사용하여 패키지에 대한 로깅 옵션을 정의할 수 있습니다.  
  
 **수행 작업**  
  
1.  [SSIS 로그 구성 대화 상자 열기](#open_dialog)  
  
2.  [컨테이너 창의 옵션 구성](#container)  
  
3.  [공급자 및 로그 탭의 옵션 구성](#provider)  
  
4.  [자세히 탭의 옵션 구성](#detail)  
  
##  <a name="open_dialog"></a> SSIS 로그 구성 대화 상자 열기  
 **SSIS 로그 구성 대화 상자를 열려면**  
  
-   [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 **SSIS** 메뉴에서 **로깅** 을 클릭합니다.  
  
##  <a name="container"></a> 컨테이너 창의 옵션 구성  
 **SSIS 로그 구성** 대화 상자의 **컨테이너** 창을 사용하여 패키지 및 해당 컨테이너에 대해 로깅을 활성화할 수 있습니다.  
  
### <a name="options"></a>변수  
 **SSIS 로그 구성**  
 패키지 및 해당 컨테이너에 대해 로깅을 활성화하려면 계층 뷰의 확인란을 선택합니다.  
  
-   확인란의 선택을 취소하면 해당 컨테이너에 대해 로깅이 활성화되지 않습니다. 로깅을 활성화하려면 선택합니다.  
  
-   확인란이 흐리게 표시된 경우에는 해당 컨테이너에서 부모의 로깅 옵션을 사용하는 것입니다. 패키지에 대해서는 이 옵션을 사용할 수 없습니다.  
  
-   확인란을 선택하면 컨테이너에서 자체 로깅 옵션을 정의합니다.  
  
 컨테이너가 흐리게 표시되어 있는 경우 해당 컨테이너에 대해 로깅 옵션을 설정하려면 확인란을 두 번 클릭합니다. 첫 번째 클릭은 확인란의 선택을 취소하고 두 번째 클릭은 확인란을 선택하여 사용할 로그 공급자 및 기록할 정보를 선택할 수 있습니다.  
  
##  <a name="provider"></a> 공급자 및 로그 탭의 옵션 구성  
 **SSIS 로그 구성** 대화 상자의 **공급자 및 로그** 탭을 사용하여 런타임 이벤트를 캡처하기 위한 로그를 생성 및 구성할 수 있습니다.  
  
### <a name="options"></a>변수  
 **공급자 유형**  
 목록에서 로그 공급자 유형을 선택합니다.  
  
 **추가**  
 지정한 유형의 로그를 패키지의 로그 공급자 모음에 추가합니다.  
  
 **이름**  
 **SSIS 로그 구성** 대화 상자의 **컨테이너** 창에서 선택한 컨테이너 또는 태스크에 대한 로그를 확인란을 사용하여 설정하거나 해제합니다. 이름 필드는 편집할 수 있습니다. 공급자의 기본 이름을 사용하거나 설명이 포함된 고유 이름을 입력합니다.  
  
 **설명**  
 설명 필드는 편집할 수 있습니다. 클릭한 다음 로그의 기본 설명을 수정합니다.  
  
 **Configuration**  
 목록에서 기존 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다. 로그 공급자의 유형에 따라 OLE DB 연결 관리자 또는 파일 연결 관리자를 구성할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 이벤트 로그의 로그 공급자에는 연결이 필요하지 않습니다.  
  
 관련 항목: [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md), [File Connection Manager](connection-manager/file-connection-manager.md)  
  
 **Delete**  
 로그 공급자를 선택한 다음 **삭제**를 클릭합니다.  
  
##  <a name="detail"></a> 자세히 탭의 옵션 구성  
 **SSIS 로그 구성** 대화 상자의 **자세히** 탭을 사용하여 로깅에 사용할 이벤트와 로깅할 세부 정보를 지정할 수 있습니다. 선택한 정보는 패키지의 모든 로그 공급자에 적용됩니다. 예를 들어 일부 정보는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 쓰고 다른 정보는 텍스트 파일에 쓰는 것은 불가능합니다.  
  
### <a name="options"></a>변수  
 **이벤트**  
 로깅할 이벤트를 설정 또는 해제합니다.  
  
 **설명**  
 이벤트에 대한 설명을 표시합니다.  
  
 **고급**  
 로깅할 이벤트를 선택하거나 선택을 취소하고, 각 이벤트에 대해 로깅할 정보를 선택하거나 선택을 취소합니다. 이벤트 목록을 제외한 모든 로깅 세부 정보를 숨기려면 **기본** 을 클릭합니다. 다음은 로깅에 사용할 수 있는 정보입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Computer**|로깅된 이벤트가 발생한 컴퓨터의 이름입니다.|  
|**연산자**|패키지를 시작한 사람의 사용자 이름입니다.|  
|**SourceName**|로깅된 이벤트가 발생한 패키지, 컨테이너 및 태스크의 이름입니다.|  
|**SourceID**|로깅된 이벤트가 발생한 패키지, 컨테이너 또는 태스크의 GUID(Global Unique Identifier)입니다.|  
|**ExecutionID**|패키지 실행 인스턴스의 GUID(Global Unique Identifier)입니다.|  
|**MessageText**|로그 항목과 연결된 메시지입니다.|  
|**DataBytes**|나중에 사용하도록 예약되어 있습니다.|  
  
 **기본**  
 로깅할 이벤트를 선택하거나 선택을 취소합니다. 이 옵션은 이벤트 목록을 제외한 로깅 세부 정보를 숨깁니다. 이벤트를 선택한 경우 해당 이벤트에 대한 모든 로깅 세부 정보가 기본적으로 선택됩니다. 로깅 세부 정보를 모두 표시하려면 **고급** 을 클릭합니다.  
  
 **로드**  
 로깅 옵션을 설정하기 위한 템플릿으로 사용할 기존 XML 파일을 지정합니다.  
  
 **저장**  
 구성 세부 정보를 XML 파일에 템플릿으로 저장합니다.  
  
  
