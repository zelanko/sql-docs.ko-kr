---
description: '5-3단원: Directory 속성 구성 값 수정'
title: '3단계: Directory 속성 구성 값 수정 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a727a5c8d709e982582c26cff8d6cf09eb44ccc
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88345699"
---
# <a name="lesson-5-3-modify-the-directory-property-configuration-value"></a>5-3단원: Directory 속성 구성 값 수정

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



이 작업에서는 패키지 수준 변수 `User::varFolderName`의 **Value** 속성을 설정하도록 **SSISTutorial.dtsConfig** 파일에 저장된 구성 설정을 수정합니다. 이 변수는 Foreach 루프 컨테이너의 **Directory** 속성을 업데이트합니다. 수정된 값은 이전 작업에서 만들어진 **New Sample Data** 폴더를 가리킵니다. 구성 설정을 수정하고 패키지를 실행한 후에 **Directory** 속성은 구성 파일의 변수로부터 업데이트되었습니다. 이전에 **Directory** 속성 값은 패키지의 일부였습니다.  
  
## <a name="modify-the-configuration-setting-of-the-directory-property"></a>Directory 속성의 구성 설정 수정  
  
1.  메모장이나 다른 텍스트 편집기에서 패키지 구성 마법사를 사용하여 이전 작업에서 만든 **SSISTutorial.dtsConfig** 구성 파일을 찾아 엽니다.  
  
2.  **ConfiguredValue** 요소의 값을 변경하여 이전 태스크에서 만든 **New Sample Data** 폴더 경로와 일치시킵니다. 경로를 따옴표로 묶지 마십시오. **New Sample Data** 폴더가 드라이브의 루트 수준(예: **C:\\**)에 있는 경우 업데이트된 XML은 다음 샘플과 비슷해야 합니다.  
  
    ```
    <?xml version="1.0"?>
    <DTSConfiguration>
      <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFEE1D3FA}" GeneratedDate="6/10/2018 8:16:50 AM"/>
      </DTSConfigurationHeading>
      <Configuration ConfiguredType="Property" 
          Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String">
        <ConfiguredValue>C:\New Sample Data</ConfiguredValue>
      </Configuration>
    </DTSConfiguration>  
    ```

    제목 정보인 **GeneratedBy**, **GeneratedFromPackageID** 및 **GeneratedDate** 는 파일과 다릅니다. 주의해야 할 요소는 **Configuration** 입니다. 이제 `User::varFolderName` 변수의 **Value** 속성에는 **C:\New Sample Data** 가 포함됩니다.  
  
3.  변경 내용을 저장하고 텍스트 편집기를 닫습니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동  
[4단계: 5단원 패키지 테스트](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  
