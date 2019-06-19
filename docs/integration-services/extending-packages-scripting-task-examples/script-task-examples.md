---
title: 스크립트 태스크 예제 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], examples
- examples [Integration Services]
- SSIS Script task, examples
ms.assetid: b0dd77ee-ee11-4cd9-87aa-61dd67f2fe1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5ee2afaf911ac4a3f66a769ded09ed92ebe0dd58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724299"
---
# <a name="script-task-examples"></a>스크립트 태스크 예

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  스크립트 태스크는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 태스크가 충족시키지 않는 거의 모든 요구 사항을 충족시키기 위해 패키지에서 사용할 수 있는 다용도 도구입니다. 이 항목에는 사용 가능한 기능 중 몇 가지를 보여 주는 스크립트 태스크 코드 예제가 나열되어 있습니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
### <a name="example-topics"></a>예 항목  
 이 섹션에는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 스크립트 태스크에 통합할 수 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 클래스의 다양한 용도를 보여 주는 코드 예가 포함되어 있습니다.  
  
 [스크립트 태스크를 사용하여 빈 플랫 파일 검색](../../integration-services/extending-packages-scripting-task-examples/detecting-an-empty-flat-file-with-the-script-task.md)  
 플랫 파일을 검사하여 플랫 파일에 데이터 행이 들어 있는지 확인하고 결과를 제어 흐름 분기에 사용할 수 있도록 변수에 저장합니다.  
  
 [스크립트 태스크를 사용하여 ForEach 루프에 사용할 목록 수집](../../integration-services/extending-packages-scripting-task-examples/gathering-a-list-for-the-foreach-loop-with-the-script-task.md)  
 사용자가 지정한 조건을 만족하는 파일 목록을 수집하고 나중에 Foreach from Variable 열거자에서 사용할 수 있도록 변수를 채웁니다.  
  
 [스크립트 태스크를 사용하여 Active Directory 쿼리](../../integration-services/extending-packages-scripting-task-examples/querying-the-active-directory-with-the-script-task.md)  
 System.DirectoryServices 네임스페이스의 클래스를 사용하여 Active Directory에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 변수 값을 기준으로 사용자 정보를 검색합니다.  
  
 [스크립트 태스크를 사용하여 성능 카운터 모니터링](../../integration-services/extending-packages-scripting-task-examples/monitoring-performance-counters-with-the-script-task.md)  
 System.Diagnostics 네임스페이스의 클래스를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 실행 진행률을 추적하는 데 사용할 수 있는 사용자 지정 성능 카운터를 만듭니다.  
  
 [스크립트 태스크를 사용한 이미지 작업](../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)  
 System.Drawing 네임스페이스의 클래스를 사용하여 이미지를 JPEG 형식으로 압축하고 이 이미지에서 썸네일 이미지를 만듭니다.  
  
 [스크립트 태스크를 사용하여 설치된 프린터 찾기](../../integration-services/extending-packages-scripting-task-examples/finding-installed-printers-with-the-script-task.md)  
 System.Drawing.Printing 네임스페이스의 클래스를 사용하여 설치된 프린터 중 특정 용지 크기를 지원하는 프린터를 찾습니다.  
  
 [스크립트 태스크를 사용하여 HTML 메일 메시지 보내기](../../integration-services/extending-packages-scripting-task-examples/sending-an-html-mail-message-with-the-script-task.md)  
 전자 메일 메시지를 일반 텍스트 형식 대신 HTML 형식으로 보냅니다.  
  
 [스크립트 태스크를 사용한 Excel 파일 작업](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
 Excel 파일의 워크시트를 나열하고 특정 워크시트가 있는지 확인합니다.  
  
 [스크립트 태스크를 사용하여 원격 프라이빗 메시지 큐에 메시지 보내기](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)  
 메시지를 원격 프라이빗 메시지 큐로 보냅니다.  
  
### <a name="other-examples"></a>기타 예  
 다음 항목에도 스크립트 태스크에 사용할 수 있는 코드 예가 포함되어 있습니다.  
  
 [스크립트 태스크에서 변수 사용](../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 다른 변수에 지정된 제한을 초과하는 패키지 변수의 값에 따라 패키지를 계속 실행할지 여부를 사용자가 확인할 수 있도록 합니다.  
  
 [스크립트 태스크에서 데이터 원본에 연결](../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 패키지에 정의된 연결 관리자에서 연결 또는 연결 정보를 검색합니다.  
  
 [스크립트 태스크에서 이벤트 발생](../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 서버의 인터넷 연결 상태에 따라 오류, 경고 또는 정보 메시지를 발생시킵니다.  
  
 [스크립트 태스크에서 로깅](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 태스크에서 처리한 항목 수를 설정된 로그 공급자에 로깅합니다.  
  
  
