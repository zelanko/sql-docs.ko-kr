---
title: OLE DB 명령 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09850707b83481909a881dcefdf00e710e6a8790
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291243"
---
# <a name="ole-db-command-transformation"></a>OLE DB 명령 변환

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 명령 변환은 데이터 흐름의 각 행에 대해 SQL 문을 실행합니다. 예를 들어 데이터베이스 테이블에서 행을 삽입, 업데이트 또는 삭제하는 SQL 문을 실행할 수 있습니다.  
  
 다음과 같은 방법으로 OLE DB 명령 변환을 구성할 수 있습니다.  
  
-   각 행에 대해 변환을 실행하는 SQL 문을 제공합니다.  
  
-   SQL 문이 시간 초과될 때까지 걸리는 시간(초)을 지정합니다.  
  
-   기본 코드 페이지를 지정합니다.  
  
 일반적으로 SQL 문에는 매개 변수가 포함됩니다. 매개 변수 값이 변환 입력의 외부 열에 저장되고 외부 열에 대한 입력 열 매핑으로 입력 열이 매개 변수에 매핑됩니다. 예를 들어 **ProductKey** 열의 값에 따라 **DimProduct** 테이블에서 행을 찾고 삭제하려면 **Param_0** 이라는 외부 열을 **ProductKey** 라는 입력 열에 매핑한 후 `DELETE FROM DimProduct WHERE ProductKey = ?`SQL 문을 실행합니다. OLE DB 명령 변환에는 매개 변수 이름이 제공되며 이 이름은 수정될 수 없습니다. 매개 변수 이름은 **Param_0**, **Param_1**등입니다.  
  
 **고급 편집기** 대화 상자를 사용하여 OLE DB 명령 변환을 구성하는 경우 SQL 문의 매개 변수는 변환 입력의 외부 열에 자동으로 매핑될 수 있으며, 각 매개 변수의 특성은 **새로 고침** 단추를 클릭하여 정의될 수 있습니다. 하지만 OLE DB 명령 변환에서 사용되는 OLE DB Provider가 매개 변수로부터의 매개 변수 정보 파생을 지원하지 않으면 외부 열을 수동으로 구성해야 합니다. 즉, 외부 입력의 각 매개 변수에 대한 열을 변환에 추가하고, **Param_0**과 같은 이름을 사용하도록 열 이름을 업데이트하고, DBParamInfoFlags 속성의 값을 지정하고, 매개 변수 값이 포함된 입력 열을 외부 열로 매핑해야 합니다.  
  
 DBParamInfoFlags의 값은 매개 변수의 특성을 나타냅니다. 예를 들어 값 **1** 은 매개 변수가 입력 매개 변수임을 지정하며, 값 **65** 는 매개 변수가 입력 매개 변수이고 Null 값이 포함될 수 있음을 지정합니다. 값은 OLE DB DBPARAMFLAGSENUM 열거의 값과 일치해야 합니다. 자세한 내용은 OLE DB 참조 설명서를 참조하십시오.  
  
 OLE DB 명령 변환은 **SQLCommand** 사용자 지정 속성을 포함합니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 일반 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="logging"></a>로깅  
 OLE DB 명령 변환이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하여 OLE DB 명령 변환이 수행하는 외부 데이터 원본에 대한 연결 및 명령 문제를 해결할 수 있습니다. OLE DB 명령 변환이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너 또는 개체 모델을 사용하여 변환을 구성할 수 있습니다. 프로그래밍 방식으로 이 변환을 구성하는 방법은 개발자 가이드를 참조하십시오.  
  
## <a name="configure-the-ole-db-command-transformation"></a>OLE DB 명령 변환 구성
  OLE DB 명령 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 플랫 파일 원본이나 OLE DB 원본과 같은 원본이 이미 들어 있어야 합니다. 이러한 변환은 일반적으로 매개 변수가 있는 쿼리에 사용됩니다.  
  
#### <a name="to-configure-the-ole-db-command-transformation"></a>OLE DB 명령 변환을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 OLE DB 명령 변환을 디자인 화면으로 끌어 옵니다.  
  
4.  데이터 원본이나 이전 변환에서 연결선(녹색 또는 빨간색 화살표)을 OLE DB 명령 변환으로 끌어서 OLE DB 명령 변환을 데이터 흐름에 연결합니다.  
  
5.  구성 요소를 마우스 오른쪽 단추로 클릭하고 편집 또는 **고급 편집기 표시**를 클릭합니다.  
  
6.  **연결 관리자** 탭의 **연결 관리자** 목록에서 OLE DB 연결 관리자를 선택합니다. 자세한 내용은 [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
7.  **구성 요소 속성** 탭을 클릭하고 **SqlCommand** 상자의 줄임표 단추 **(...)** 를 클릭합니다.  
  
8.  **문자열 값 편집기**에서 각 매개 변수에 대한 매개 변수 표시자로 물음표(?)를 사용하여 매개 변수가 있는 SQL 문을 입력합니다.  
  
9. **새로 고침**을 클릭합니다. **새로 고침**을 클릭하면 변환이 외부 열 컬렉션의 각 매개 변수에 대한 열을 만들고 DBParamInfoFlags 속성을 설정합니다.  
  
10. **입/출력 속성** 탭을 클릭합니다.  
  
11. **OLE DB 명령 입력**을 확장한 후 **외부 열**을 확장합니다.  
  
12. **외부 열** 목록에 SQL 문의 각 매개 변수에 대한 열이 나열되는지 확인합니다. 열 이름은 **Param_0**, **Param_1**등입니다.  
  
     열 이름은 변경하면 안 됩니다. 열 이름을 변경하면 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에서 OLE DB 명령 변환에 대한 유효성 검사 오류가 발생합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
