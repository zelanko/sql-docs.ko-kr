---
title: 패키지 실행 태스크 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.executepackagetask.parameter.F1
- sql12.dts.designer.executepackagetask.package.f1
- sql12.dts.designer.executepackagetask.general.f1
ms.assetid: c2c96b4f-eb10-4d8b-be34-88edfd0785fb
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 45d295035ecd4b01b481fc40573336a0fc5a0109
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182846"
---
# <a name="execute-package-task-editor"></a>패키지 실행 태스크 편집기
  패키지 실행 태스크 편집기로 패키지 실행 태스크를 구성합니다. 패키지 실행 태스크는 패키지가 다른 패키지를 워크플로의 일부로 실행할 수 있도록 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 엔터프라이즈 기능을 확장했습니다.  
  
 **수행 작업**  
  
-   [패키지 실행 태스크 편집기 열기](#open)  
  
-   [일반 페이지에서 옵션 설정](#general)  
  
-   [패키지 페이지에서 옵션 설정](#package)  
  
-   [매개 변수 바인딩 페이지에서 옵션 설정](#parameter)  
  
##  <a name="open"></a> 패키지 실행 태스크 편집기 열기  
  
1.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 패키지 실행 태스크가 들어 있는 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 프로젝트를 엽니다.  
  
2.  SSIS 디자이너에서 태스크를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
##  <a name="general"></a> 일반 페이지에서 옵션 설정  
 **이름**  
 패키지 실행 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 패키지 실행 태스크에 대한 설명을 입력합니다.  
  
##  <a name="package"></a> 패키지 페이지에서 옵션 설정  
 **ReferenceType**  
 자식 패키지가 프로젝트 내부에 있는 경우 **프로젝트 참조** 를 선택합니다. 자식 패키지가 프로젝트 외부에 있는 경우 **외부 참조** 를 선택합니다.  
  
> [!NOTE]  
>  **ReferenceType** 옵션은 읽기 전용이며 패키지가 포함된 프로젝트가 프로젝트 배포 모델로 전환되지 않은 경우에는 **외부 참조** 로 설정됩니다. 변환에 대한 자세한 내용은 [Integration Services 서버에 프로젝트 배포](../../2014/integration-services/deploy-projects-to-integration-services-server.md)를 참조하세요.  
  
 **암호**  
 자식 패키지가 암호로 보호되어 있으면 자식 패키지의 암호를 입력하거나 줄임표 단추 (...)를 클릭하여 자식 패키지의 새 암호를 만듭니다.  
  
 `ExecuteOutOfProcess`  
 자식 패키지를 부모 패키지 프로세스에서 실행할지 아니면 별도의 프로세스에서 실행할지 지정합니다. 기본적으로 패키지 실행 태스크의 ExecuteOutOfProcess 속성 설정 `False`, 자식 패키지가 부모 패키지와 같은 프로세스에서 실행 합니다. 이 속성을 `true`로 설정하면 하위 패키지가 개별 프로세스로 실행됩니다. 이렇게 하면 하위 패키지의 실행 속도가 느려집니다. 또한 이 속성을 `true`로 설정하면 도구만 설치로 패키지를 디버깅할 수 없으며 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 제품을 설치해야 합니다. 자세한 내용은 [Integration Services 설치](install-windows/install-integration-services.md)를 참조하세요.  
  
### <a name="referencetype-dynamic-options"></a>ReferenceType 동적 옵션  
  
#### <a name="referencetype--external-reference"></a>ReferenceType = 외부 참조  
 **위치**  
 자식 패키지의 위치를 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**SQL Server**|위치를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스로 설정합니다.|  
|**파일 시스템**|파일 시스템에 위치를 설정합니다.|  
  
 **대량 삽입 태스크 편집기**  
 자식 패키지의 저장소 위치 유형을 선택합니다.  
  
 **PackageNameReadOnly**  
 패키지 이름을 표시합니다.  
  
#### <a name="referencetype--project-reference"></a>ReferenceType = 프로젝트 참조  
 **PackageNameFromProjectReference**  
 프로젝트에 포함된 패키지 중 자식 패키지로 지정할 패키지를 선택합니다.  
  
### <a name="location-dynamic-options"></a>Location 동적 옵션  
  
#### <a name="location--sql-server"></a>Location = SQL Server  
 **대량 삽입 태스크 편집기**  
 목록에서 OLE DB 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [OLE DB 연결 관리자](connection-manager/ole-db-connection-manager.md), [OLE DB 연결 관리자 구성](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **PackageName**  
 자식 패키지의 이름을 입력하거나 줄임표 (...)를 클릭하여 패키지를 찾습니다.  
  
#### <a name="location--file-system"></a>Location = 파일 시스템  
 **대량 삽입 태스크 편집기**  
 목록에서 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **PackageNameReadOnly**  
 패키지 이름을 표시합니다.  
  
##  <a name="parameter"></a> 매개 변수 바인딩 페이지에서 옵션 설정  
 부모 패키지나 프로젝트의 값을 자식 패키지에 전달할 수 있습니다. 프로젝트에서 프로젝트 배포 모델을 사용해야 하며 자식 패키지는 부모 패키지와 동일한 프로젝트에 포함되어 있어야 합니다.  
  
 프로젝트를 프로젝트 배포 모델로 변환하는 방법은 [Integration Services 서버에 프로젝트 배포](../../2014/integration-services/deploy-projects-to-integration-services-server.md)를 참조하세요.  
  
 **자식 패키지 매개 변수**  
 자식 패키지 매개 변수의 이름을 입력하거나 선택합니다.  
  
 **매개 변수 또는 변수 바인딩**  
 자식 패키지에 전달할 값이 포함된 매개 변수나 변수를 선택합니다.  
  
 **추가**  
 자식 패키지 매개 변수에 매개 변수나 변수를 매핑하려면 클릭합니다.  
  
 **제거**  
 매개 변수나 변수와 자식 패키지 매개 변수 간의 매핑을 제거하려면 클릭합니다.  
  
  