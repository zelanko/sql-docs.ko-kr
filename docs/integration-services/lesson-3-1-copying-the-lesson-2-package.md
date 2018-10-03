---
title: '1단계: 2단원 패키지 복사 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2cc63345e757ca07490a6bf365c2523ccda8b0c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761451"
---
# <a name="lesson-3-1---copying-the-lesson-2-package"></a>3-1단원 - 2단원 패키지 복사
이 태스크에서는 2단원에서 만든 Lesson 2.dtsx 패키지의 복사본을 만듭니다. 또는 자습서에 포함되어 있는 완성된 2단원 패키지를 프로젝트에 추가한 다음 복사할 수도 있습니다. 3단원의 나머지 부분에서 이 새 복사본을 사용합니다.  
  
### <a name="to-create-the-lesson-3-package"></a>3단원 패키지를 만들려면  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools를 아직 열지 않은 경우 **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server 2012**를 차례로 가리킨 다음 **SQL Server Data Tools**를 클릭합니다.  
  
2.  **파일** 메뉴에서 **열기**, **프로젝트/솔루션**을 차례로 클릭하고 **SSIS Tutorial** 을 선택한 다음 **열기**를 클릭하고 **SSIS Tutorial.sln**을 두 번 클릭합니다.  
  
3.  솔루션 탐색기에서 **Lesson 2.dtsx**를 마우스 오른쪽 단추로 클릭한 다음 **복사**를 클릭합니다.  
  
4.  솔루션 탐색기에서 **SSIS 패키지**를 마우스 오른쪽 단추로 클릭한 다음 **붙여넣기**를 클릭합니다.  
  
    기본적으로 복사된 패키지의 이름은 Lesson 3.dtsx가 됩니다.  
  
5.  솔루션 탐색기에서 **Lesson 3.dtsx** 를 두 번 클릭하여 패키지를 엽니다.  
  
6.  **제어 흐름** 탭 배경의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
7.  속성 창에서 **Name** 속성을 **Lesson 3**으로 업데이트합니다.  
  
8.  **ID** 속성 상자를 클릭한 다음 목록에서 **<Generate New ID>** 를 클릭합니다.  
  
### <a name="to-add-the-completed-lesson2-package"></a>완성된 2단원 패키지를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 연 다음 SSIS 자습서 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 **SSIS 패키지**를 마우스 오른쪽 단추로 클릭한 다음 **기존 패키지 추가**를 클릭합니다.  
  
3.  **기존 패키지의 복사본 추가** 대화 상자의 **패키지 위치**에서 **파일 시스템**을 선택합니다.  
  
4.  찾아보기 **(…)** 단추를 클릭하여 컴퓨터의 **Lesson 2.dtsx** 로 이동한 다음 **열기**를 클릭합니다.  
  
    이 자습서에 대한 모든 단원 패키지를 다운로드하려면 다음을 수행합니다.  
  
    1.  [Integration Services 제품 예제](http://go.microsoft.com/fwlink/?LinkId=275027)로 이동합니다.  
  
    2.  **DOWNLOADS** 탭을 클릭합니다.  
  
    3.  SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 파일을 클릭합니다.  
  
5.  이전 절차의 3-8단계에서 설명한 대로 3단원 패키지를 복사하여 붙여넣습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[2단계: 로깅 추가 및 구성](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
