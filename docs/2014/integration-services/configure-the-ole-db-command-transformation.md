---
title: OLE DB 명령 변환 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [Integration Services]
- OLE DB Command transformation
ms.assetid: c800f167-3d2e-4c10-8ba3-a02f1872ccea
caps.latest.revision: 24
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a29642a667d4d22ecf5c7f6d3de0848b4725df91
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254485"
---
# <a name="configure-the-ole-db-command-transformation"></a>OLE DB 명령 변환 구성
  OLE DB 명령 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 플랫 파일 원본이나 OLE DB 원본과 같은 원본이 이미 들어 있어야 합니다. 이러한 변환은 일반적으로 매개 변수가 있는 쿼리에 사용됩니다.  
  
### <a name="to-configure-the-ole-db-command-transformation"></a>OLE DB 명령 변환을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 OLE DB 명령 변환을 디자인 화면으로 끌어 옵니다.  
  
4.  데이터 원본이나 이전 변환에서 연결선(녹색 또는 빨간색 화살표)을 OLE DB 명령 변환으로 끌어서 OLE DB 명령 변환을 데이터 흐름에 연결합니다.  
  
5.  구성 요소를 마우스 오른쪽 단추로 클릭하고 편집 또는 **고급 편집기 표시**를 클릭합니다.  
  
6.  **연결 관리자** 탭의 **연결 관리자** 목록에서 OLE DB 연결 관리자를 선택합니다. 자세한 내용은 [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
7.  **구성 요소 속성** 탭을 클릭하고 **SqlCommand** 상자의 줄임표 단추 **(…)** 를 클릭합니다.  
  
8.  **문자열 값 편집기**에서 각 매개 변수에 대한 매개 변수 표시자로 물음표(?)를 사용하여 매개 변수가 있는 SQL 문을 입력합니다.  
  
9. **새로 고침**을 클릭합니다. **새로 고침**을 클릭하면 변환이 외부 열 컬렉션의 각 매개 변수에 대한 열을 만들고 DBParamInfoFlags 속성을 설정합니다.  
  
10. **입/출력 속성** 탭을 클릭합니다.  
  
11. **OLE DB 명령 입력**을 확장한 후 **외부 열**을 확장합니다.  
  
12. **외부 열** 목록에 SQL 문의 각 매개 변수에 대한 열이 나열되는지 확인합니다. 열 이름은 **Param_0**, **Param_1**등입니다.  
  
     열 이름은 변경하면 안 됩니다. 열 이름을 변경하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 OLE DB 명령 변환에 대한 유효성 검사 오류가 발생합니다.  
  
     데이터 형식도 변경하면 안 됩니다. 각 열의 DataType 속성은 올바른 데이터 형식으로 설정됩니다.  
  
13. **외부 열** 에 열이 나열되지 않으면 열을 수동으로 추가해야 합니다.  
  
    -   SQL 문의 각 매개 변수에 대해 **열 추가** 를 한 번 클릭합니다.  
  
    -   열 이름을 **Param_0**, **Param_1**등으로 업데이트합니다.  
  
    -   DBParamInfoFlags 속성에 값을 지정합니다. 값은 OLE DB DBPARAMFLAGSENUM 열거의 값과 일치해야 합니다. 자세한 내용은 OLE DB 참조 설명서를 참조하십시오.  
  
    -   열의 데이터 형식을 지정하고 데이터 형식에 따라 열의 코드 페이지, 길이, 전체 자릿수 및 소수 자릿수를 지정합니다.  
  
    -   사용되지 않는 매개 변수를 삭제하려면 **외부 열**에서 매개 변수를 선택한 후 **열 제거**를 클릭합니다.  
  
    -   **열 매핑** 을 클릭하고 **사용 가능한 입력 열** 목록에 있는 열을 **사용 가능한 대상 열** 목록에 있는 매개 변수로 매핑합니다.  
  
14. **확인**을 클릭합니다.  
  
15. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 명령 변환](data-flow/transformations/ole-db-command-transformation.md)   
 [Integration Services 변환](data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](data-flow/integration-services-paths.md)   
 [데이터 흐름 태스크](control-flow/data-flow-task.md)  
  
  
