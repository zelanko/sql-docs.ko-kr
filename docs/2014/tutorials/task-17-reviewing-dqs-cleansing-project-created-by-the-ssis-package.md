---
title: '작업 17: SSIS 패키지에 의해 생성 된 DQS 정리 프로젝트 검토 | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d60355e28327d7953d0782782e3ec55950314fe5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067091"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>태스크 17: SSIS 패키지로 생성된 DQS 정리 프로젝트 검토
  이 작업에서는 DQS 클라이언트에서 SSIS 패키지로 생성된 DQS 프로젝트를 열고, 정리 프로세스의 결과를 검토하고, 선택적으로 대화형 정리를 수행하고, 결과를 내보냅니다.  
  
1.  **Data Quality Client**를 시작 합니다.  
  
2.  **관리** 창에서 **작업 모니터링** 을 클릭 합니다.  
  
3.  **작업 시작 시간** 을 기준으로 목록을 정렬 하 여 최신 레코드를 확인 합니다.  
  
4.  프로젝트 이름이 **Cleanseandcurate**로 표시 됩니다. 공급자 데이터를 정리 합니다. GUID.  
  
     ![SSIS 패키지를 통해 만든 DQS 정리 프로젝트](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "SSIS 패키지를 통해 만든 DQS 정리 프로젝트")  
  
5.  **활성** 필드의 값이 **활성**인지 확인 합니다.  
  
6.  아래쪽 창에서 **프로파일러** 탭을 클릭 하 여 SSIS 패키지에서 수행한 정리 작업의 프로파일러 통계를 확인 합니다.  
  
7.  **닫기** 를 클릭 하 여 **관리** 화면을 닫습니다.  
  
8.  **DQS 클라이언트**의 기본 페이지에 있는 **데이터 품질 프로젝트** 창에서 **데이터 품질 프로젝트 열기** 를 클릭 합니다.  
  
9. 프로젝트 목록에서 SSIS DQS 정리 구성 요소로 생성된 프로젝트를 선택합니다. 프로젝트 이름은 **Cleanseandcurate 형식 이어야 합니다. 공급자 데이터를 정리 합니다. GUID (빨간색)**. **만든 날짜** 열을 기준으로 목록을 정렬 하 고 최신 레코드를 찾아야 할 수도 있습니다.  
  
10. **다음**을 클릭합니다.  
  
11. **결과 관리 및 보기** 페이지는이 자습서의 앞부분에서 수행한 대화형 정리를 통해 잘 알고 있어야 합니다.  
  
12. 정리 결과를 검토합니다. 또한 대화형 정리를 수행하고 다음 페이지에서 결과를 Excel 파일 또는 데이터베이스로 내보낼 수 있습니다.  
  
13. **다음**을 클릭합니다. 이 **내보내기** 페이지에서는 excel 파일, CSV 파일 또는 SQL 데이터베이스로 결과를 내보낼 수 있습니다.  
  
14. **마침** 을 클릭하여 작업을 마칩니다.  
  
15. **DQS 클라이언트**의 기본 페이지에 있는 **관리** 창에서 **작업 모니터링** 을 클릭 합니다.  
  
16. 프로젝트에 대 한 **IsActive** 필드의 값이 이제 **종료** 되었습니다.  
  
## <a name="next-step"></a>다음 단계  
 [결론](../../2014/tutorials/conclusion.md)  
  
  
