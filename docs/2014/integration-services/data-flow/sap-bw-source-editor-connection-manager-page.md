---
title: SAP BW 원본 편집기(연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2a6dc531-85ca-43c5-a65f-3ad3f7d537c4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: cfb36f73366487ae413bdbeb7d62cc9aa1026f0b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84914343"
---
# <a name="sap-bw-source-editor-connection-manager-page"></a>SAP BW 원본 편집기(연결 관리자 페이지)
  **SAP BW 원본 편집기** 의 **연결 관리자** 페이지를 사용하여 SAP BW 원본의 SAP BW 연결 관리자를 선택할 수 있습니다. 이 페이지에서는 SAP Netweaver BW 시스템에서 데이터를 추출하기 위한 실행 모드와 매개 변수도 선택합니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 원본 구성 요소에 대한 자세한 내용은 [SAP BW 원본](sap-bw-source.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
 **연결 관리자 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 원본이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 원본을 두 번 클릭합니다.  
  
3.  **SAP BW 원본 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
## <a name="static-options"></a>정적 옵션  
  
> [!NOTE]  
>  원본을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 **SAP BW 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **SAP BW 연결 관리자** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 이 대화 상자에 대한 자세한 내용은 [SAP BW Connection Manager Editor](../sap-bw-connection-manager-editor.md)을 참조하십시오.  
  
 **OHS 대상**  
 원본에서 데이터를 추출하는 데 사용할 OHS(Open Hub Service) 대상을 선택합니다.  
  
 **실행 모드**  
 원본에서 데이터를 추출하는 방법을 지정합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**P - 프로세스 체인 트리거**|프로세스 체인을 트리거합니다. 이 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 추출 프로세스를 시작합니다.|  
|**W - 알릴 때까지 대기**|SAP Netweaver BW 시스템에서 데이터 추출 시작 알림을 기다립니다. 이 경우 SAP Netweaver BW 시스템은 추출 프로세스를 시작합니다.|  
|**E - 추출만**|특정 요청 ID와 연결된 데이터를 검색합니다. 이 경우 SAP Netweaver BW 시스템에서 데이터를 내부 테이블에 이미 추출했으므로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 데이터를 읽기만 합니다.|  
  
 **미리 보기**  
 결과를 미리 볼 수 있는 **미리 보기** 대화 상자를 엽니다. 자세한 내용은 [Preview](preview.md)을(를) 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW 원본 편집기의 **연결 관리자** 페이지에서 사용할 수 있는 **미리 보기** 옵션은 데이터를 실제로 추출합니다. 이전 추출 이후에 변경된 데이터만 추출하도록 SAP Netweaver BW를 구성한 경우 **미리 보기** 를 선택하면 미리 본 데이터가 다음 추출에서 제외됩니다.  
  
 **미리 보기**를 클릭하면 **요청 로그** 대화 상자도 열립니다. 이 대화 상자를 사용하여 샘플 데이터에 대해 SAP Netweaver BW 시스템에 요청하는 동안 기록된 이벤트를 확인할 수 있습니다. 자세한 내용은 [Request Log](request-log.md)을(를) 참조하세요.  
  
## <a name="execution-mode-dynamic-options"></a>실행 모드 동적 옵션  
  
> [!NOTE]  
>  원본을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
### <a name="execution-mode--p---trigger-process-chain"></a>실행 모드 = P - 프로세스 체인 트리거  
  
#### <a name="rfc-destination-options"></a>RFC 대상 옵션  
 이러한 값을 미리 알고 입력할 필요는 없습니다. **조회** 단추를 사용하여 적절한 RFC 대상을 찾고 선택합니다. RFC 대상을 선택하면 이러한 옵션의 적절한 값이 입력됩니다.  
  
 **게이트웨이 호스트**  
 게이트웨이 호스트의 서버 이름 또는 IP 주소를 입력합니다. 일반적으로 이름 또는 IP 주소는 SAP 애플리케이션 서버와 동일합니다.  
  
 **게이트웨이 서비스**  
 게이트웨이 서비스 이름을 `sapgwNN` 형식으로 입력합니다. 여기서 `NN`은 시스템 번호입니다.  
  
 **프로그램 ID**  
 RFC 대상과 연결된 프로그램 ID를 입력합니다.  
  
 **조회**  
 **RFC 대상 조회** 대화 상자를 사용하여 RFC 대상을 조회합니다. 이 대화 상자에 대한 자세한 내용은 [Look Up RFC Destination](look-up-rfc-destination.md)을 참조하십시오.  
  
#### <a name="process-chain-options"></a>프로세스 체인 옵션  
 이러한 값을 미리 알고 입력할 필요는 없습니다. **조회** 단추를 사용하여 적절한 프로세스 체인을 찾고 선택합니다. 프로세스 체인을 선택하면 이 옵션의 적절한 값이 입력됩니다.  
  
 **프로세스 체인**  
 원본에 의해 트리거될 프로세스 체인의 이름을 입력합니다.  
  
 **조회**  
 **프로세스 체인 조회** 대화 상자를 사용하여 프로세스 체인을 조회합니다. 이 대화 상자에 대한 자세한 내용은 [Look Up Process Chain](look-up-process-chain.md)을 참조하십시오.  
  
### <a name="execution-mode--w---wait-for-notify"></a>실행 모드 = W - 알릴 때까지 대기  
  
#### <a name="rfc-destination-options"></a>RFC 대상 옵션  
 이러한 값을 미리 알고 입력할 필요는 없습니다. **조회** 단추를 사용하여 적절한 RFC 대상을 찾고 선택합니다. RFC 대상을 선택하면 이러한 옵션의 적절한 값이 입력됩니다.  
  
 **게이트웨이 호스트**  
 게이트웨이 호스트의 서버 이름 또는 IP 주소를 입력합니다. 일반적으로 이름 또는 IP 주소는 SAP 애플리케이션 서버와 동일합니다.  
  
 **게이트웨이 서비스**  
 게이트웨이 서비스 이름을 `sapgwNN` 형식으로 입력합니다. 여기서 `NN`은 시스템 번호입니다.  
  
 **프로그램 ID**  
 RFC 대상과 연결된 프로그램 ID를 입력합니다.  
  
 **조회**  
 **RFC 대상 조회** 대화 상자를 사용하여 RFC 대상을 조회합니다. 이 대화 상자에 대한 자세한 내용은 [Look Up RFC Destination](look-up-rfc-destination.md)을 참조하십시오.  
  
### <a name="execution-mode--e---extract-only"></a>실행 모드 = E - 추출만  
 **요청 ID**  
 추출과 연결된 요청 ID를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SAP BW 원본 편집기&#40;열 페이지&#41;](sap-bw-source-editor-columns-page.md)   
 [SAP BW 원본 편집기&#40;오류 출력 페이지&#41;](sap-bw-source-editor-error-output-page.md)   
 [SAP BW 원본 편집기&#40;고급 페이지&#41;](sap-bw-source-editor-advanced-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 도움말](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
