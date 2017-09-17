---
title: "DQSInstaller.exe를 사용하여 DQS 기술 자료 내보내기 및 가져오기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e85b9553a3300f51f52fab300642f15f3f08617f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>Dqsinstaller.exe를 사용하여 DQS 기술 자료 내보내기 및 가져오기
  기존 DQS 설치의 경우 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 의 모든 기술 자료를 한 번에 DQS 백업 파일(.dqsb)로 내보낸 다음 나중에 명령 프롬프트에서 DQSInstaller.exe 파일을 실행하여 .dqsb 파일을 통해 다른 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 로 모든 기술 자료를 한 번에 가져올 수 있습니다. 명령 프롬프트에서 DQSInstaller.exe를 실행하는 방법은 [Run DQSInstaller.exe from Command Prompt](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt)에서 [Run DQSInstaller.exe to Complete Data Quality Server Installation](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)을 참조하십시오.  
  
 이 기능을 사용하면 *를 사용하여 각 기술 자료를 .dqs 파일로 개별적으로 내보낼 필요 없이* 의 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 모든 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]기술 자료를 한 번에 백업할 수 있습니다. 마찬가지로 *를 사용하여 .dqs 파일에서 각 기술 자료를 개별적으로 가져올 필요 없이 백업 파일에서 다른* 로 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 모든 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]기술 자료를 한 번에 가져올 수 있습니다. 이 기능은 컴퓨터에서 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]를 제거한 다음 다른 컴퓨터에 다시 설치할 때 기술 자료를 백업 및 복원하는 데 특히 유용합니다. 기존 설치된 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 의 모든 기술 자료를 DQS 백업 파일(.dqsb)로 내보낸 다음 다른 컴퓨터에 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]를 설치한 후 백업 파일에서 모든 기술 자료를 손쉽게 가져올 수 있습니다.  
  
##  <a name="export"></a> .dqsb 파일로 기술 자료 내보내기  
 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]를 제거하는 동안을 비롯하여 언제든지 기존 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]의 모든 기술 자료를 내보낼 수 있습니다.  
  
-   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 의 모든 기술 자료를 DQS 백업 파일(.dqsb)로 내보내려면 기술 자료를 내보낼 전체 경로 및 파일 이름과 함께 명령 프롬프트에서 `exportkbs` 매개 변수를 사용하여 DQSInstaller.exe를 실행합니다. 예를 들어 C: 드라이브의 DQSBackup.dqsb 파일로 모든 기술 자료를 내보내려면:  
  
    ```  
    dqsinstaller.exe –exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  지정된 파일 이름이 지정된 위치에 이미 있는 경우 설치 관리자에서 파일을 덮어쓸지 묻는 메시지를 표시합니다.  
  
-   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]를 제거하는 동안 모든 기술 자료를 DQS 백업 파일로 내보내려면 기술 자료를 내보낼 전체 경로 및 파일 이름과 함께 명령 프롬프트에서 `uninstall` 매개 변수를 사용하여 DQSInstaller.exe를 실행합니다. 예를 들어 C: 드라이브의 DQSBackup.dqsb 파일로 모든 기술 자료를 내보내고 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]의 설치를 해제하려면:  
  
    ```  
    dqsinstaller.exe –uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 매개 변수를 사용하여 명령 프롬프트에서 `uninstall`를 제거하는 동안 DQS 백업 파일의 전체 경로 및 파일 이름을 지정하지 않은 경우 모든 기술 자료가 삭제됨을 알리고 제거 프로세스를 계속할지 여부를 선택하라는 메시지가 표시됩니다.  
  
##  <a name="import"></a> .dqsb 파일에서 기술 자료 가져오기  
 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치를 완료한 후 DQS 백업 파일(.dqsb)에서 모든 기술 자료를 가져올 수 있습니다. 기술 자료를 가져오려면 유효한 DQS 백업 파일(.dqsb)이 있어야 합니다.  
  
 기술 자료를 가져올 전체 경로 및 파일 이름과 함께 명령 프롬프트에서 `importkbs` 매개 변수를 사용하여 DQSInstaller.exe 파일을 실행합니다. 예를 들어 C: 드라이브의 DQSBackup.dqsb 파일에서 모든 기술 자료를 가져오려면:  
  
```  
dqsinstaller.exe –importkbs c:\DQSBackup.dqsb  
```  
  
 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 에 가져오려는 기술 자료와 이름이 같은 기술 자료가 이미 있는 경우 가져온 기술 자료의 이름에 밑줄(_)과 함께 1부터 시작되는 정수 값이 추가됩니다. 예를 들어 "CompanyName" 도메인이 중복된 경우 가져온 도메인 이름은 "CompanyName_1"이 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Run DQSInstaller.exe to Complete Data Quality Server Installation](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [Data Quality Services 설치](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [.dqs 파일로 기술 자료 내보내기](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [.dqs 파일에서 기술 자료 가져오기](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
