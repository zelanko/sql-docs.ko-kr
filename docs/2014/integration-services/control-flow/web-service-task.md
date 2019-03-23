---
title: 웹 서비스 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicetask.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 86b86039f3e308953d41f5a463b0716a76d5c361
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377311"
---
# <a name="web-service-task"></a>웹 서비스 태스크
  웹 서비스 태스크는 웹 서비스 메서드를 실행합니다. 웹 서비스 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   웹 서비스 메서드에서 반환되는 값을 변수에 기록합니다. 예를 들어 웹 서비스 메서드로부터 그 날의 최고 기온을 가져온 다음 이 값을 사용하여 열 값을 설정하는 식에 사용된 변수를 업데이트할 수 있습니다.  
  
-   웹 서비스 메서드에서 반환되는 값을 파일에 기록합니다. 예를 들어 잠재 고객 목록을 파일에 기록하고 패키지에서 이 파일을 데이터 원본으로 사용하여 데이터베이스에 파일을 기록하기 전에 데이터를 정리할 수 있습니다.  
  
## <a name="wsdl-file"></a>WSDL 파일  
 웹 서비스 태스크는 HTTP 연결 관리자를 사용하여 웹 서비스에 연결합니다. HTTP 연결 관리자는 웹 서비스 태스크와 별도로 구성되고 태스크에서 참조됩니다. HTTP 연결 관리자는 서버 URL과 같은 서버 프록시 설정, 웹 서비스 서버 액세스를 위한 자격 증명 및 제한 시간 길이를 지정합니다. 자세한 내용은 [HTTP 연결 관리자](../connection-manager/http-connection-manager.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  HTTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 HTTP 연결 관리자는 웹 사이트 또는 WSDL(Web Service Description Language) 파일로 연결할 수 있습니다. WSDL 파일로 연결하는 HTTP 연결 관리자의 URL에는 `?WSDL` 매개 변수가 포함됩니다(예: `http://MyServer/MyWebService/MyPage.asmx?WSDL`).  
  
 **디자이너에서 제공하는** 웹 서비스 태스크 편집기 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 대화 상자를 사용하여 웹 서비스 태스크를 구성하려면 WSDL 파일을 로컬에서 사용할 수 있어야 합니다.  
  
-   HTTP 연결 관리자가 웹 사이트로 연결하는 경우 WSDL 파일을 로컬 컴퓨터로 수동으로 복사해야 합니다.  
  
-   HTTP 연결 관리자가 WSDL 파일로 연결하는 경우 웹 서비스 태스크에서 웹 사이트의 파일을 로컬 파일로 다운로드할 수 있습니다.  
  
 WSDL 파일에는 웹 서비스에서 제공하는 메서드, 메서드에 필요한 입력 매개 변수, 메서드가 반환하는 응답 및 웹 서비스와 통신하는 방법이 나열되어 있습니다.  
  
 메서드에서 입력 매개 변수가 사용되는 경우 웹 서비스 태스크에는 매개 변수 값이 필요합니다. 예를 들어 자신의 신장을 기준으로 구입할 스키의 길이를 보여 주는 웹 서비스 메서드에서는 입력 매개 변수로 자신의 신장을 제공해야 합니다. 매개 변수 값은 태스크 내에 정의된 문자열이나 태스크 또는 부모 컨테이너의 범위에 정의된 변수에서 제공할 수 있습니다. 변수를 사용할 경우에는 패키지 구성 또는 스크립트를 사용하여 매개 변수 값을 동적으로 업데이트할 수 있는 이점이 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지 구성](../package-configurations.md)을 참조하세요.  
  
 여러 웹 서비스 메서드에서는 입력 매개 변수가 사용되지 않습니다. 예를 들어 현재 달에 태어난 대통령의 이름을 가져오는 웹 서비스 메서드의 경우에는 웹 서비스가 로컬에서 현재 달을 논리적으로 확인할 수 있기 때문에 입력 매개 변수가 필요하지 않습니다.  
  
 웹 서비스 메서드의 결과는 변수나 파일로 기록될 수 있습니다. 파일 연결 관리자를 사용하면 결과를 기록할 파일을 지정하거나 변수 이름을 제공할 수 있습니다. 자세한 내용은 [파일 연결 관리자](../connection-manager/file-connection-manager.md) 및 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md)를 참조하세요.  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>웹 서비스 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 웹 서비스 태스크에 사용할 수 있는 사용자 지정 로그 항목을 보여 줍니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`WSTaskBegin`|태스크에서 웹 서비스 액세스를 시작했습니다.|  
|`WSTaskEnd`|태스크에서 웹 서비스 메서드를 완료했습니다.|  
|`WSTaskInfo`|태스크에 대한 설명 정보입니다.|  
  
## <a name="configuration-of-the-web-service-task"></a>웹 서비스 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [웹 서비스 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [웹 서비스 태스크 편집기&#40;입력 페이지&#41;](../web-service-task-editor-input-page.md)  
  
-   [웹 서비스 태스크 편집기&#40;출력 페이지&#41;](../web-service-task-editor-output-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>프로그래밍 방식으로 웹 서비스 태스크 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="related-content"></a>관련 내용  
 MSDN Library의 비디오 - [방법: 웹 서비스 태스크 (SQL Server 비디오)를 사용 하 여 웹 서비스 호출](https://go.microsoft.com/fwlink/?LinkId=259642), technet.microsoft.com 합니다.  
  
 curatedviews.cloudapp.net의 큐레이트 응답, [스크립트를 사용하여 SSIS의 웹 서비스 사용](https://go.microsoft.com/fwlink/?LinkId=321996)  
  
  
