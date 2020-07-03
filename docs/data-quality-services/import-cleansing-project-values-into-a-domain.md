---
title: 도메인으로 정리 프로젝트 값 가져오기
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importprojectvalues.f1
ms.assetid: f23e38e2-39e0-42d7-abd5-34d8fcca5d2a
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 8688d5d20f1b5ac600e75327725ab18e9f8dba1b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892397"
---
# <a name="import-cleansing-project-values-into-a-domain"></a>도메인으로 정리 프로젝트 값 가져오기

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서는 데이터 품질 정리 프로젝트나 DQS 정리 구성 요소가 포함된 Integration Services 패키지에서 정리 프로세스 중에 수집된 데이터 품질 기술 자료를 도메인으로 가져올 수 있습니다. 이렇게 하면 신뢰할 수 있는 정보가 손실되지 않고 기술 자료가 지속적으로 개선됩니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   Data Quality 클라이언트의 정리 프로젝트나 DQS 정리 구성 요소가 포함된 Integration Services 패키지에서 도메인을 사용한 경우에만 정리 프로젝트 값을 도메인으로 가져올 수 있습니다.  
  
-   Data Quality 클라이언트의 정리 프로젝트나 DQS 정리 구성 요소가 포함된 Integration Services 패키지가 올바르게 완료된 상태여야 합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 정리 프로세스 도중 수집된 데이터 품질 기술 자료를 도메인으로 가져오려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="import-cleansing-project-values"></a><a name="Import"></a> 정리 프로젝트 값 가져오기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client 응용 프로그램을 실행](../data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면의 도메인 관리 작업에서 기술 자료를 엽니다.  
  
3.  기존 도메인에 값을 추가하는 경우 도메인 목록에서 도메인을 선택합니다.  
  
4.  **도메인 값** 탭을 클릭하고 아이콘 표시줄에서 **값 가져오기** 아이콘을 클릭한 후 **프로젝트 값 가져오기**를 클릭합니다. **프로젝트 값 가져오기** 대화 상자가 나타나고 도메인을 사용하여 정리한 데이터 품질 프로젝트 및 Integration Services 패키지의 목록이 표시됩니다.  
  
    > [!NOTE]  
    >  해당 도메인이나 연결된 도메인을 사용하여 프로젝트가 생성되지 않았거나 프로젝트가 완료되지 않은 경우 **프로젝트 값 가져오기** 옵션을 사용할 수 없습니다.  
  
5.  **프로젝트 값 가져오기** 대화 상자에서 다음을 수행합니다.  
  
    -   **가져옴** 드롭다운 목록에서 모든 프로젝트를 표시하려면 **모두** 를 선택하고, 값을 아직 가져오지 않은 프로젝트만 표시하려면 **아니요** 를 선택합니다.  
  
    -   가져올 값이 있는 프로젝트를 선택합니다.  
  
    -   **새 탭에서 값 추가** 를 선택하여 **올바름** 및 **수정됨** 탭의 값 외에 새 탭의 값을 가져옵니다.  
  
    -   **확인**을 클릭합니다.  
  
6.  **도메인 값** 탭으로 전환되고 값을 가져왔다는 메시지가 표시됩니다. 가져와서 도메인에 새로 추가된 값이 **값** 테이블에 표시됩니다.  
  
7.  **새 항목만 표시** 를 선택 취소하여 도메인에 있는 모든 값을 표시합니다.  
  
8.  **올바름**, **오류**또는 **유효하지 않음** 을 선택하여 선택한 형식의 해당 값만 표시합니다.  
  
9. 특정 문자열을 검색하려면 **찾기** 입력란에 문자열을 입력합니다. 위쪽 또는 아래쪽 화살표를 클릭하여 검색 조건에 맞는 값 사이를 이동합니다. 이러한 값은 노란색으로 강조 표시됩니다.  
  
10. **Finish**를 클릭합니다.  
  
    > [!NOTE]  
    >  **도메인 값** 탭의 값에 대한 작업 방법은 [Change Domain Values](../data-quality-services/change-domain-values.md)을 참조하세요.  
  
##  <a name="follow-up-after-importing-project-values-into-a-domain"></a><a name="FollowUp"></a>후속 작업: 도메인에 프로젝트 값을 가져온 후  
 정리 프로세스 도중 수집된 데이터 품질 기술 자료를 도메인으로 가져온 후 도메인 및 값에 대해 다른 도메인 관리 태스크를 수행할 수 있습니다. 자세한 내용은 [도메인 관리](../data-quality-services/managing-a-domain.md)를 참조하세요.  
  
##  <a name="values-that-will-be-imported"></a><a name="Values"></a>가져올 값  
 프로젝트에서 도메인으로 가져올 수 있는 값은 다음과 같습니다.  
  
-   문자열 값만 도메인으로 가져올 수 있습니다.  
  
-   **정리**작업의 **결과 관리 및 보기**페이지에 있는 **수정** , **수정됨** 및 **새로 만들기** 탭의 값만 가져옵니다. **프로젝트 값 가져오기** 대화 상자에서 **새 탭에서 값 추가** 확인란을 선택한 경우에만 **새로 만들기** 탭에 있는 값을 가져옵니다.  
  
-   값은 올바른 값 또는 수정 사항이 있는 오류로 가져올 수 있습니다. 수정 값이 있는 오류 값만 가져올 수 있습니다.  
  
-   수정 값은 기술 자료에 없는 새 값이거나 기존의 올바른 값입니다.  
  
-   레코드 수준이 아닌 값 수준에서 수행된 수정 사항만 기술 자료로 가져올 수 있습니다.  
  
-   가져온 값이 도메인 규칙과 충돌하면 유효하지 않은 값이 생성됩니다.  
  
-   한 번에 여러 프로젝트에서 값을 가져오면 값이 순서대로 추가됩니다.  
  
-   도메인의 용어 기반 관계의 결과로 만들어진 수정 사항은 올바른 값(오류 아님)으로 추가됩니다.  
  
##  <a name="values-that-will-not-be-imported"></a><a name="ValuesNot"></a>가져올 수 없는 값  
 프로젝트에서 도메인으로 가져올 수 없는 값은 다음과 같습니다.  
  
-   **정리** 작업의 **결과 관리 및 보기** 페이지에서 **제안** 및 **유효하지 않음** 탭의 값은 가져올 수 없습니다.  
  
-   정리 프로젝트에 있는 값이 도메인의 기존 값과 충돌할 경우 프로젝트에 있는 값이 생략됩니다. 정리 및 기술 자료 값 사이의 충돌도 포함됩니다.  
  
-   레코드 수준에서 수행된 수정 사항은 기술 자료로 가져올 수 없습니다.  
  
-   대체 값이 참조 데이터 서비스에 의해 수정되거나 올바른 것으로 승인된 경우 도메인으로 값을 가져올 수 없습니다.  
  
-   수정 값이 기술 자료에서 유효하지 않은 값 또는 오류 값으로 표시될 경우 오류 또는 수정 값을 가져올 수 없습니다.  
  
-   도메인이 복합 도메인의 일부이고 정리가 복합 도메인에 대해 수행된 경우 값을 가져올 수 없습니다.  
  
-   기술 자료가 작업 중인 상태이고 가져오기 작업을 수행하는 사용자에 의해 잠긴 경우에만 프로젝트에서 값을 가져올 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 정리](../data-quality-services/data-cleansing.md)   
 [DQS 정리 변환](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
