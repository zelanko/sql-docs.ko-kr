---
title: Integration Services 경로 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.patheditor.general.f1
- sql13.dts.designer.patheditor.metadata.f1
- sql13.dts.designer.patheditor.visualizers.f1
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: efe52410b491848001fc7e0861e27732d36bc173
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410635"
---
# <a name="integration-services-paths"></a>Integration Services 경로
  경로는 하나의 데이터 흐름 구성 요소의 출력을 다른 구성 요소의 입력에 연결함으로써 데이터 흐름의 두 구성 요소를 연결합니다. 경로에는 원본과 대상이 있습니다. 예를 들어 경로가 OLE DB 원본과 정렬 변환을 연결하는 경우 OLE DB 원본은 경로의 원본이며, 정렬 변환은 경로의 대상입니다. 원본은 경로가 시작되는 구성 요소이며, 대상은 경로가 끝나는 구성 요소입니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지를 실행하는 경우에는 데이터 뷰어를 경로에 연결하여 데이터 흐름의 데이터를 볼 수 있습니다. 표에 데이터를 표시하도록 데이터 뷰어를 구성할 수 있습니다. 데이터 뷰어는 유용한 디버깅 도구입니다. 자세한 내용은 [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md)을 참조하세요.  
  
## <a name="configure-the-path"></a>경로 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 경로 속성을 설정하고, 경로를 통과하는 데이터 열의 메타데이터를 보고, 데이터 뷰어를 구성할 수 있는 **데이터 흐름 경로 편집기** 대화 상자를 제공합니다.  
  
 구성 가능한 경로 속성에는 경로의 이름, 설명 및 주석이 포함됩니다. 또한 경로를 프로그래밍 방식으로 구성할 수 있습니다. 자세한 내용은 [프로그래밍 방식으로 데이터 흐름 구성 요소 연결](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)을 참조하세요.  
  
 경로 주석에는 **디자이너의** 데이터 흐름 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭에서 디자인 화면에 표시된 경로 원본의 이름 또는 경로 이름이 표시됩니다. 경로 주석은 데이터 흐름, 제어 흐름 및 이벤트 처리기에 추가할 수 있는 주석과 비슷합니다. 단지 경로 주석은 경로에 연결되며, 다른 주석은 **디자이너의**데이터 흐름 **,** 제어 흐름 **및**이벤트 처리기 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 테이블에 표시된다는 점만 다릅니다.  
  
 메타데이터에는 이전 구성 요소의 출력에 있는 각 열의 이름, 데이터 형식, 전체 자릿수, 소수 자릿수, 길이, 코드 페이지 및 원본 구성 요소가 표시됩니다. 원본 구성 요소는 해당 열을 만든 데이터 흐름 구성 요소입니다. 이러한 구성 요소는 데이터 흐름에서 첫 번째 구성 요소일 수도 있으며, 아닐 수도 있습니다. 예를 들어 UNION ALL 및 정렬 변환은 해당 열을 만들며, 이는 출력 열에 대한 원본이 됩니다. 반대로 열 복사 변환은 열을 변경하지 않은 상태로 전달하거나 입력 열을 복사하여 새 열을 만들 수도 있습니다. 열 복사 변환은 새로운 열에 대해서만 원본 구성 요소가 됩니다.  

## <a name="set-the-properties-of-a-path-with-the-data-flow-path-editor"></a>데이터 흐름 경로 편집기를 사용하여 경로의 속성 설정
경로는 두 개의 데이터 흐름 구성 요소를 연결합니다. 경로 메타데이터를 설정하려면 데이터 흐름에 적어도 두 개 이상의 연결된 데이터 흐름 구성 요소가 있어야 합니다.
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 후 경로를 두 번 클릭합니다.  
  
4.  **데이터 흐름 경로 편집기**에서 **일반**을 클릭합니다. 그러면 경로의 기본 이름을 편집하고 경로에 대한 설명을 제공할 수 있습니다. 또한 PathAnnotation 속성을 수정할 수 있습니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  

## <a name="general-page---data-flow-path-editor"></a>일반 페이지 - 데이터 흐름 경로 편집기
**데이터 흐름 경로 편집기** 대화 상자를 사용하여 경로 속성을 설정하고, 열 메타데이터를 보고, 경로에 연결된 데이터 뷰어를 관리할 수 있습니다.  
  
 **데이터 흐름 경로 편집기** 대화 상자의 **일반** 노드를 사용하여 경로의 이름을 지정하고 경로를 설명할 수 있을 뿐만 아니라 경로 주석 옵션을 지정할 수 있습니다.  
  
### <a name="options"></a>변수  
 **이름**  
 경로에 사용할 고유 이름을 제공합니다.  
  
 **ID**  
 경로의 계보 식별자입니다. 이 속성은 읽기 전용입니다.  
  
 **IdentificationString**  
 경로를 식별하는 문자열입니다. 위에서 입력한 이름으로 자동으로 생성됩니다.  
  
 **설명**  
 경로에 대한 설명을 입력합니다.  
  
 **PathAnnotation**  
 사용할 주석의 유형을 지정합니다. 주석을 사용하지 않으려면 **Never** 를 선택하고, 요청 시 주석을 사용하려면 **AsNeeded** 를 선택하고, **SourceName** 옵션의 값을 사용하여 자동으로 주석을 달려면 **SourceName** 을 선택하고, **Name** 속성의 값을 사용하여 자동으로 주석을 달려면 **PathName** 을 선택합니다.  
  
 **DestinationName**  
 경로의 끝인 입력을 표시합니다.  
  
 **SourceName**  
 경로의 시작인 출력을 표시합니다.  
 
## <a name="metadata-page---data-flow-path-editor"></a>메타데이터 페이지 - 데이터 흐름 경로 편집기
**데이터 흐름 경로 편집기** 대화 상자의 **메타데이터** 페이지를 사용하여 경로 열의 메타데이터를 볼 수 있습니다.  
  
### <a name="options"></a>변수  
 **경로 메타데이터**  
 열 메타데이터를 나열합니다. 열 데이터를 정렬하려면 열 제목을 클릭합니다.  
  
 **이름**  
 열 이름을 나열합니다.  
  
 **데이터 형식**  
 열의 데이터 형식을 나열합니다.  
  
 **정밀도**  
 숫자 값의 자릿수를 나열합니다.  
  
 **소수 자릿수**  
 숫자 값에서 소수점 이하 자릿수를 나열합니다.  
  
 **길이**  
 현재 열 길이를 나열합니다.  
  
 **코드 페이지**  
 열의 코드 페이지를 나열합니다. 값 **0** 은 열에서 코드 페이지를 사용하지 않음을 나타냅니다. 이는 데이터가 유니코드이거나 데이터에 숫자, 날짜 또는 시간 데이터 형식이 있는 경우 발생합니다.  
  
 **정렬 키 위치**  
 열의 정렬 키 위치를 나열합니다. 값 **0** 은 열이 정렬되어 있지 않음을 나타냅니다.  
  
> [!NOTE]  
>  빼기(-) 접두사는 열이 내림차순으로 정렬되어 있음을 나타냅니다.  
  
 **비교 플래그**  
 열에 적용되는 비교 플래그를 나열합니다.  
  
 **원본 구성 요소**  
 열의 원본인 데이터 흐름 구성 요소를 나열합니다.  
  
 **클립보드로 복사**  
 열 메타데이터를 클립보드로 복사합니다. 기본적으로 모든 메타데이터 행은 현재 표시된 순서대로 정렬되어 복사됩니다.  
 
## <a name="data-viewers-page---data-flow-path-editor"></a>데이터 뷰어 페이지 - 데이터 흐름 경로 편집기
**데이터 흐름 경로 편집기** 대화 상자의 **데이터 뷰어** 페이지를 사용하여 경로에 연결된 데이터 뷰어를 관리할 수 있습니다.  
  
### <a name="options"></a>변수  
 **이름**  
 데이터 뷰어를 나열합니다.  
  
 **데이터 뷰어 유형**  
 데이터 뷰어의 유형을 나열합니다.  
  
 **추가**  
 **데이터 뷰어 구성** 대화 상자를 사용하여 데이터 뷰어를 추가하려면 클릭합니다.  
  
 **Delete**  
 선택한 데이터 뷰어를 삭제하려면 클릭합니다.  
  
 **구성**  
 **데이터 뷰어 구성** 대화 상자를 사용하여 선택한 데이터 뷰어를 구성하려면 클릭합니다.  
 
## <a name="path-properties"></a>Path Properties
[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델의 데이터 흐름 개체에는 구성 요소 수준, 입/출력 수준 및 입/출력 열 수준의 공용 속성과 사용자 지정 속성이 있습니다. 많은 속성은 데이터 흐름 엔진이 런타임에 할당하는 읽기 전용 값을 갖습니다.  
  
 이 항목은 데이터 흐름 개체를 연결하는 경로의 사용자 지정 속성을 나열하고 설명합니다.  
  
### <a name="custom-properties-of-a-path"></a>경로의 사용자 지정 속성  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 데이터 흐름 구성 요소를 연결하는 경로는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 인터페이스를 구현합니다.  
  
 다음 표에서는 데이터 흐름 경로의 구성 가능한 속성에 대해 설명합니다. 데이터 흐름 엔진은 여기에 나열되지 않은 추가 읽기 전용 속성에도 값을 할당합니다.  
  
|속성 이름|데이터 형식|설명|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Integer(열거형)|디자이너 화면에 주석을 경로와 함께 표시할지 여부를 나타내는 값입니다. 가능한 값은 **AsNeeded**, **SourceName**, **PathName**및 **Never**입니다. 기본값은 **AsNeeded**입니다.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|경로에 연결된 입력입니다.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|경로에 연결된 출력입니다.|  
