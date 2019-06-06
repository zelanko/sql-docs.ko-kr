---
title: CreateObject 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 918836e949593672417240c1b91026e1e02c4788
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712316"
---
# <a name="createobject-method-rds"></a>CreateObject 메서드(RDS)
대상 비즈니스 개체에 대 한 프록시를 만들고에 대 한 포인터를 반환 합니다. 인터넷을 통해 요청 및 데이터를 보낼 비즈니스 개체와의 통신에 대 한 서버 쪽 스텁에 프록시 패키징하고 데이터입니다. In-process 구성 요소 개체에 대 한 프록시 사용 되 고, 개체에 대 한 포인터만 제공 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
 원격 데이터 서비스는 다음 프로토콜을 지원합니다. HTTP, HTTPS (HTTP over Secure Socket Layer), DCOM 및 진행 합니다.  
  
|프로토콜|구문|  
|--------------|------------|  
|HTTP|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|HTTPS|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|In-process|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>매개 변수  
 *개체*  
 에 지정 된 형식의 개체로 계산 되는 개체 변수에 *ProgID*합니다.  
  
 *DataSpace*  
 나타내는 개체 변수는 [rds. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 새 개체의 인스턴스를 만드는 데 사용 되는 개체입니다.  
  
 *ProgID*  
 A **문자열** 응용 프로그램의 비즈니스 규칙을 구현 하는 서버 쪽 비즈니스 개체를 지정 하는 프로그래밍 방식 식별자를 포함 하는 값입니다.  
  
 *awebsrvr* 또는 *computername*  
 A **문자열** 서버 비즈니스 개체의 인스턴스가 만들어지는 인터넷 정보 서비스 (IIS) 웹 서버를 식별 하는 URL을 나타내는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 *HTTP 프로토콜* 는 표준 웹 프로토콜입니다. *HTTPS* 는 보안 웹 프로토콜입니다. 사용 된 *DCOM 프로토콜* HTTP 하지 않고도 로컬 영역 네트워크를 실행 하는 경우. 합니다 *프로세스에서* 프로토콜 로컬 동적 연결 라이브러리 (DLL)는 네트워크를 사용 하지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataSpace 개체(RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [DataFactory 개체, 쿼리 메서드 및 CreateObject 메서드 예제 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [DataSpace 개체 및 CreateObject 메서드 예제 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset 메서드(RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


