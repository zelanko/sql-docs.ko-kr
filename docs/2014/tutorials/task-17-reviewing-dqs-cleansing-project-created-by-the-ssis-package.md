---
title: '태스크 17: SSIS 패키지에서 프로젝트 생성 된 DQS 정리를 검토 합니다. | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4653ce040e19b82b9e70daa7ebfc02047d71b194
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057852"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>태스크 17: SSIS 패키지로 생성된 DQS 정리 프로젝트 검토
  이 작업에서는 DQS 클라이언트에서 SSIS 패키지로 생성된 DQS 프로젝트를 열고, 정리 프로세스의 결과를 검토하고, 선택적으로 대화형 정리를 수행하고, 결과를 내보냅니다.  
  
1.  시작할 **Data Quality 클라이언트**합니다.  
  
2.  클릭 **작업 모니터링** 에 **관리** 창입니다.  
  
3.  기준으로 목록을 정렬할 **작업 시작 시간** 최신 레코드를 표시 합니다.  
  
4.  다음 형식으로 프로젝트의 이름을 표시 되는지 확인 합니다. **CleanseAndCurate.Cleanse Supplier Data.GUID**합니다.  
  
     ![SSIS 패키지에서 생성 된 DQS 정리 프로젝트](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "SSIS 패키지에서 생성 된 DQS 정리 프로젝트")  
  
5.  값을 **활성** 필드가 **Active**합니다.  
  
6.  클릭 **Profiler** SSIS 패키지가 수행한 정리 작업에 대 한 프로파일러 통계를 보려면 아래쪽 창에서 탭 합니다.  
  
7.  클릭 **닫습니다** 닫으려면 합니다 **관리** 화면.  
  
8.  기본 페이지에서 **DQS 클라이언트**, 클릭 **데이터 품질 프로젝트 열기** 에 **데이터 품질 프로젝트** 창입니다.  
  
9. 프로젝트 목록에서 SSIS DQS 정리 구성 요소로 생성된 프로젝트를 선택합니다. 프로젝트의 이름 형식 이어야 합니다.  **CleanseAndCurate.Cleanse Supplier Data.GUID (빨간색)** 합니다. 기준으로 목록을 정렬 해야 할 수 있습니다 **작성일** 열 및 최신 레코드를 찾습니다.  
  
10. **다음**을 클릭합니다.  
  
11. 합니다 **결과 관리 및 보기** 페이지에서이 자습서의 앞부분에서 수행한 대화형 정리에 대해 잘 알고 있어야 합니다.  
  
12. 정리 결과를 검토합니다. 또한 대화형 정리를 수행하고 다음 페이지에서 결과를 Excel 파일 또는 데이터베이스로 내보낼 수 있습니다.  
  
13. **다음**을 클릭합니다. 이 **내보내기** 페이지를 excel 파일, CSV 파일 또는 SQL database에 결과 내보낼 수 있습니다.  
  
14. **마침** 을 클릭하여 작업을 마칩니다.  
  
15. 기본 페이지에서 **DQS 클라이언트**, 클릭 **활동 모니터링** 에 **관리** 창입니다.  
  
16. 값 **IsActive** 프로젝트에 대 한 필드 **종료 됨** 이제 합니다.  
  
## <a name="next-step"></a>다음 단계  
 [결론](../../2014/tutorials/conclusion.md)  
  
  
