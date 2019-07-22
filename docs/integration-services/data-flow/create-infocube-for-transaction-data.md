---
title: 트랜잭션 데이터용 InfoCube 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 673cea01-a260-4fce-a1a0-f73839289805
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f0ca83c61a09c03c5c066da4b65a5a342f86c631
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045254"
---
# <a name="create-infocube-for-transaction-data"></a>트랜잭션 데이터용 InfoCube 만들기

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **트랜잭션 데이터용 InfoCube 만들기** 대화 상자를 사용하여 SAP Netweaver BW 시스템에서 트랜잭션 데이터용으로 새 InfoCube를 만들 수 있습니다.  
  
 **SAP BW 대상 편집기** 의 **연결 관리자** 페이지에서 **트랜잭션 데이터용 InfoCube 만들기**대화 상자를 열 수 있습니다. SAP BW 대상에 대한 자세한 내용은 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)을 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **트랜잭션 데이터용 InfoCube 만들기 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **연결 관리자** 페이지의 **SAP BW 개체 만들기** 그룹 상자에서 **InfoCube**를 선택한 다음 **만들기**를 클릭합니다.  
  
## <a name="general-options"></a>일반 옵션  
 **InfoCube 이름**  
 새 InfoCube의 이름을 입력합니다.  
  
 **자세한 설명**  
 새 InfoCube에 대한 설명을 입력합니다.  
  
 **저장 및 활성화**  
 새 InfoCube를 저장하고 활성화합니다.  
  
## <a name="infocube-transfer-structure-options"></a>InfoCube 전송 구조 옵션  
 InfoCube 전송 구조 섹션에서 데이터 흐름 열을 InfoObject에 연결할 수 있습니다.  
  
 **PipelineElement**  
 SAP BW 대상에 연결된 열을 데이터 흐름의 출력에 표시합니다.  
  
 **PipelineDataType**  
 데이터 흐름 열의 데이터 형식을 표시합니다.  
  
 **InfoObject**  
 데이터 흐름 열과 연결된 InfoObject의 이름을 표시합니다.  
  
 **유형**  
 데이터 흐름 열과 연결된 InfoObject의 유형을 표시합니다. 다음 표에서는 유형에 사용할 수 있는 값을 나열합니다.  
  
|값|설명|  
|-----------|-----------------|  
|CHA|특징|  
|UNI|단위|  
|KYF|주요 수치|  
|TIM|시간 특징|  
  
 **Iobject - 검색**  
 기존 InfoObject를 현재 행의 데이터 흐름 열에 연결합니다. 이 연결을 만들려면 **검색**을 클릭한 다음 **InfoObject 조회** 대화 상자를 사용하여 기존 InfoObject를 선택합니다. 이 대화 상자에 대한 자세한 내용은 [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md)을 참조하십시오.  
  
 기존 InfoObject를 선택한 후 **InfoObject** 및 **유형** 열이 선택한 값으로 채워집니다.  
  
 **Iobject - 새로 만들기**  
 새 InfoObject를 만들고 이 InfoObject를 현재 행의 데이터 흐름 열에 연결합니다. 새 InfoObject를 만들려면 **새로 만들기**를 클릭한 다음 **새 InfoObject 만들기** 대화 상자를 사용하여 InfoObject를 만듭니다. 이 대화 상자에 대한 자세한 내용은 [Create New InfoObject](../../integration-services/data-flow/create-new-infoobject.md)을 참조하십시오.  
  
 새 InfoObject를 만든 후 **InfoObject** 및 **유형** 열이 새 값으로 채워집니다.  
  
 **Iobject - 제거**  
 InfoObject와 현재 행의 데이터 흐름 열 간의 연결을 제거합니다. 이 연결을 제거하려면 **제거**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
