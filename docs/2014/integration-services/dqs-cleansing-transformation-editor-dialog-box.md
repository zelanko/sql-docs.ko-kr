---
title: DQS 정리 변환 편집기 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssdqs.designer.cleansing.f1
- SQL12.SSDQS.DESIGNER.DQCONNECTION.F1
ms.assetid: 07e79641-71ee-45d0-a9ba-ed6f9f68f333
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cbb5ca8c048b42313b4776b4a2e4b99e44eec406
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059415"
---
# <a name="dqs-cleansing-transformation-editor-dialog-box"></a>DQS 정리 변환 편집기 대화 상자
  **DQS 정리 변환 편집기** 대화 상자를 통해 DQS(Data Quality Services)를 사용하여 데이터를 수정할 수 있습니다. 자세한 내용은 [Data Quality Services Concepts](../../2014/data-quality-services/data-quality-services-concepts.md)을(를) 참조하세요.  
  
 변환에 대한 자세한 내용은 [DQS Cleansing Transformation](data-flow/transformations/dqs-cleansing-transformation.md)을 참조하십시오.  
  
 **수행 작업**  
  
-   [DQS 정리 변환 편집기 열기](#open)  
  
-   [연결 관리자 탭에서 옵션 설정](#connection)  
  
-   [매핑 탭에서 옵션 설정](#mapping)  
  
-   [고급 탭에서 옵션 설정](#advanced)  
  
-   [DQS 정리 연결 관리자 대화 상자에서 옵션 설정](#manager)  
  
##  <a name="open"></a> DQS 정리 변환 편집기 열기  
  
1.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]패키지에 DQS 정리 변환을 추가합니다.  
  
2.  구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
##  <a name="connection"></a> 연결 관리자 탭에서 옵션 설정  
 **데이터 품질 연결 관리자**  
 목록에서 기존 DQS 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **DQS 정리 연결 관리자** 대화 상자를 사용하여 새 연결 관리자를 만듭니다. [DQS 정리 연결 관리자 대화 상자에서 옵션 설정](#manager)을 참조하세요.  
  
 **데이터 품질 기술 자료**  
 연결된 데이터 원본에 대한 기존 DQS 기술 자료를 선택합니다. DQS 기술 자료에 대한 자세한 내용은 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하십시오.  
  
 **연결 암호화**  
 DQS 서버 사이의 데이터 전송을 암호화 하기 위해 연결을 암호화할지 여부를 지정 하 고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]입니다.  
  
 **사용 가능한 도메인**  
 선택한 기술 자료에 사용 가능한 도메인을 나열합니다. 단일 도메인과 둘 이상의 단일 도메인을 포함하는 복합 도메인의 두 가지 도메인 유형이 있습니다.  
  
 복합 도메인에 열을 매핑하는 방법은 [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md)을 참조하십시오.  
  
 도메인에 대한 자세한 내용은 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하십시오.  
  
 **오류 출력 구성**  
 행 수준 오류 처리 방법을 지정합니다. 변환에서 연결된 데이터 원본의 데이터를 수정할 때 예기치 않은 데이터 값 또는 유효성 검사 제약 조건으로 인해 오류가 발생할 수 있습니다.  
  
 유효한 값은 다음과 같습니다.  
  
-   **구성 요소 실패**- 변환에 실패하여 Data Quality Services 데이터베이스에 입력 데이터가 삽입되지 않았음을 나타냅니다. 이것은 기본값입니다.  
  
-   **행 리디렉션**- 입력 데이터가 Data Quality Services 데이터베이스에 삽입되지 않고 오류 출력으로 리디렉션되었음을 나타냅니다.  
  
##  <a name="mapping"></a> 매핑 탭에서 옵션 설정  
 복합 도메인에 열을 매핑하는 방법은 [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md)을 참조하십시오.  
  
 **사용 가능한 입력 열**  
 연결된 데이터 원본의 열을 나열합니다. 수정할 데이터가 들어 있는 하나 이상의 열을 선택합니다.  
  
 **입력 열**  
 **사용 가능한 입력 열** 영역에서 선택한 입력 열을 나열합니다.  
  
 **도메인**  
 입력 열에 매핑할 도메인을 선택합니다.  
  
 **원본 별칭**  
 원래 열 값이 들어 있는 원본 열을 나열합니다.  
  
 열 이름을 수정할 필드를 클릭합니다.  
  
 **출력 별칭**  
 **DQS 정리 변환**을 통해 출력될 열을 나열합니다. 원래 열 값 또는 수정된 값이 들어 있는 열입니다.  
  
 열 이름을 수정할 필드를 클릭합니다.  
  
 **상태 별칭**  
 수정된 데이터에 대한 상태 정보가 들어 있는 열을 나열합니다. 열 이름을 수정할 필드를 클릭합니다.  
  
##  <a name="advanced"></a> 고급 탭에서 옵션 설정  
 **출력 표준화**  
 도메인에 대해 정의된 출력 형식을 기반으로 표준화된 형식으로 데이터를 출력할지 여부를 나타냅니다. 표준화된 형식에 대한 자세한 내용은 [데이터 정리](../../2014/data-quality-services/data-cleansing.md)를 참조하세요.  
  
 **신뢰도**  
 수정된 데이터에 대한 신뢰 수준을 포함할지 여부를 나타냅니다. 신뢰 수준은 수정 내용 또는 제안 내용에 대한 DQS의 확신도를 나타냅니다. 신뢰 수준에 대한 자세한 내용은 [데이터 정리](../../2014/data-quality-services/data-cleansing.md)를 참조하세요.  
  
 **원인**  
 데이터 수정 이유를 포함할지 여부를 나타냅니다.  
  
 **추가된 데이터**  
 기존 참조 데이터 공급자에서 받은 추가 데이터를 출력할지 여부를 나타냅니다. 자세한 내용은 [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)을(를) 참조하세요.  
  
 **추가된 데이터 스키마**  
 데이터 스키마를 출력할지 여부를 나타냅니다. 자세한 내용은 [참조 데이터에 도메인 또는 복합 도메인 연결](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)합니다.  
  
##  <a name="manager"></a> DQS 정리 연결 관리자 대화 상자에서 옵션 설정  
 **서버 이름**  
 연결할 DQS 서버의 이름을 선택하거나 입력합니다. 서버에 대한 자세한 내용은 [DQS Administration](../../2014/data-quality-services/dqs-administration.md)를 참조하십시오.  
  
 **연결 테스트**  
 지정한 연결이 표시되는지 확인하려면 클릭합니다.  
  
 다음을 수행하여 연결 영역에서 **DQS 정리 연결 관리자** 대화 상자를 열 수도 있습니다.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 기존 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 열거나 새 프로젝트를 만듭니다.  
  
2.  연결 영역을 마우스 오른쪽 단추로 클릭하고 **새 연결**을 클릭한 다음 **DQS**를 클릭합니다.  
  
3.  **추가**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본에 데이터 품질 규칙 적용](data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
  
