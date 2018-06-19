---
title: 새 InfoObject 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3587a633-1c0b-4d63-a22a-6b2b93923c3a
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 30507a5fadbefbbc277dcea923411194232a331b
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35334427"
---
# <a name="create-new-infoobject"></a>새 InfoObject 만들기
  **새 InfoObject 만들기** 대화 상자를 사용하여 SAP Netweaver BW 시스템에서 새 InfoObject를 만들 수 있습니다.  
  
 **InfoObject 만들기** 대화 상자는 **SAP BW 대상 편집기** 의 **연결 관리자**페이지에서 열 수 있습니다. SAP BW 대상에 대한 자세한 내용은 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)을(를) 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **새 InfoObject 만들기 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **연결 관리자** 페이지의 **SAP BW 개체 만들기** 그룹 상자에서 다음 단계 중 하나를 수행하여 InfoObject를 만듭니다.  
  
    1.  InfoObject를 직접 만들려면 **InfoObject**를 선택한 다음 **만들기** 를 클릭하여 **새 InfoObject 만들기** 대화 상자를 엽니다.  
  
    2.  InfoCube를 만드는 동안 InfoObject를 만들려면 **InfoCube**를 선택한 다음 **만들기**를 클릭합니다. **트랜잭션 데이터용 InfoCube 만들기** 대화 상자에 있는 목록의 행 중 하나에 대한 **IObject** 열에서 **만들기** 를 선택하여 **새 InfoObject 만들기** 대화 상자를 엽니다.  
  
        > [!NOTE]  
        >  테이블의 각 행은 패키지의 데이터 흐름에 있는 열을 나타냅니다.  
  
    3.  트랜잭션 데이터용 InfoSouce를 만드는 동안 InfoObject를 만들려면 **InfoSource**를 선택한 다음 **만들기**를 클릭합니다. **InfoSource 만들기** 대화 상자에서 **트랜잭션 데이터**를 선택한 다음 **확인**을 클릭합니다. **트랜잭션 데이터용 InfoSource 만들기** 대화 상자에 있는 목록의 행 중 하나에 대한 **IObject** 열에서 **만들기** 를 선택하여 **새 InfoObject 만들기** 대화 상자를 엽니다.  
  
        > [!NOTE]  
        >  테이블의 각 행은 패키지의 데이터 흐름에 있는 열을 나타냅니다.  
  
    4.  마스터 데이터용 InfoSource를 만드는 동안 InfoObject를 만들려면 **InfoSource**를 선택한 다음 **만들기**를 클릭합니다. **InfoSource 만들기** 대화 상자에서 **마스터 데이터**를 선택한 다음 **확인**을 클릭합니다. **마스터 데이터용 InfoSource 만들기** 대화 상자에서 **새로 만들기** 를 클릭하여 **새 InfoObject 만들기** 대화 상자를 엽니다.  
  
 **새 InfoObject 만들기** 대화 상자의 **특성** 섹션에서 **새로 만들기** 를 클릭하여 **새 InfoObject 만들기** 대화 상자를 열 수도 있습니다.  
  
## <a name="general-options"></a>일반 옵션  
 **특징**  
 차원 데이터를 나타내는 InfoObject를 만듭니다.  
  
 **주요 수치**  
 팩트 데이터를 나타내는 InfoObject를 만듭니다.  
  
 **InfoObject 이름**  
 InfoObject의 이름을 입력합니다.  
  
 **간단한 설명**  
 InfoObject에 대한 간단한 설명을 입력합니다.  
  
 **자세한 설명**  
 InfoObject에 대한 자세한 설명을 입력합니다.  
  
 **마스터 데이터 있음**  
 InfoObject에 특성, 텍스트 또는 계층의 형태로 마스터 데이터가 포함됨을 나타냅니다.  
  
> [!NOTE]  
>  InfoObject가 차원 데이터를 나타내고 **특징** 옵션을 선택한 경우 이 옵션을 선택합니다.  
  
 **소문자 허용**  
 InfoObject 데이터에서 소문자를 허용합니다.  
  
 **저장 및 활성화**  
 새 InfoObject를 저장하고 활성화합니다.  
  
## <a name="data-type-options"></a>데이터 형식 옵션  
 **CHAR - 문자열**  
 InfoObject에 문자 데이터가 포함됨을 나타냅니다.  
  
 **NUMC - 숫자 문자열**  
 InfoObject에 숫자 데이터가 포함됨을 나타냅니다.  
  
 **DATS - 날짜(YYYYMMDD)**  
 InfoObject에 날짜 데이터가 포함됨을 나타냅니다.  
  
 **TIMS - 시간(HHMMSS)**  
 InfoObject에 시간 데이터가 포함됨을 나타냅니다.  
  
 **길이**  
 데이터의 길이를 입력합니다.  
  
## <a name="text-options"></a>텍스트 옵션  
 **텍스트 사용**  
 InfoObject에 텍스트가 포함됨을 나타냅니다.  
  
 **짧은 텍스트**  
 InfoObject에 짧은 텍스트가 포함됨을 나타냅니다.  
  
 **보통 텍스트**  
 InfoObject에 보통 텍스트가 포함됨을 나타냅니다.  
  
 **긴 텍스트**  
 InfoObject에 긴 텍스트가 포함됨을 나타냅니다.  
  
 **언어 종속적 텍스트**  
 텍스트가 언어에 따라 달라짐을 나타냅니다.  
  
 **시간 종속적 텍스트**  
 텍스트가 시간에 따라 달라짐을 나타냅니다.  
  
## <a name="attributes-section"></a>특성 섹션  
 **특성** 섹션은 InfoObject의 특성 목록과 이 목록에서 특성을 추가하고 제거할 수 있는 옵션으로 구성되어 있습니다.  
  
### <a name="attributes-list"></a>특성 목록  
 **특성** 목록에는 만들고 있는 InfoObject의 특성이 표시됩니다. **특성** 목록에는 다음과 같은 열 머리글이 있습니다.  
  
 **InfoObject**  
 InfoObject의 이름을 표시합니다.  
  
 **설명**  
 InfoObject에 대한 설명을 표시합니다.  
  
 **InfoObject 유형**  
 InfoObject의 유형을 표시합니다. 다음 표에서는 유형에 사용할 수 있는 값을 나열합니다.  
  
|값|설명|  
|-----------|-----------------|  
|CHA|특징|  
|KYF|주요 수치|  
|UNI|단위|  
|TIM|시간 특징|  
  
### <a name="attributes-options"></a>특성 옵션  
 다음 옵션을 사용하여 만들고 있는 InfoObject의 특성을 추가하고 제거할 수 있습니다.  
  
 **추가**  
 기존 InfoObject를 특성으로 추가합니다.  
  
 기존 InfoObject를 추가하려면 추가를 클릭한 다음 **InfoObject 조회** 대화 상자를 사용하여 InfoObject를 찾습니다. 이 대화 상자에 대한 자세한 내용은 [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md)을 참조하십시오.  
  
 **새로 만들기**  
 새 InfoObject를 특성으로 추가합니다.  
  
 새 InfoObject를 만들고 추가하려면 새로 만들기를 클릭한 다음 **새 InfoObject 만들기** 대화 상자의 새 인스턴스를 사용하여 새 InfoObject를 만듭니다.  
  
 **제거**  
 선택한 InfoObject를 **특성** 목록에서 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 데이터용 InfoCube 만들기](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [InfoSource 만들기](../../integration-services/data-flow/create-infosource.md)   
 [트랜잭션 데이터용 InfoSource 만들기](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [마스터 데이터용 InfoSource 만들기](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
