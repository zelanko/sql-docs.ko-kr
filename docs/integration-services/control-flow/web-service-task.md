---
description: 웹 서비스 태스크
title: 웹 서비스 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.webservicetask.f1
- sql13.dts.designer.webservicestask.general.f1
- sql13.dts.designer.webservicestask.input.f1
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cecf1f8803b0180ef6127cde203659be26f3c6c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477905"
---
# <a name="web-service-task"></a>웹 서비스 태스크

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  웹 서비스 태스크는 웹 서비스 메서드를 실행합니다. 웹 서비스 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   웹 서비스 메서드에서 반환되는 값을 변수에 기록합니다. 예를 들어 웹 서비스 메서드로부터 그 날의 최고 기온을 가져온 다음 이 값을 사용하여 열 값을 설정하는 식에 사용된 변수를 업데이트할 수 있습니다.  
  
-   웹 서비스 메서드에서 반환되는 값을 파일에 기록합니다. 예를 들어 잠재 고객 목록을 파일에 기록하고 패키지에서 이 파일을 데이터 원본으로 사용하여 데이터베이스에 파일을 기록하기 전에 데이터를 정리할 수 있습니다.  
  
## <a name="wsdl-file"></a>WSDL 파일  
 웹 서비스 태스크는 HTTP 연결 관리자를 사용하여 웹 서비스에 연결합니다. HTTP 연결 관리자는 웹 서비스 태스크와 별도로 구성되고 태스크에서 참조됩니다. HTTP 연결 관리자는 서버 URL과 같은 서버 프록시 설정, 웹 서비스 서버 액세스를 위한 자격 증명 및 제한 시간 길이를 지정합니다. 자세한 내용은 [HTTP 연결 관리자](../../integration-services/connection-manager/http-connection-manager.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  HTTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 HTTP 연결 관리자는 웹 사이트 또는 WSDL(Web Service Description Language) 파일로 연결할 수 있습니다. WSDL 파일로 연결하는 HTTP 연결 관리자의 URL에는 `?WSDL` 매개 변수가 포함됩니다(예: `https://MyServer/MyWebService/MyPage.asmx?WSDL`).  
  
 **디자이너에서 제공하는** 웹 서비스 태스크 편집기 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 대화 상자를 사용하여 웹 서비스 태스크를 구성하려면 WSDL 파일을 로컬에서 사용할 수 있어야 합니다.  
  
-   HTTP 연결 관리자가 웹 사이트로 연결하는 경우 WSDL 파일을 로컬 컴퓨터로 수동으로 복사해야 합니다.  
  
-   HTTP 연결 관리자가 WSDL 파일로 연결하는 경우 웹 서비스 태스크에서 웹 사이트의 파일을 로컬 파일로 다운로드할 수 있습니다.  
  
 WSDL 파일에는 웹 서비스에서 제공하는 메서드, 메서드에 필요한 입력 매개 변수, 메서드가 반환하는 응답 및 웹 서비스와 통신하는 방법이 나열되어 있습니다.  
  
 메서드에서 입력 매개 변수가 사용되는 경우 웹 서비스 태스크에는 매개 변수 값이 필요합니다. 예를 들어 자신의 신장을 기준으로 구입할 스키의 길이를 보여 주는 웹 서비스 메서드에서는 입력 매개 변수로 자신의 신장을 제공해야 합니다. 매개 변수 값은 태스크 내에 정의된 문자열이나 태스크 또는 부모 컨테이너의 범위에 정의된 변수에서 제공할 수 있습니다. 변수를 사용할 경우에는 패키지 구성 또는 스크립트를 사용하여 매개 변수 값을 동적으로 업데이트할 수 있는 이점이 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지 구성](../../integration-services/packages/package-configurations.md)을 참조하세요.  
  
 여러 웹 서비스 메서드에서는 입력 매개 변수가 사용되지 않습니다. 예를 들어 현재 달에 태어난 대통령의 이름을 가져오는 웹 서비스 메서드의 경우에는 웹 서비스가 로컬에서 현재 달을 논리적으로 확인할 수 있기 때문에 입력 매개 변수가 필요하지 않습니다.  
  
 웹 서비스 메서드의 결과는 변수나 파일로 기록될 수 있습니다. 파일 연결 관리자를 사용하면 결과를 기록할 파일을 지정하거나 변수 이름을 제공할 수 있습니다. 자세한 내용은 [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md) 및 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)를 참조하세요.  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>웹 서비스 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 웹 서비스 태스크에 사용할 수 있는 사용자 지정 로그 항목을 보여 줍니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|태스크에서 웹 서비스 액세스를 시작했습니다.|  
|**WSTaskEnd**|태스크에서 웹 서비스 메서드를 완료했습니다.|  
|**WSTaskInfo**|태스크에 대한 설명 정보입니다.|  
  
## <a name="configuration-of-the-web-service-task"></a>웹 서비스 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>프로그래밍 방식으로 웹 서비스 태스크 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="web-service-task-editor-general-page"></a>웹 서비스 태스크 편집기(일반 페이지)
  **웹 서비스 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 HTTP 연결 관리자를 지정하고, 웹 서비스 태스크에 사용하는 WSDL(웹 서비스 기술 언어) 파일의 위치를 지정하고, 웹 서비스 태스크를 설명하고, WSDL 파일을 다운로드할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **HTTPConnection**  
 목록에서 연결 관리자를 선택하거나 \<**New connection...**>를 클릭하여 새 연결 관리자를 만듭니다.  
  
> [!IMPORTANT]  
>  HTTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 **관련 항목:**  [HTTP 연결 관리자](../../integration-services/connection-manager/http-connection-manager.md), [HTTP 연결 관리자 편집기&#40;서버 페이지&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 컴퓨터에 로컬인 WSDL 파일의 정규화된 경로를 입력하거나 찾아보기 단추 **(...)** 를 클릭하여 이 파일을 찾습니다.  
  
 WSDL 파일을 컴퓨터에 이미 수동으로 다운로드한 경우에는 이 파일을 선택하고, WSDL 파일을 아직 다운로드하지 않은 경우에는 다음 단계를 수행합니다.  
  
-   파일 이름 확장명이 ".wsdl"인 빈 파일을 만듭니다.  
  
-   **WSDLFile** 옵션으로 이 빈 파일을 선택합니다.  
  
-   **OverwriteWSDLFile** 값을 **True** 로 설정하여 이 빈 파일을 실제 WSDL 파일로 덮어쓸 수 있도록 합니다.  
  
-   **WSDL 다운로드** 를 클릭하여 실제 WSDL 파일을 다운로드하고 빈 파일을 덮어씁니다.  
  
    > [!NOTE]  
    >  **WSDL 다운로드** 옵션은 **WSDLFile** 상자에 기존 로컬 파일의 이름을 입력할 때까지 사용할 수 없습니다.  
  
 **OverwriteWSDLFile**  
 웹 서비스 태스크에 대한 WSDL 파일을 덮어쓸지 여부를 나타냅니다.  
  
 **WSDL 다운로드** 단추를 사용하여 WSDL 파일을 다운로드하려면 이 값을 **True**로 설정합니다.  
  
 **이름**  
 웹 서비스 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 웹 서비스 태스크에 대한 설명을 입력합니다.  
  
 **WSDL 다운로드**  
 WSDL 파일을 다운로드합니다.  
  
 이 단추는 **WSDLFile** 상자에 기존 로컬 파일의 이름을 입력할 때까지 사용할 수 없습니다.  
  
## <a name="web-service-task-editor-input-page"></a>웹 서비스 태스크 편집기(입력 페이지)
  **웹 서비스 태스크 편집기** 대화 상자의 **입력** 페이지를 사용하여 웹 서비스, 웹 메서드 및 웹 메서드에 입력으로 제공할 값을 지정할 수 있습니다. 문자열을 값 열에 직접 입력하거나 값 열에서 변수를 선택하여 값을 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **서비스**  
 목록에서 웹 메서드를 실행하는 데 사용할 웹 서비스를 선택합니다.  
  
 **메서드**  
 목록에서 실행할 태스크에 사용할 웹 메서드를 선택합니다.  
  
 **WebMethodDocumentation**  
 웹 방식에 대한 설명을 입력하거나 찾아보기 단추 **(...)** 를 클릭하여 **웹 메서드 설명서** 대화 상자에 설명을 입력합니다.  
  
 **이름**  
 웹 메서드에 대한 입력의 이름을 나열합니다.  
  
 **형식**  
 입력의 데이터 형식을 나열합니다.  
  
> [!NOTE]  
>  웹 서비스 태스크는 정수 및 문자열과 같은 기본 형식, 기본 형식의 배열 및 시퀀스, 열거 등과 같은 데이터 형식의 매개 변수만 지원합니다.  
  
 **변수**  
 확인란을 선택하여 입력을 제공하기 위한 변수를 사용합니다.  
  
 **값**  
 Variable 확인란이 선택된 경우 목록에서 변수를 선택하여 입력을 제공하고 선택되지 않은 경우 입력에 사용할 값을 입력합니다.  
  
## <a name="web-service-task-editor-output-page"></a>웹 서비스 태스크 편집기(출력 페이지)
  **웹 서비스 태스크 편집기** 대화 상자의 **출력** 페이지를 사용하여 웹 메서드에서 반환하는 결과를 저장할 위치를 지정할 수 있습니다.  
  
### <a name="static-options"></a>정적 옵션  
 **OutputType**  
 결과를 저장할 때 사용할 스토리지 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 연결**|결과를 파일에 저장합니다. 이 값을 선택하면 동적 옵션 **File**이 표시됩니다.|  
|**변수**|결과를 변수에 저장합니다. 이 값을 선택하면 동적 옵션 **Variable**이 표시됩니다.|  
  
### <a name="outputtype-dynamic-options"></a>OutputType 동적 옵션  
  
#### <a name="outputtype--file-connection"></a>OutputType = 파일 연결  
 **최근에 사용한 파일**  
 목록에서 파일 연결 관리자를 선택하거나 \<**New Connection...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="outputtype--variable"></a>OutputType = 변수  
 **변수**  
 목록에서 변수를 선택하거나 \<**New Variable...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:**  [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>관련 내용  
 MSDN Library의 비디오 - [방법: 웹 서비스 태스크를 사용하여 웹 서비스 호출(SQL Server 비디오)](https://go.microsoft.com/fwlink/?LinkId=259642)을 참조하세요.  
