---
title: 유사 항목 그룹화 변환을 사용하여 유사한 데이터 행 식별 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Fuzzy Grouping transformation
- match similar data [Integration Services]
- similar data rows [Integration Services]
- fuzzy matches
ms.assetid: ffcb41a6-e23d-49ea-8c32-ac980e3dc495
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 73675d391e2b53f9cc6fc25824b32d5bdef8d2de
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406265"
---
# <a name="identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation"></a>유사 항목 그룹화 변환을 사용하여 유사한 데이터 행 식별
  유사 항목 그룹화 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크 하나의 원본이 이미 들어 있어야 합니다.  
  
### <a name="to-implement-fuzzy-grouping-transformation-in-a-data-flow"></a>데이터 흐름에서 유사 항목 그룹화 변환을 구현하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 유사 항목 그룹화 변환을 디자인 화면으로 끌어 옵니다.  
  
4.  데이터 원본이나 이전 변환에서 연결선을 유사 항목 그룹화 변환으로 끌어서 유사 항목 그룹화 변환을 데이터 흐름에 연결합니다.  
  
5.  유사 항목 그룹화 변환을 두 번 클릭합니다.  
  
6.  **유사 항목 그룹화 변환 편집기** 대화 상자의 **연결 관리자** 탭에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스로 연결되는 OLE DB 연결 관리자를 선택합니다.  
  
    > [!NOTE]  
    >  변환에는 임시 테이블 및 인덱스를 만들기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결이 필요합니다.  
  
7.  **열** 탭을 클릭하고 **사용 가능한 입력 열** 목록에서 데이터 집합에서 유사 행을 식별하는 데 사용할 입력 열의 확인란을 선택합니다.  
  
8.  **통과** 열의 확인란을 선택하여 변환 출력으로 통과할 입력 열을 식별합니다. 통과 열은 중복 행의 식별 과정에 포함되지 않습니다.  
  
    > [!NOTE]  
    >  그룹화에 사용되는 입력 열은 통과 열로 자동으로 선택되지 않으며 그룹화에 사용되는 경우 선택을 해제할 수 없습니다.  
  
9. 필요에 따라 **출력 별칭** 열에서 출력 열의 이름을 업데이트합니다.  
  
10. 필요에 따라 **그룹 출력 별칭** 열에서 정리된 열의 이름을 업데이트합니다.  
  
    > [!NOTE]  
    >  열의 기본 이름은 "_clean" 접미사가 붙은 입력 열의 이름입니다.  
  
11. 필요에 따라 **일치 유형** 열에서 사용할 일치 유형을 업데이트합니다.  
  
    > [!NOTE]  
    >  적어도 하나 이상의 열에서 유사 항목 일치가 사용되어야 합니다.  
  
12. **최소 유사성** 열에서 최소 유사성 수준 열을 지정합니다. 값은 0에서 1 사이여야 합니다. 값이 1에 가까울수록 입력 열의 유사 값이 그룹으로 묶입니다. 최소 유사성이 1이면 정확히 일치하는 항목을 나타냅니다.  
  
13. 필요에 따라 **유사성 출력 별칭** 열에서 유사성 열의 이름을 업데이트합니다.  
  
14. 데이터 값에 숫자 처리를 지정하려면 **숫자** 열의 값을 업데이트합니다.  
  
15. 변환에서 열의 문자열 데이터를 비교하는 방법을 지정하려면 **비교 플래그** 열에서 기본으로 선택된 비교 옵션을 수정합니다.  
  
16. **고급** 탭을 클릭하여 변환이 고유 행 식별자(_key_in), 중복 행 식별자(_key_out) 및 유사성 값(_score)에 대한 출력에 추가하는 열 이름을 수정합니다.  
  
17. 필요에 따라 슬라이더 막대를 움직여서 유사성 임계값을 조정합니다.  
  
18. 선택적으로 데이터의 구분 기호를 무시하려면 토큰 구분 기호 확인란의 선택을 취소합니다.  
  
19. **확인**을 클릭합니다.  
  
20. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](../../../integration-services/data-flow/integration-services-paths.md)   
 [데이터 흐름 태스크](../../../integration-services/control-flow/data-flow-task.md)  
  
  
