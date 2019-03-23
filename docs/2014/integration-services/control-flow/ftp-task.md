---
title: FTP 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.f1
helpviewer_keywords:
- FTP task [Integration Services]
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fcc071c10a2daa31190727dfc9f3cbe617bdcb66
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382201"
---
# <a name="ftp-task"></a>FTP 태스크
  FTP 태스크는 데이터 파일을 다운로드 및 업로드하고 서버의 디렉터리를 관리합니다. 예를 들어 패키지는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 워크플로의 일부로 원격 서버 또는 인터넷 위치에서 데이터 파일을 다운로드할 수 있습니다. FTP 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   데이터를 이동하고 변환을 데이터에 적용하기 전이나 후에 디렉터리 및 데이터 파일을 다른 디렉터리로 복사합니다.  
  
-   원본 FTP 위치에 로그인하고 파일 또는 패키지를 대상 디렉터리로 복사합니다.  
  
-   데이터베이스에 데이터를 로드하기 전에 FTP 위치에서 파일을 다운로드하고 열 데이터에 변환을 적용합니다.  
  
 런타임 시 FTP 태스크는 FTP 연결 관리자를 사용하여 서버에 연결합니다. FTP 연결 관리자는 FTP 태스크와 별도로 구성된 후 FTP 태스크에서 참조됩니다. FTP 연결 관리자에는 서버 설정, FTP 서버 액세스를 위한 자격 증명, 제한 시간 및 서버 연결 다시 시도 횟수와 같은 옵션이 포함되어 있습니다. 자세한 내용은 [FTP 연결 관리자](../connection-manager/ftp-connection-manager.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  FTP 연결 관리자는 익명 인증과 기본 인증만 지원하며 Windows 인증은 지원하지 않습니다.  
  
 로컬 파일이나 로컬 디렉터리에 액세스할 때 FTP 태스크는 파일 연결 관리자 또는 변수에 저장된 경로 정보를 사용합니다. 반면 원격 파일이나 원격 디렉터리에 액세스할 때는 직접 지정된 원격 서버의 경로, FTP 연결 관리자에 지정된 경로 또는 변수에 저장된 경로 정보를 사용합니다. 자세한 내용은 [파일 연결 관리자](../connection-manager/file-connection-manager.md) 및 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md)를 참조하세요.  
  
 이는 FTP 태스크에서 여러 개의 파일을 받고 여러 개의 원격 파일을 삭제할 수 있다는 것을 의미합니다. 그러나 파일 연결 관리자는 하나의 파일만 액세스할 수 있기 때문에 연결 관리자를 사용할 경우 하나의 파일만 보내고 하나의 로컬 파일만 삭제할 수 있습니다. 여러 개의 로컬 파일에 액세스하려면 FTP 태스크에 변수를 사용하여 경로 정보를 제공해야 합니다. 예를 들어 "C:\Test\\*.txt"가 포함된 변수는 Test 디렉터리에서 .txt 확장명을 가진 모든 파일 삭제 또는 보내기를 지원하는 경로를 제공합니다.  
  
 여러 개의 파일을 보내고 여러 개의 로컬 파일 및 디렉터리에 액세스하려면 Foreach 루프에 태스크를 포함하여 FTP 태스크를 여러 번 실행할 수도 있습니다. Foreach 루프는 For Each File 열거자를 사용하여 디렉터리의 모든 파일을 열거할 수 있습니다. 자세한 내용은 [Foreach Loop Container](foreach-loop-container.md)을 참조하세요.  
  
 FTP 태스크는 경로에서 *?* 및 *\** 와일드카드 문자를 지원합니다. 와일드카드 문자를 사용하면 태스크가 여러 개의 파일에 액세스할 수 있습니다. 그러나 와일드카드 문자는 파일 이름을 지정하는 경로 부분에만 사용할 수 있습니다. 예를 들어 C:\MyDirectory\\*.txt는 유효한 경로지만 C:\\\*\MyText.txt는 유효한 경로가 아닙니다.  
  
 작업 실패 시 파일 시스템 태스크를 중지하거나 ASCII 모드로 파일을 전송하도록 FTP 작업을 구성할 수 있습니다. 파일 복사본을 보내고 받는 작업은 대상 파일과 디렉터리를 덮어쓰도록 구성할 수 있습니다.  
  
## <a name="predefined-ftp-operations"></a>미리 정의된 FTP 작업  
 FTP 태스크에는 미리 정의된 작업 집합이 포함되어 있습니다. 다음 표에서는 이러한 작업을 설명합니다.  
  
|연산|Description|  
|---------------|-----------------|  
|파일 보내기|로컬 컴퓨터의 파일을 FTP 서버로 보냅니다.|  
|파일 받기|FTP 서버의 파일을 로컬 컴퓨터에 저장합니다.|  
|로컬 디렉터리 만들기|로컬 컴퓨터에 폴더를 만듭니다.|  
|원격 디렉터리 만들기|FTP 서버에 폴더를 만듭니다.|  
|로컬 디렉터리 제거|로컬 컴퓨터의 폴더를 삭제합니다.|  
|원격 디렉터리 제거|FTP 서버의 폴더를 삭제합니다.|  
|로컬 파일 삭제|로컬 컴퓨터의 파일을 삭제합니다.|  
|원격 파일 삭제|FTP 서버의 파일을 삭제합니다.|  
  
## <a name="custom-log-entries-available-on-the-ftp-task"></a>FTP 태스크에 사용할 수 있는 사용자 지정 로그 항목  
 다음 표에서는 FTP 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`FTPConnectingToServer`|태스크에서 FTP 서버에 대한 연결을 시작했음을 나타냅니다.|  
|`FTPOperation`|태스크에서 수행하는 FTP 작업의 시작 부분과 유형을 보고합니다.|  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)을 참조하세요.  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [FTP 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)   
 [FTP 태스크 편집기&#40;파일 전송 페이지&#41;](../ftp-task-editor-file-transfer-page.md)   
 [Integration Services 태스크](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  
