---
description: Raw File Destination
title: 원시 파일 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfiledest.f1
- sql13.dts.designer.rawfiledestinationconnectionmanager.f1
- sql13.dts.designer.rawfiledestinationcolumns.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 27b28672540d25fe84573c37004161992d3d3827
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194207"
---
# <a name="raw-file-destination"></a>Raw File Destination

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  원시 파일 대상은 원시 데이터를 파일에 기록합니다. 대상의 기본 데이터 형식을 사용하므로 데이터를 변환하거나 구문 분석할 필요도 거의 없습니다. 따라서 원시 파일 대상은 플랫 파일 및 OLE DB 대상과 같은 다른 대상보다 빨리 데이터를 기록할 수 있습니다.  
  
 원시 데이터를 파일에 기록하는 것 외에도 패키지를 실행할 필요 없이 원시 파일 대상을 사용하여 열만 포함된 비어 있는 원시 파일(메타데이터 전용 파일)을 생성할 수 있습니다. 원시 파일 원본을 사용하면 대상이 이전에 기록한 원시 데이터를 검색할 수 있습니다. 또한 원시 파일 원본이 메타데이터 전용 파일을 가리키도록 설정할 수 있습니다.  
  
 원시 파일 서식에는 정렬 정보가 포함됩니다. 원시 파일 대상에는 문자열 열을 위한 비교 플래그를 포함하여 모든 정렬 정보가 저장됩니다. 원시 파일 원본은 정렬 정보를 읽고 적용합니다. 고급 편집기를 사용하면 파일의 정렬 플래그를 무시하도록 원시 파일 원본을 구성할 수 있습니다. 비교 플래그에 대한 자세한 내용은 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)를 참조하십시오.  
  
 다음과 같은 방법으로 원시 파일 대상을 구성할 수 있습니다.  
  
-   원시 파일 대상이 기록할 파일 이름 또는 파일 이름이 포함된 변수인 액세스 모드를 지정합니다.  
  
-   원시 파일 대상이 같은 이름의 기존 파일에 데이터를 추가할지 아니면 새 파일을 만들지 여부를 나타냅니다.  
  
 원시 파일 대상은 패키지 실행 사이에 부분적으로 처리된 데이터의 결과를 즉시 기록하는 데 자주 사용됩니다. 원시 데이터를 저장하면 원시 파일 원본에서 데이터를 신속하게 읽고 최종 대상에 로드되기 전에 추가 변환을 수행할 수 있습니다. 예를 들어 패키지를 여러 번 실행하고 이 때마다 원시 데이터를 파일에 기록할 수 있습니다. 그런 다음에는 다른 패키지에서 원시 파일 원본을 사용하여 각 파일에서 데이터를 읽고, UNION ALL 변환을 사용하여 데이터를 하나의 데이터 집합으로 병합한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블과 같은 최종 대상으로 데이터를 로드하기 전에 데이터를 요약하는 추가 변환을 적용할 수 있습니다.  
  
> [!NOTE]  
>  원시 파일 대상은 BLOB(Binary Large Object) 데이터를 제외한 Null 데이터를 지원합니다.  
  
> [!NOTE]  
>  원시 파일 대상에는 연결 관리자가 사용되지 않습니다.  
  
 이 원본에는 하나의 일반 입력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
## <a name="append-and-new-file-options"></a>추가 및 새 파일 옵션  
 WriteOption 속성에는 기존 파일에 데이터를 추가하거나 새 파일을 만드는 옵션이 포함됩니다.  
  
 다음 표에서는 WriteOption 속성에서 사용할 수 있는 옵션에 대해 설명합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|Append|기존 파일에 데이터를 추가합니다. 추가된 데이터의 메타데이터가 해당 파일 형식과 일치해야 합니다.|  
|항상 만들기|항상 새 파일을 만듭니다.|  
|한 번 만들기|새 파일을 만듭니다. 파일이 있는 경우 구성 요소가 실패합니다.|  
|잘라내기 및 추가|기존 파일을 잘라낸 다음 데이터를 파일에 기록합니다. 추가된 데이터의 메타데이터가 해당 파일 형식과 일치해야 합니다.|  
  
 다음은 데이터 추가와 관련된 중요한 항목입니다.  
  
-   기존 원시 파일에 데이터를 추가해도 데이터가 다시 정렬되지 않습니다.  
  
     정렬된 키가 올바른 순서인지 확인해야 합니다.  
  
-   기존 원시 파일에 데이터를 추가해도 파일 메타데이터(정렬 정보)는 변경되지 않습니다.  
  
 예를 들어 패키지는 ProductKey(PK)로 정렬된 데이터를 읽습니다. 패키지 데이터 흐름은 데이터를 기존 원시 파일에 추가합니다. 패키지를 처음 실행하면 PK 1000, 1100, 1200의 세 개 행이 수신됩니다. 원시 파일에는 이제 다음과 같은 데이터가 포함됩니다.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
 패키지를 두 번째로 실행하면 PK 1001, 1300의 새로운 두 행이 수신됩니다. 원시 파일에는 이제 다음과 같은 데이터가 포함됩니다.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
-   1001, productD  
  
-   1300, productE  
  
 새 데이터가 원시 파일의 끝에 추가되고 정렬된 키(PK)의 순서가 뒤섞입니다. 또한 추가 작업으로 파일 메타데이터(정렬 정보)는 변경되지 않았습니다. 원시 파일 원본을 사용하여 이 파일을 읽으면 이 파일의 데이터가 더 이상 올바른 순서가 아니더라도 구성 요소에 이 파일이 여전히 PK로 정렬된 것으로 표시됩니다.  
  
 데이터를 추가할 때 정렬된 키를 올바른 순서로 유지하기 위해서는 패키지 데이터 흐름을 다음과 같이 디자인할 수 있습니다.  
  
1.  원본 A를 사용하여 새 행을 검색합니다.  
  
2.  원본 B를 사용하여 RawFile1에서 기존 행을 검색합니다.  
  
3.  UNION ALL 변환을 사용하여 원본 A와 원본 B의 입력을 조합합니다.  
  
4.  PK로 정렬합니다.  
  
5.  원시 파일 대상을 사용하여 RawFile2에 기록합니다.  
  
     RawFile1은 데이터 흐름에서 읽는 중이므로 잠겨 있습니다.  
  
6.  RawFile1을 RawFile2로 바꿉니다.  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>루프에서 원시 파일 대상 사용  
 원시 파일 대상을 사용하는 데이터 흐름이 루프에 있는 경우 파일을 한 번만 만들고 루프가 반복되면 파일에 데이터를 추가할 수 있습니다. 파일에 데이터를 추가하려면 추가되는 데이터는 기존 파일의 형식과 일치해야 합니다.  
  
 루프의 첫 번째 반복에서 파일을 만든 다음 루프의 후속 반복에서 행을 추가하려면 디자인 타임에 다음을 수행해야 합니다.  
  
1.  WriteOption 속성을 **CreateOnce** 또는 **CreateAlways** 로 설정하고 루프의 반복 하나를 실행합니다. 파일이 생성됩니다. 이렇게 하면 추가된 데이터와 파일의 메타데이터가 일치하게 됩니다.  
  
2.  WriteOption 속성을 **Append** 로 다시 설정하고 ValidateExternalMetadata 속성을 **False** 로 설정합니다.  
  
 **Append** 옵션 대신에 **TruncateAppend** 옵션을 사용할 경우 이전 반복에서 추가된 행이 잘리고 새 행이 추가됩니다. **TruncateAppend** 옵션을 사용할 경우에도 데이터가 파일 형식과 일치해야 합니다.  
  
## <a name="configuration-of-the-raw-file-destination"></a>원시 파일 대상 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
-   [원시 파일 사용자 지정 속성](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 sqlservercentral.com의 블로그 항목 - [원시 파일의 놀라운 기능](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131)  
  
## <a name="raw-file-destination-editor-connection-manager-page"></a>원시 파일 대상 편집기(연결 관리자 페이지)
  원시 파일 대상 편집기를 사용하여 원시 데이터를 파일에 기록하도록 원시 파일 대상을 구성합니다.  
  
 **수행 작업**  
  
-   [원시 파일 대상 편집기 열기](#open)  
  
-   [연결 관리자 탭에서 옵션 설정](#connection)  
  
-   [열 탭에서 옵션 설정](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> 원시 파일 대상 편집기 열기  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 원시 파일 대상을 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]패키지에 추가합니다.  
  
2.  구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **편집** 을 클릭합니다.  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> 연결 관리자 탭에서 옵션 설정  
 **액세스 모드**  
 파일 이름 지정 방법을 선택합니다. **파일 이름** 을 선택하여 파일 이름 및 경로를 직접 입력하고 **변수를 사용한 파일 이름** 을 선택하여 파일 이름이 포함된 변수를 지정합니다.  
  
 **파일 이름** 또는 **변수 이름**  
 원시 파일의 이름과 경로를 입력하거나 파일 이름이 포함된 변수를 선택합니다.  
  
 **쓰기 옵션**  
 파일을 만들고 파일에 쓰는 데 사용할 메서드를 선택합니다.  
  
 **초기 원시 파일 생성**  
 패키지를 실행할 필요 없이 열만 포함된 빈 원시 파일(메타데이터 전용 파일)을 생성하려면 단추를 클릭합니다. 파일에는 **원시 파일 대상 편집기** 의 **열** 페이지에서 선택한 열이 포함됩니다. 원시 파일 원본이 이 메타데이터 전용 파일을 가리키도록 설정할 수 있습니다.  
  
 **초기 원시 파일 생성** 을 누르면 메시지 상자가 표시됩니다. **확인** 을 클릭하여 파일 만들기를 계속합니다. **열** 페이지의 서로 다른 열 목록을 선택하려면 **취소** 를 클릭합니다.  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> 열 탭에서 옵션 설정  
 **사용 가능한 입력 열**  
 원시 파일에 쓸 하나 이상의 입력 열을 선택합니다.  
  
 **입력 열**  
 입력 열은 **사용 가능한 입력 열** 에서 선택할 경우 이 테이블에 자동으로 추가되거나 이 테이블에서 입력 열을 직접 선택할 수 있습니다.  
  
 **출력 별칭**  
 출력 열에 사용할 대체 이름을 지정합니다.  
  
## <a name="raw-file-destination-editor-columns-page"></a>원시 파일 대상 편집기(열 페이지)
  원시 파일 대상 편집기를 사용하여 원시 데이터를 파일에 기록하도록 원시 파일 대상을 구성합니다.  
  
 **수행 작업**  
  
-   [원시 파일 대상 편집기 열기](#open)  
  
-   [연결 관리자 탭에서 옵션 설정](#connection)  
  
-   [열 탭에서 옵션 설정](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> 원시 파일 대상 편집기 열기  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 원시 파일 대상을 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]패키지에 추가합니다.  
  
2.  구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **편집** 을 클릭합니다.  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> 연결 관리자 탭에서 옵션 설정  
 **액세스 모드**  
 파일 이름 지정 방법을 선택합니다. **파일 이름** 을 선택하여 파일 이름 및 경로를 직접 입력하고 **변수를 사용한 파일 이름** 을 선택하여 파일 이름이 포함된 변수를 지정합니다.  
  
 **파일 이름** 또는 **변수 이름**  
 원시 파일의 이름과 경로를 입력하거나 파일 이름이 포함된 변수를 선택합니다.  
  
 **쓰기 옵션**  
 파일을 만들고 파일에 쓰는 데 사용할 메서드를 선택합니다.  
  
 **초기 원시 파일 생성**  
 패키지를 실행할 필요 없이 열만 포함된 빈 원시 파일(메타데이터 전용 파일)을 생성하려면 단추를 클릭합니다. 원시 파일 원본이 메타데이터 전용 파일을 가리키도록 설정할 수 있습니다.  
  
 단추를 클릭하면 열 목록이 나타납니다. 취소를 클릭하고 열을 수정하거나 확인을 클릭하여 파일 만들기를 계속할 수 있습니다.  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> 열 탭에서 옵션 설정  
 **사용 가능한 입력 열**  
 원시 파일에 쓸 하나 이상의 입력 열을 선택합니다.  
  
 **입력 열**  
 입력 열은 **사용 가능한 입력 열** 에서 선택할 경우 이 테이블에 자동으로 추가되거나 이 테이블에서 입력 열을 직접 선택할 수 있습니다.  
  
 **출력 별칭**  
 출력 열에 사용할 대체 이름을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [원시 파일 원본](../../integration-services/data-flow/raw-file-source.md)   
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
