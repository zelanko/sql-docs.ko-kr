---
title: "다중 플랫 파일 연결 관리자 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.multifile.advanced.f1
- sql13.dts.designer.multifile.columns.f1
- sql13.dts.designer.multifile.general.f1
- sql13.dts.designer.multifile.preview.f1
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 619bd2c1cfb6336b97ea9226deb184ef070e317e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="multiple-flat-files-connection-manager"></a>다중 플랫 파일 연결 관리자
  다중 플랫 파일 연결 관리자를 사용하면 패키지에서 다중 플랫 파일의 데이터에 액세스할 수 있습니다. 예를 들어 데이터 흐름 태스크가 For 루프 컨테이너와 같은 루프 컨테이너 내부에 있는 경우 플랫 파일 원본에서 다중 플랫 파일 연결 관리자를 사용할 수 있습니다. 각 컨테이너 루프에서 플랫 파일 원본은 다중 플랫 파일 연결 관리자가 제공하는 다음 파일 이름에서 데이터를 로드합니다.  
  
 패키지에 다중 플랫 파일 연결 관리자를 추가하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 다중 플랫 파일 연결로 확인되는 연결 관리자를 만들고, 다중 플랫 파일 연결 관리자의 속성을 설정하며, 다중 플랫 파일 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **MULTIFLATFILE**로 설정됩니다.  
  
 다음과 같은 방법으로 다중 플랫 파일 연결 관리자를 구성할 수 있습니다.  
  
-   사용할 파일, 로캘 및 코드 페이지를 지정합니다. 로캘은 날짜 같은 로캘 구분 데이터를 해석하는 데 사용되고 코드 페이지는 문자열 데이터를 유니코드로 변환하는 데 사용됩니다.  
  
-   파일 형식을 지정합니다. 구분 기호로 분리된 형식, 고정 폭 형식 또는 왼쪽 정렬 형식을 사용할 수 있습니다.  
  
-   머리글 행, 데이터 행 및 열 구분 기호를 지정합니다. 열 구분 기호는 파일 수준에서 설정하고 열 수준에서 덮어쓸 수 있습니다.  
  
-   파일의 첫 번째 행에 열 이름이 포함되는지 여부를 나타냅니다.  
  
-   텍스트 한정자 문자를 지정합니다. 텍스트 한정자를 인식하도록 각 열을 구성할 수 있습니다.  
  
-   개별 열에 대해 이름, 데이터 형식 및 최대 너비와 같은 속성을 설정합니다.  
  
 다중 플랫 파일 연결 관리자에서 다중 파일을 참조하는 경우 파일의 경로는 세로줄 문자(|)로 구분됩니다. 연결 관리자의 **ConnectionString** 속성은 다음 형식을 갖습니다.  
  
 \<*경로*>|\<*경로*>  
  
 또한 와일드카드 문자를 사용하여 다중 파일을 지정할 수 있습니다. 예를 들어 C 드라이브의 모든 텍스트 파일을 참조하려면 **ConnectionString** 속성 값을 C:\\*.txt로 설정할 수 있습니다.  
  
 다중 플랫 파일 연결 관리자에서 다중 파일을 참조하는 경우 모든 파일은 형식이 동일해야 합니다.  
  
 기본적으로 다중 플랫 파일 연결 관리자는 문자열 길이를 50자로 설정합니다. **다중 플랫 파일 연결 관리자 편집기** 대화 상자에서 예제 데이터를 평가하고 이러한 열의 길이를 자동으로 조정하여 데이터가 잘리지 않거나 열 너비를 초과하지 않도록 할 수 있습니다. 플랫 파일 원본 또는 변환에서 열 길이를 조정하지 않으면 열 길이가 데이터 흐름 전체에서 동일하게 유지됩니다. 이러한 열이 보다 좁은 대상 열에 매핑되면 사용자 인터페이스에 경고가 나타나며 런타임 시 데이터 잘림으로 인한 오류가 발생할 수 있습니다. 플랫 파일 연결 관리자, 플랫 파일 원본 또는 변환에서 대상 열과 호환 가능하도록 열 크기를 조정할 수 있습니다. 출력 열의 길이를 수정하려면 **고급 편집기** 대화 상자의 **입/출력 속성** 탭에서 출력 열의 **Length** 속성을 설정합니다.  
  
 연결 관리자를 사용하는 플랫 파일 원본을 추가 및 구성한 후에 다중 플랫 파일 연결 관리자에서 열 길이를 업데이트한 경우에는 플랫 파일 원본에서 출력 열의 크기를 수동으로 조정하지 않아도 됩니다. **플랫 파일 원본** 대화 상자를 열면 플랫 파일 원본에 열 메타데이터를 동기화하는 옵션이 제공됩니다.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>다중 플랫 파일 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="multiple-flat-files-connection-manager-editor-general-page"></a>다중 플랫 파일 연결 관리자 편집기(일반 페이지)
  **다중 플랫 파일 연결 관리자 편집기** 대화 상자의 **일반** 페이지를 사용하여 데이터 형식이 같은 파일 그룹을 선택하고 데이터 형식을 지정할 수 있습니다. 다중 플랫 파일 연결 기능을 사용하면 패키지를 같은 형식의 텍스트 파일 그룹에 연결할 수 있습니다.  
  
 다중 플랫 파일 연결 관리자에 대한 자세한 내용은 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **연결 관리자 이름**  
 워크플로에서의 다중 플랫 파일 연결에 대한 고유 이름을 지정합니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **Description**  
 연결에 대한 설명을 입력합니다. 해당 연결의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **파일 이름**  
 다중 플랫 파일 연결에 사용할 경로와 파일 이름을 입력합니다. "C:\\*.txt"와 같이 와일드카드 문자를 사용하거나 파일 이름을 구분하는 세로줄 문자(|)를 사용하여 다중 파일을 지정할 수 있습니다. 모든 파일의 데이터 형식은 동일해야 합니다.  
  
 **찾아보기**  
 다중 플랫 파일 연결에 사용할 파일 이름을 찾습니다. 여러 파일을 선택할 수 있습니다. 모든 파일의 데이터 형식은 동일해야 합니다.  
  
 **로캘**  
 정렬 순서와 날짜 및 시간 변환 정보를 제공하는 지역을 지정합니다.  
  
 **유니코드**  
 유니코드를 사용할지 여부를 나타냅니다. 유니코드를 사용하면 코드 페이지를 지정할 수 없습니다.  
  
 **코드 페이지**  
 비유니코드 텍스트에 대한 코드 페이지를 지정합니다.  
  
 **형식**  
 구분 기호로 분리됨, 고정 폭, 왼쪽 정렬 중 어떤 서식을 사용할지를 지정합니다. 모든 파일의 데이터 형식은 동일해야 합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|구분 기호로 분리됨|**열** 페이지에 지정된 구분 기호로 열을 구분합니다.|  
|고정 폭|열에 고정 폭이 지정됩니다. 폭은 **열** 페이지의 표식 줄을 끌어 지정할 수 있습니다.|  
|왼쪽 정렬|왼쪽 정렬 파일은 마지막 열을 제외한 모든 열에 고정 폭이 지정된 파일입니다. 마지막 열은 **열** 페이지에서 지정한 행 구분 기호로 구분됩니다.|  
  
 **텍스트 한정자**  
 사용할 텍스트 한정자를 지정합니다. 예를 들어 텍스트 필드를 따옴표로 묶도록 지정할 수 있습니다.  
  
 **머리글 행 구분 기호**  
 구분 기호 목록에서 머리글 행 구분 기호를 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|머리글 행을 캐리지 리턴-줄 바꿈 조합으로 구분합니다.|  
|**{CR}**|머리글 행을 캐리지 리턴으로 구분합니다.|  
|**{LF}**|머리글 행을 줄 바꿈으로 구분합니다.|  
|**세미콜론 {;}**|머리글 행을 세미콜론으로 구분합니다.|  
|**콜론 {:}**|머리글 행을 콜론으로 구분합니다.|  
|**쉼표 {,}**|머리글 행을 쉼표로 구분합니다.|  
|**탭 {t}**|머리글 행을 탭으로 구분합니다.|  
|**세로 막대{&#124;}**|머리글 행을 세로 막대로 구분합니다.|  
  
 **건너뛸 머리글 행**  
 건너뛸 머리글 행 수를 지정합니다(있는 경우).  
  
 **첫 번째 데이터 행의 열 이름**  
 첫 번째 데이터 행에 열 이름을 제공할지 여부를 나타냅니다.  
  
## <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>다중 플랫 파일 연결 관리자 편집기(열 페이지)
  **다중 플랫 파일 연결 관리자 편집기** 대화 상자의 **열** 노드를 사용하여 행 정보 및 열 정보를 지정하고 선택한 첫 번째 파일을 미리 볼 수 있습니다.  
  
 다중 플랫 파일 연결 관리자에 대한 자세한 내용은 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)를 참조하십시오.  
  
### <a name="static-options"></a>정적 옵션  
 **연결 관리자 이름**  
 워크플로에서의 다중 플랫 파일 연결에 대한 고유 이름을 지정합니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **Description**  
 연결에 대한 설명을 입력합니다. 해당 연결의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
### <a name="flat-file-format-dynamic-options"></a>플랫 파일 형식 동적 옵션  
  
#### <a name="format--delimited"></a>형식 = 구분 기호로 분리됨  
 **행 구분 기호**  
 사용 가능한 행 구분 기호의 목록에서 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|행이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.|  
|**{CR}**|행이 캐리지 리턴으로 구분됩니다.|  
|**{LF}**|행이 줄 바꿈으로 구분됩니다.|  
|**세미콜론 {;}**|행이 세미콜론으로 구분됩니다.|  
|**콜론 {:}**|행이 콜론으로 구분됩니다.|  
|**쉼표 {,}**|행이 쉼표로 구분됩니다.|  
|**탭 {t}**|행이 탭으로 구분됩니다.|  
|**세로 막대{&#124;}**|행이 세로 막대로 구분됩니다.|  
  
 **열 구분 기호**  
 사용 가능한 열 구분 기호의 목록에서 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|열이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.|  
|**{CR}**|열이 캐리지 리턴으로 구분됩니다.|  
|**{LF}**|열이 줄 바꿈으로 구분됩니다.|  
|**세미콜론 {;}**|열이 세미콜론으로 구분됩니다.|  
|**콜론 {:}**|열이 콜론으로 구분됩니다.|  
|**쉼표 {,}**|열이 쉼표로 구분됩니다.|  
|**탭 {t}**|열이 탭으로 구분됩니다.|  
|**세로 막대{&#124;}**|열이 세로 막대로 구분됩니다.|  
  
 **열 다시 설정**  
 **열 다시 설정**을 클릭하여 원래 열을 제외한 모든 열을 제거합니다.  
  
#### <a name="format--fixed-width"></a>형식 = 고정 폭  
 **글꼴**  
 미리 보기 데이터를 표시할 글꼴을 선택합니다.  
  
 **원본 데이터 열**  
 세로 행 표식을 밀어 행 너비를 조정하고 미리 보기 창의 맨 위에 있는 눈금자를 클릭하여 열 너비를 조정합니다.  
  
 **행 너비**  
 개별 열의 구분 기호를 추가하기 전에 행 길이를 지정합니다. 또는 미리 보기 창에서 세로줄을 끌어 행의 끝을 표시합니다. 행 너비 값이 자동으로 업데이트됩니다.  
  
 **열 다시 설정**  
 **열 다시 설정**을 클릭하여 원래 열을 제외한 모든 열을 제거합니다.  
  
#### <a name="format--ragged-right"></a>형식 = 왼쪽 정렬  
  
> [!NOTE]  
>  왼쪽 정렬 파일에서는 마지막 열을 제외한 모든 열에 고정 폭이 지정됩니다. 마지막 열은 행 구분 기호로 구분됩니다.  
  
 **글꼴**  
 미리 보기 데이터를 표시할 글꼴을 선택합니다.  
  
 **원본 데이터 열**  
 세로 행 표식을 밀어 행 너비를 조정하고 미리 보기 창의 맨 위에 있는 눈금자를 클릭하여 열 너비를 조정합니다.  
  
 **행 구분 기호**  
 사용 가능한 행 구분 기호의 목록에서 선택하거나 구분 기호 텍스트를 입력합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|행이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.|  
|**{CR}**|행이 캐리지 리턴으로 구분됩니다.|  
|**{LF}**|행이 줄 바꿈으로 구분됩니다.|  
|**세미콜론 {;}**|행이 세미콜론으로 구분됩니다.|  
|**콜론 {:}**|행이 콜론으로 구분됩니다.|  
|**쉼표 {,}**|행이 쉼표로 구분됩니다.|  
|**탭 {t}**|행이 탭으로 구분됩니다.|  
|**세로 막대{&#124;}**|행이 세로 막대로 구분됩니다.|  
  
 **열 다시 설정**  
 **열 다시 설정**을 클릭하여 원래 열을 제외한 모든 열을 제거합니다.  
  
## <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>다중 플랫 파일 연결 관리자 편집기(고급 페이지)
  **다중 플랫 파일 연결 관리자 편집기** 대화 상자의 **고급** 페이지를 사용하여 플랫 파일 연결 관리자에서 연결하는 텍스트 파일에 있는 각 열의 데이터 형식 및 구분 기호와 같은 속성을 설정할 수 있습니다.  
  
 기본적으로 문자열 열의 길이는 50자입니다. 샘플 데이터를 평가한 다음 자동으로 이러한 열의 길이를 조정하여 데이터 잘림이나 열 너비 초과를 방지할 수 있습니다. 또한 대상 열과의 호환성을 위해 다른 메타데이터를 업데이트할 수 있습니다. 예를 들어 정수 데이터만 포함하는 열의 데이터 형식을 DT_I2와 같은 숫자 데이터 형식으로 변경할 수 있습니다.  
  
 다중 플랫 파일 연결 관리자에 대한 자세한 내용은 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **연결 관리자 이름**  
 워크플로에서의 다중 플랫 파일 연결 관리자에 대한 고유 이름을 지정합니다. 제공한 이름은 **디자이너의** 연결 관리자 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 영역에 표시됩니다.  
  
 **Description**  
 연결 관리자에 대한 설명을 입력합니다. 설명에 해당 연결 관리자의 용도를 정의하면 패키지를 이해하기 쉬우며 유지 관리가 간편합니다.  
  
 **각 열의 속성을 구성하십시오.**  
 왼쪽 창에서 열을 선택하면 오른쪽 창에 해당 속성이 표시됩니다. 데이터 형식 속성에 대한 설명은 다음 표를 참조하십시오. 나열된 일부 속성은 일부 플랫 파일 형식에 대해서만 구성 가능합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**ColumnType**|열 유형이 구분 기호로 분리됨, 고정 폭 또는 왼쪽 정렬 중 어떤 것인지를 나타냅니다. 이 속성은 읽기 전용입니다. 왼쪽 정렬 파일은 마지막 열을 제외한 모든 열에 고정 폭이 지정된 파일입니다. 마지막 열은 행 구분 기호로 종료됩니다.|  
|**OutputColumnWidth**|저장할 값을 바이트 수로 지정합니다. 유니코드 파일의 경우 문자 수로 표시됩니다. 데이터 흐름 태스크에서 이 값은 플랫 파일 원본의 출력 열 너비를 설정하는 데 사용됩니다.<br /><br /> 참고: 개체 모델에서 이 속성의 이름은 MaximumWidth입니다.|  
|**DataType**|사용 가능한 데이터 형식의 목록에서 선택합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.|  
|**TextQualified**|텍스트 한정자를 사용하여 텍스트 데이터를 한정할지 여부를 나타냅니다.<br /><br /> **True**: 플랫 파일의 텍스트 데이터가 한정됩니다.<br /><br /> **False**: 플랫 파일의 텍스트 데이터가 한정되지 않습니다.|  
|**이름**|열 이름을 지정합니다. 기본값은 열 번호 매기기 목록이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.|  
|**DataScale**|숫자 데이터의 소수 자릿수를 지정합니다. 소수 자릿수란 소수점 이하 자릿수를 말합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.|  
|**ColumnDelimiter**|사용 가능한 열 구분 기호의 목록에서 선택합니다. 텍스트에 거의 사용되지 않는 구분 기호를 선택합니다. 고정 폭 열에 대해서는 이 값이 무시됩니다.<br /><br /> **{CR}{LF}** – 열이 캐리지 리턴-줄 바꿈 조합으로 구분됩니다.<br /><br /> **{CR}** – 열이 캐리지 리턴으로 구분됩니다.<br /><br /> **{LF}** – 열이 줄 바꿈으로 구분됩니다.<br /><br /> **세미콜론 {;}** – 열이 세미콜론으로 구분됩니다.<br /><br /> **콜론 {:}** – 열이 콜론으로 구분됩니다.<br /><br /> **쉼표 {,}** – 열이 쉼표로 구분됩니다.<br /><br /> **탭 {t}** – 열이 탭으로 구분됩니다.<br /><br /> **세로 막대 {&#124;}** – 열이 세로 막대로 구분됩니다.|  
|**DataPrecision**|숫자 데이터의 전체 자릿수를 지정합니다. 전체 자릿수란 숫자의 자릿수를 말합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.|  
|**InputColumnWidth**|저장할 값을 바이트 수로 지정합니다. 유니코드 파일의 경우 문자 수로 표시됩니다. 구분 기호로 분리된 열에 대해서는 이 값이 무시됩니다.<br /><br /> **참고** 개체 모델에서 이 속성의 이름은 ColumnWidth입니다.|  
  
 **새로 만들기**  
 **새로 만들기**를 클릭하여 새 열을 추가합니다. 기본적으로 **새로 만들기** 단추는 목록 끝에 새 열을 추가합니다. 이 단추의 드롭다운 목록에서 다음 옵션도 사용할 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**열 추가**|목록 끝에 새 열을 추가합니다.|  
|**앞에 삽입**|선택한 열 앞에 새 열을 삽입합니다.|  
|**뒤에 삽입**|선택한 열 뒤에 새 열을 삽입합니다.|  
  
 **Delete**  
 열을 선택한 다음 **삭제**를 클릭하여 제거합니다.  
  
 **유형 제안**  
 **열 유형 제안** 대화 상자를 사용하여 첫 번째로 선택한 파일에 있는 샘플 데이터를 평가하고 각 열의 데이터 형식과 길이에 대한 제안을 가져올 수 있습니다. 자세한 내용은 [열 유형 제안 대화 상자 UI 참조](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)를 참조하세요.  
  
## <a name="multiple-flat-files-connection-manager-editor-preview-page"></a>다중 플랫 파일 연결 관리자 편집기(미리 보기 페이지)
  **다중 플랫 파일 연결 관리자 편집기** 대화 상자의 **미리 보기** 페이지를 사용하여 첫 번째로 선택한 원본 파일의 내용을 정의할 때 해당 내용을 열로 구분해서 볼 수 있습니다.  
  
 다중 플랫 파일 연결 관리자에 대한 자세한 내용은 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **연결 관리자 이름**  
 워크플로에서의 다중 플랫 파일 연결에 대한 고유 이름을 지정합니다. 제공한 이름은 **디자이너의** 연결 관리자 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 영역에 표시됩니다.  
  
 **Description**  
 연결에 대한 설명을 입력합니다. 해당 연결의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **건너뛸 데이터 행**  
 플랫 파일의 시작 부분에서 건너뛸 행 수를 지정합니다.  
  
 **행 미리 보기**  
 선택한 옵션을 사용하여 열과 행으로 구분해서 첫 번째로 선택한 플랫 파일에 있는 샘플 데이터를 검토합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [플랫 파일 원본](../../integration-services/data-flow/flat-file-source.md)   
 [플랫 파일 대상](../../integration-services/data-flow/flat-file-destination.md)   
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
