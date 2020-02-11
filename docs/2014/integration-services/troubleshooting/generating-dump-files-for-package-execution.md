---
title: 패키지 실행을 위한 덤프 파일 생성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8022532dcb038b7c9a5839acb0541337ac3d5001
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62766154"
---
# <a name="generating-dump-files-for-package-execution"></a>패키지 실행을 위한 덤프 파일 생성
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 패키지 실행에 대한 정보를 제공하는 디버그 덤프 파일을 만들 수 있습니다. 이러한 파일의 정보는 패키지 실행 문제를 해결하는 데 도움이 됩니다.  
  
> [!NOTE]  
>  디버그 덤프 파일에는 중요한 정보가 들어 있을 수 있습니다. 중요한 정보를 보호하려면 ACL(액세스 제어 목록)을 통해 파일에 대한 액세스를 제한하거나 파일을 액세스가 제한된 폴더에 복사합니다. 예를 들어 디버그 파일을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 서비스에 보내기 전에 중요한 정보나 기밀 정보를 제거하는 것이 좋습니다.  
  
 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 때는 프로젝트에 포함된 패키지 실행에 대한 정보를 제공하는 덤프 파일을 만들 수 있습니다. ISServerExec.exe 프로세스가 끝나면 덤프 파일이 만들어집니다. **패키지 실행** 대화 상자에서 **오류 덤프** 옵션을 선택하여 패키지 실행 중 오류가 발생하면 덤프 파일이 만들어지도록 지정할 수 있습니다. 다음 저장 프로시저도 사용할 수 있습니다.  
  
-   [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
  
     패키지 실행 중 오류 또는 이벤트가 발생할 때 그리고 특정 이벤트가 발생할 때 덤프 파일을 만들도록 구성하려면 이 저장 프로시저를 호출합니다.  
  
-   [catalog.create_execution_dump](/sql/integration-services/system-stored-procedures/catalog-create-execution-dump)  
  
     실행 중인 패키지를 일시 중지하고 덤프 파일을 만들도록 하려면 이 저장 프로시저를 호출합니다.  
  
 패키지 배포 모델을 사용하여 패키지를 배포하는 경우 명령줄에서 디버그 덤프 옵션을 지정하기 위해 **dtexec** 유틸리티 또는 **dtutil** 유틸리티를 사용하여 디버그 덤프 파일을 만듭니다. 자세한 내용은 [dtexec Utility](../packages/dtexec-utility.md) 및 [dtutil Utility](../dtutil-utility.md)를 참조하세요. 패키지 배포 모델에 대 한 자세한 내용은 [프로젝트 및 패키지 배포](../packages/deploy-integration-services-ssis-projects-and-packages.md) 및 [SSIS&#41;&#40;패키지 배포 ](../packages/legacy-package-deployment-ssis.md)를 참조 하세요.  
  
## <a name="debug-dump-file-format"></a>디버그 덤프 파일 형식  
 디버그 덤프 옵션을 지정하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 다음과 같은 디버그 덤프 파일을 만듭니다.  
  
-   .mdmp 디버그 덤프 파일. 이진 파일입니다.  
  
-   .tmp 디버그 덤프 파일. 텍스트 형식 파일입니다.  
  
 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 이러한 파일을 *\<드라이브>:* \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps 폴더에 저장합니다.  
  
 다음 표에서는 .tmp 파일의 특정 섹션에 대해서만 설명합니다. .tmp 파일에는 이 표에 나열되지 않은 추가 데이터가 포함되어 있습니다.  
  
|정보 유형|Description|예제|  
|-------------------------|-----------------|-------------|  
|Environment|운영 체제 버전, 메모리 사용량 현황 데이터, 프로세스 ID 및 프로세스 이미지 이름. 환경 정보는 .tmp 파일의 시작 부분에 있습니다.|# SSIS Textual Dump taken at 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Image Name [C:\Program Files\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Running on 2 amd64 processors under WOW64<br /><br /> # Memory: 58% in use. Physical: 845M/2044M  Paging: 2404M/4095M (avail/total)|  
|DLL(동적 연결 라이브러리) 경로 및 버전|패키지 처리 시 시스템에서 로드하는 각 DLL의 경로 및 버전 번호|# Loaded Module: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Loaded Module: C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Loaded Module: C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|최근 메시지|시스템에서 표시한 최근 메시지. 각 메시지의 시간, 유형, 설명 및 스레드 ID가 포함됩니다.|[M:1]   Ring buffer entry:              (*pRecord)<br /><br /> [D:2]      <<\<CRingBufferLogging::RingBufferLoggingRecord>>> ( \@ 0282F1A8 )<br /><br /> [E:3]         Time Stamp: 2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         Thread ID: 2368           (ThreadID)<br /><br /> [E:3]         Event Name: OnError                        (EventName)<br /><br /> [E:3]         Source Name:                (SourceName)<br /><br /> [E:3]         Source ID:                        (SourceID)<br /><br /> [E:3]         Execution ID:                 (ExecutionGUID)<br /><br /> [E:3]         Data Code: -1073446879              (DataCode)<br /><br /> [E:3]         설명: 구성 요소가 없거나, 등록되지 않았거나, 업그레이드할 수 없거나, 필수 인터페이스가 없습니다. 이 구성 요소에 대한 연락처 정보는 ""입니다.|  
  
## <a name="related-content"></a>관련 내용  
 [패키지 실행 대화 상자](../execute-package-dialog-box.md)  
  
  
