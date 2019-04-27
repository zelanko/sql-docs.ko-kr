---
title: '3단계: Directory 속성 구성 값 수정 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb83ac5bb1b811c23b782b01167c437e9b989518
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767365"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>3단계: Directory 속성 구성 값 수정
  이 태스크에서는 패키지 수준 변수 `User::varFolderName`의 Value 속성에 대해 SSISTutorial.dtsConfig 파일에 저장된 구성 설정을 수정합니다. 이 변수는 Foreach 루프 컨테이너의 Directory 속성을 업데이트합니다. 수정 된 값은 가리킵니다는 `New Sample Data` 이전 태스크에서 만든 폴더에 있습니다. 구성 설정을 수정하고 패키지를 실행하면 Directory 속성은 원래 패키지에서 구성된 디렉터리 값 대신 구성 파일에서 채워진 값을 사용하여 변수를 통해 업데이트됩니다.  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>Directory 속성의 구성 설정을 수정하려면  
  
1.  메모장이나 다른 텍스트 편집기에서 패키지 구성 마법사를 사용하여 이전 태스크에서 만든 SSISTutorial.dtsConfig 구성 파일을 찾아 엽니다.  
  
2.  값을 변경 합니다 **ConfiguredValue** 의 경로 일치 하는 요소는 `New Sample Data` 이전 태스크에서 만든 폴더입니다. 경로를 따옴표로 묶지 마십시오. 경우는 `New Sample Data` 폴더가 드라이브의 루트 수준 (예: c:\\), 업데이트 된 XML 다음 샘플과 유사 해야 합니다.:  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     머리글 정보 `GeneratedBy`, `GeneratedFromPackageID`, 및 **GeneratedDate** 달라 지므로 파일에서 물론입니다. 주의해야 할 요소는 `Configuration`입니다. 이제 변수의 `Value` 속성인 `User::varFolderName`에 C:\New Sample Data가 포함됩니다.  
  
3.  변경 내용을 저장하고 텍스트 편집기를 닫습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [4단계: 5 단원 자습서 패키지 테스트](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
