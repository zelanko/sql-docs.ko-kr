---
description: CreateObject 메서드(RDS)
title: CreateObject 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: rothja
ms.author: jroth
ms.openlocfilehash: ae158d217437184be4ead71beeb2d2404248396f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722439"
---
# <a name="createobject-method-rds"></a>CreateObject 메서드(RDS)
대상 비즈니스 개체에 대 한 프록시를 만들어 해당 개체에 대 한 포인터를 반환 합니다. 프록시 패키지 및는 비즈니스 개체와 통신 하 여 인터넷을 통해 요청 및 데이터를 전송 하기 위해 서버 쪽 스텁으로 데이터를 마샬링합니다. In-process 구성 요소 개체의 경우에는 프록시를 사용 하지 않고 개체에 대 한 포인터만 제공 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
 원격 데이터 서비스는 HTTP, HTTPS (HTTP over Secure Socket Layer), DCOM 및 in-process 프로토콜을 지원 합니다.  
  
|프로토콜|구문|  
|--------------|------------|  
|HTTP|Set object = 스페이스. CreateObject ("ProgId", "https \: //awebsrvr")|  
|HTTPS|Set object = 스페이스. CreateObject ("ProgId", "https \: //awebsrvr")|  
|DCOM|Set object = 스페이스 이름. CreateObject ("ProgId", "computername")|  
|In-Process|Set object = 스페이스. CreateObject ("ProgId", "")|  
  
## <a name="parameters"></a>매개 변수  
 *Object*  
 *ProgID*에 지정 된 형식인 개체로 계산 되는 개체 변수입니다.  
  
 *스페이스가*  
 RDS를 나타내는 개체 변수입니다 [. ](./dataspace-object-rds.md) 새 개체의 인스턴스를 만드는 데 사용 되는 공간 개체입니다.  
  
 *ProgID*  
 응용 프로그램의 비즈니스 규칙을 구현 하는 서버측 비즈니스 개체를 지정 하는 프로그래밍 id를 포함 하는 **문자열** 값입니다.  
  
 *awebsrvr* 또는 *computername*  
 서버 비즈니스 개체의 인스턴스가 만들어진 인터넷 정보 서비스 (IIS) 웹 서버를 식별 하는 URL을 나타내는 **문자열** 값입니다.  
  
## <a name="remarks"></a>설명  
 *HTTP 프로토콜* 은 표준 웹 프로토콜입니다. *HTTPS* 는 보안 웹 프로토콜입니다. HTTP를 사용 하지 않고 로컬 영역 네트워크를 실행 하는 경우 *DCOM 프로토콜* 을 사용 합니다. *In-process* 프로토콜은 로컬 DLL (동적 연결 라이브러리)입니다. 네트워크를 사용 하지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataSpace 개체(RDS)](./dataspace-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [DataFactory 개체, 쿼리 메서드 및 CreateObject 메서드 예제 (VBScript)](./datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [스페이스 개체 및 CreateObject 메서드 예제 (VBScript)](./dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset 메서드(RDS)](./createrecordset-method-rds.md)