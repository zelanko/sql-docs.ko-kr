---
title: 사용자 지정 비즈니스 개체 등록 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f998463e0f8190aa040b801d2fd29c732bb31dce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922362"
---
# <a name="registering-a-custom-business-object"></a>사용자 지정 비즈니스 개체 등록
웹 서버를 통해 사용자 지정 비즈니스 개체 (.dll 또는 .exe)를 성공적으로 시작 하려면이 절차에 설명 된 대로 비즈니스 개체의 ProgID를 레지스트리에 입력 해야 합니다. 이 RDS 기능은 사용 권한 실행 파일만 실행 하 여 웹 서버의 보안을 보호 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
> [!NOTE]
>  MDAC 2.0 이상 및 Windows DAC의 경우 기본 비즈니스 개체 [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)는 Mdac/Windows dac를 설치 하는 동안 기본적으로 등록 되지 않습니다. 그러나 설치 전에 **RDSServer. DataFactory** 가 컴퓨터에서 실행을 위해 안전 하 게 등록 된 경우 레지스트리 항목은 새 설치를 위해 유지 관리 됩니다.  
  
### <a name="to-register-a-custom-business-object"></a>사용자 지정 비즈니스 개체를 등록 하려면:  
  
1.  **시작** 을 클릭 한 다음 **실행**을 클릭 합니다.  
  
2.  **RegEdit** 를 입력 하 고 **확인**을 클릭 합니다.  
  
3.  레지스트리 편집기에서 **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\w3svc\parameters\adclaunch** 레지스트리 키로 이동 합니다.  
  
4.  **ADCLaunch** 키를 선택 하 고 **편집**메뉴에서 **새로 만들기** 를 가리킨 다음 **키**를 클릭 합니다.  
  
5.  사용자 지정 비즈니스 개체의 ProgID를 입력 하 고 **Enter 키**를 누릅니다. **값** 항목을 비워 둡니다.


