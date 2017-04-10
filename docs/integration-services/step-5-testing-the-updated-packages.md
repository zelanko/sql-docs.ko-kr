---
title: "5단계: 업데이트된 패키지 테스트 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
caps.latest.revision: 15
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# 5단계: 업데이트된 패키지 테스트
대상 컴퓨터에 자습서 패키지를 설치하는 데 사용할 배포 번들을 만드는 다음 단원을 진행하기 전에 패키지를 테스트해야 합니다. 이 태스크에서는 Deployment Tutorial 프로젝트에 추가한 후 구성을 사용하여 확장했던 DataTransfer.dtsx 및 LoadXMLData 패키지를 실행합니다.  
  
패키지가 실행되면 패키지의 각 실행 파일은 성공적으로 완료되었을 때 녹색이 됩니다. 모든 실행 파일이 녹색이면 패키지가 성공적으로 완료된 것입니다. 또한 **진행률** 탭에서 패키지 실행 진행률을 볼 수 있습니다.  
  
패키지가 성공적으로 실행되지 않은 경우 다음 단원을 진행하기 전에 패키지를 수정해야 합니다.  
  
### DataTransfer 패키지를 실행하려면  
  
1.  솔루션 탐색기에서 DataTransfer.dtsx를 클릭합니다.  
  
2.  **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.  
  
3.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.  
  
### LoadXMLData 패키지를 실행하려면  
  
1.  솔루션 탐색기에서 LoadXMLData.dtsx를 클릭합니다.  
  
2.  **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.  
  
3.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.  
  
## 다음 단원  
[2단원: SSIS에서 배포 번들 만들기](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
  
  
