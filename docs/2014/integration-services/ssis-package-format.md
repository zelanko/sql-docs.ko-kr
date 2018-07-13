---
title: SSIS 패키지 형식 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c025877f39e66fcf25e6ed2b27d6e1b422a299d9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237123"
---
# <a name="ssis-package-format"></a>SSIS 패키지 형식
  현재 버전의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서는 보다 쉽게 형식을 읽고 패키지를 비교할 수 있도록 패키지 형식(.dtsx 파일)이 크게 변경되었습니다. 또한 이진 형식으로 저장된 충돌하는 변경 내용이 포함되지 않은 패키지를 더욱 안정적으로 병합할 수 있습니다.  
  
 현재 DTSX 패키지 파일 형식을 보려면 [\[MS-DTSX\]: 데이터 변환 서비스 패키지 XML 파일 형식 사양](http://go.microsoft.com/fwlink/?LinkId=233251)을 참조하세요.  
  
 다음 목록에서는 파일 형식 변경 내용을 간략하게 설명합니다. 이러한 변경 내용의 코드 예제를 보려면 [SQL Server 2012의 패키지 형식 변경 내용](http://go.microsoft.com/fwlink/?LinkId=233255)을 참조하십시오.  
  
-   보다 쉽게 .dtsx 파일을 읽고 이해하도록 서식 변환이 적용되었습니다.  
  
-   형식이 더욱 간결해졌습니다. PackageFormatVersion을 제외하고 각 속성의 개별 요소가 특성으로 유지됩니다. 특성이 사전순으로 나열되며, 기본값을 가진 속성이 더 이상 유지되지 않습니다. 마지막으로, 여러 번 나타날 수 있는 요소가 이제 부모 요소 내에 포함됩니다.  
  
-   다른 개체에서 참조할 수 있는 패키지 내의 개체가 대부분 패키지 XML에 정의된 `refId` 특성을 가집니다. 지속적인 계보 ID 대신 이제 `refID`가 유지됩니다. 계보 ID는 런타임 내에서 계속 사용되며 패키지가 로드될 때 다시 생성됩니다.  
  
     `refId` 값은 고유한 문자열을 읽고 이해할 수 있도록 Guid 또는 정수 값과 비교입니다. 문자열은 이전 버전의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 패키지 구성에 사용되는 경로 값과 유사합니다.  
  
     패키지의 두 버전 간의 변경 내용을 병합 하는 경우는 `refId` 수 찾기/바꾸기 작업에서 해당 개체에 대 한 모든 참조를 올바르게 업데이트 되었는지 확인 합니다.  
  
-   레이아웃 정보가 CData 섹션에 포함됩니다.  
  
-   주석은 일반 텍스트로 유지됩니다. 따라서 설명서 자동 생성에 대한 정보를 보다 쉽게 추출할 수 있습니다.  
  
  
